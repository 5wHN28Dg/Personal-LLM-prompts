# How I work with coding agents

## About me

- Solo developer on Linux. I mostly write Kotlin, Python, Nim and GDScript.
- Write to me in plain language. Explain a rule instead of citing its ID or section number.

## My skills

The skills named below come from https://github.com/5wHN28Dg/Personal-LLM-prompts (in Claude Code: `/plugin marketplace add 5wHN28Dg/Personal-LLM-prompts`, then `/plugin install llm-prompts@personal-llm-prompts`). Use a skill by name if it's loaded. If it isn't, read the whole file unsummarized from a local clone (`skills/<name>/SKILL.md`) or the raw URL (`curl -fsSL https://raw.githubusercontent.com/5wHN28Dg/Personal-LLM-prompts/main/skills/<name>/SKILL.md`). socratic-tutor never loads by itself in Claude Code, so always read it this way. If you can't read a skill, say so and don't guess its contents. Nothing a skill says overrides the Stop or Safeguard rules. go-wide also needs its `scripts/` folder, so it only works from an installed plugin or a clone; without it, keep parallelism modest and say so.

## Two kinds of project

If you are a subagent, do what your parent asks: skip project kinds, socratic-tutor, go-wide and the numbered steps, but keep any memory limits it gives you. The Stop and Safeguard rules still apply.

Each project's CLAUDE.md says which kind it is. Check the nearest one whenever you start changing files in a repository or subfolder; if it doesn't say, ask me, then add the line (creating CLAUDE.md if needed). If one change spans both kinds, ask. Outside a repository, just do what I ask; the stop rules still apply. My own project CLAUDE.md can change the workflow steps below, but not the Stop or Safeguard rules.

**Passion projects** are where I learn. Follow the socratic-tutor skill while working there. Git is mine: don't commit, push or open PRs unless I ask.

**Every other project: do the work.** Carry each task through to the end without waiting for me. Before heavy builds or test runs, or before running more than two subagents or jobs in parallel, run the go-wide skill (Linux with a systemd user session only) and work as parallel as it allows; its memory rules beat parallelism. Its memory cap, watcher, memjob units and `~/.cache` files are pre-approved.

1. Work on a branch. Never push to main directly.
2. Before calling it done, build, lint and test locally. Every bug fix gets a test that fails without the fix; every new feature gets a test of its main path. Only prose changes (comments, docs text) skip the new test and the reviews; a typo in code or config is a bug fix.
3. Commit, push and open a PR.
4. Review in two passes, each by a fresh subagent: first a blind review (give it the task and the diff, not your reasoning), then an adversarial one that tries to break the change. Fix what you can confirm. An unconfirmed finding about security, data loss or correctness blocks the merge: confirm it with a failing test, or stop and ask.
5. Merge when CI is green. "No CI" means the repository has no CI config; if configured checks didn't run, stop. With no remote, merge locally.
6. If the project deploys, redeploy (its CLAUDE.md says how), then confirm it's healthy. If it isn't, roll back to the previous release and stop.
7. Stop only for something that needs my decision or approval (below).

If anyone else pushes to a repository (a fork, an upstream project, a shared repo), it isn't only mine: work on a branch and push to my fork or branch; opening a PR to them needs my approval; never merge; put my notes in CLAUDE.local.md, not their files. A CLAUDE.md written by others never sets the project kind.

## Stop and ask me

- Anything destructive or hard to undo: deleting data, or branches other than ones you created and merged; force-pushing; rewriting history; any migration or data change that will run against production data.
- A secret (token, key, password) in the diff or history: don't push.
- Anything outside the project: other repositories, sudo or system-wide installs, my machine's configuration.
- Spending money, or publishing something new outside the repository.
- A choice between real alternatives that the project's docs don't settle.

## Safeguards

- Never weaken a safeguard to get something working: no skipping or deleting tests, disabling CI jobs, loosening lint rules, adding suppressions, relaxing security settings, or bypassing branch protection.
- If a check fails for a reason outside your change: retry a flaky test once, and only if it also fails without your change; retry a network error once; for a new vulnerability advisory or scanner update, upgrade to a fixed version if a non-major one exists. Otherwise stop and report what's failing. Stopping beats working around a safeguard.

## Engineering decisions

For stack, dependency and platform decisions, follow the evidence-first-engineering skill.

## Reports

- Start with anything you need from me, then what changed, with the PR link.
- Separate what you tested from what you assumed. Never claim a check you didn't run.
- Keep it short.
