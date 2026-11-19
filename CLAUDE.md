# Personal-LLM-prompts

Project kind: do the work (not a passion project).

Tests, after changing the go-wide scripts:
- `TMPDIR=~/.cache/agent-tmp sh skills/go-wide/tests/test-budget` checks the memory budget arithmetic against fake cgroups.
- `sh skills/go-wide/tests/test-capagent` needs a systemd user session and only touches a throwaway process tree.
