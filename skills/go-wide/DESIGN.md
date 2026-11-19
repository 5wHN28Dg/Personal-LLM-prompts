# go-wide design notes

Decisions that aren't obvious from the scripts, and ideas that were tried and rejected, so they
aren't re-proposed without the evidence. Both designs below went through a blind and an
adversarial review (2026-11-19), with experiments on systemd 259 and Linux 7.0.

## Built: a shared admission ledger (phase 1)

`memjob` claims its limit in `$XDG_RUNTIME_DIR/go-wide/ledger` under `flock`, against the
machine-wide `FREE` from `budget`, before starting. Safety comes from that one global check;
nothing else (session lists, fairness) can loosen it.

- A claim is `claim <pid> <start> <unit> <bytes>`, keyed by the memjob's pid and start time.
  `systemd-run --scope` keeps the pid, so the claim lives exactly as long as the job's main
  process. It counts in full until the job's cgroup has its limit; after that the cgroup's own
  numbers count. (Counting it only "until the cgroup exists" left a window where neither counted.)
- The lock is held only inside a subshell; the job never inherits it. (An inherited lock fd keeps
  the lock for the child's whole life.) Writes go to a temp file and are renamed.
- A job that doesn't fit waits (`want` entries, keyed the same way, so a killed waiter's entry
  disappears), at most `MEMJOB_WAIT` s (default 20, well under an agent tool's timeout), then exits
  75. The oldest waiter's memory is held back from later requests, so a stream of small jobs can't
  starve a big one. A limit above `CEILING` (what would be free with no memjobs) is refused at once.
- If `flock` or `budget` fails, the job starts without admission control, with a warning: no worse
  than before the ledger existed.
- It bounds memjobs only. Agents (each capped at CAP), the desktop and browsers can still grow, so
  memwatch's CRITICAL kill remains the backstop. Scripts from an older plugin version don't claim.

Rejected: a shared parent slice for all memjobs with MemoryMax = total - floor as a kernel backstop.
When it fired, the kernel killed the largest memjob, not the one that grew, and sometimes two
(verified); and it rarely binds, because admission already keeps memjobs well below it.

## Later: fair sharing between sessions (phase 2)

Built and rejected once (PR #5) when each session computed its share alone: sessions with different
views could together hand out more than is free. With the ledger it can sit on top of the global
check. Requirements from review: define a session's reserve as its jobs' limits (1.5 x held for aged
--long jobs); count only sessions that are waiting or running jobs; age wants so the oldest is
admitted once it fits globally, whatever the shares; no heartbeats (pid + start time liveness).

## Rejected for now: SQM-style sharing (protect, throttle, pause)

- `memory.low` between sibling session slices does nothing under machine-wide pressure: its
  ancestors (user.slice, user@.service) have memory.low = 0, and changing that needs root.
- `memory.high` on a job without swap turns a fast kill into a long hang (a 400 MiB job under
  memory.high=300M didn't finish in 60 s) and raised user@1000.service pressure toward
  systemd-oomd's kill threshold.
- Freezing a job frees nothing unless its swap limit is raised and `memory.reclaim` pushes it out;
  the 4 GiB swap file caps the gain; `systemctl stop` refuses a frozen unit (it would disable the
  CRITICAL kill unless it uses `kill -s KILL`); clients of a frozen server hang instead of failing.
- Per-session slices nest one level deeper and would hide jobs from the `find -maxdepth 5` scans.

Real SQM-like protection needs system-level setup (memory.low on user slices, zram): the owner's
call, not something the skill does.
