---
name: go-wide
description: Work maximally in parallel (many subagents or parallel tasks, simultaneous builds/tests) while guaranteeing the machine never runs out of memory. Caps this agent session's memory with a cgroup, runs heavy commands in kill-first sub-groups, and starts a watcher that stops runaway jobs by itself. Works with any coding agent on Linux with systemd. Use when the user asks to go wide, max out parallelism or subagents, or invokes /go-wide.
---

# Go wide, memory-safe

Work as parallel as you can: split work across as many subagents or parallel tasks as is useful. **The memory rules below always win over parallelism.**

Scripts: `~/.agents/skills/go-wide/scripts/` (called `$S` below). Always use absolute paths, including in any prompts you hand to subagents.

## 1. Budget, cap and watcher (do first)

1. Run `$S/budget`. It derives everything from this machine: `FLOOR` (RAM always left free; default 20% of total, override with `FLOOR_PCT=<n>`), `CAP` (your memory limit), alert levels and `MAX_JOBS` (core count). Tell the user the numbers in one line.
2. Run `$S/capself`. It finds this agent's process tree (any terminal agent, or an editor bridge such as Zed's `*-acp`), moves it, while it keeps running, into a capped group of `CAP` GiB, and starts a background watcher bound to this session. No restart is needed and no context is lost.
   - "could not find the agent process": rerun with `AGENT_MATCH=<your agent's executable name>`, or `AGENT_ROOT_PID=<pid>`.
   - Exit 2 (no systemd user manager or cgroup v2, e.g. macOS or a container): you are in **watch-only mode**. Skip `memjob`, use half the usual parallelism, and check `free -g` before starting each heavy command.

## 2. Heavy commands go through memjob

Builds, links, test suites, browsers, dev servers, emulators and anything else that may take more than ~500 MB: `$S/memjob <GiB> <command…>`, with a realistic limit (2–4 GiB is typical). A job that exceeds its limit is killed alone; you and the user's desktop survive. Exit code 137 means it hit its limit: retry with a higher limit or less internal parallelism.
- Keep the sum of running memjob limits ≤ `CAP` and parallel compile/test processes ≤ `MAX_JOBS`. Cap link parallelism separately (`--link-jobs`, `-l`).
- Temp files: run commands with `TMPDIR=~/.cache/agent-tmp` (create it if missing). Never put large files in `/tmp` or `/dev/shm`; on many systems they're RAM, and killing a process doesn't free them. Delete temp files when each task finishes.
- If you hand work to subagents, every subagent prompt must include: its memory share, its `-j`/`-n` limit, the memjob rule with the absolute path, and the temp-file rule.

## 3. Watch

The watcher started in step 1 already protects the machine on its own: on every level change it sends a desktop notification and writes a line to `~/.cache/go-wide/memwatch-<pid>.log`, and on CRITICAL it stops the largest memjob by itself.

You should still follow the level so you can pace yourself:
- If your agent can stream a background command's output to you (for example Claude Code's Monitor tool), watch `tail -n0 -F <that log>`.
- Otherwise, read the last line of the log before starting each heavy command or batch of parallel work.

Then act on it:
- **WARNING:** start no new heavy jobs; use lower `-j` on new or restarted commands (a running process can't be changed).
- **CRITICAL:** the watcher stops the largest memjob; the log names it. Tell the user what was stopped, and restart it later with a smaller limit or less parallelism.
- **normal** (after recovery): resume normal pacing.

## Notes
- The cap and watcher last until the agent process exits. A new session or editor restart starts uncapped; running this skill again re-caps it.
- Memory a process held before capping stays counted against its old group; only new allocations count toward the cap.
