# Personal LLM prompts

The prompts and system prompts I use, packaged as skills. I keep iterating on them.

Each one lives in `skills/<name>/SKILL.md`. In Claude Code they install as a plugin. Everywhere else, the body of each file is plain markdown you can paste into any LLM.

## Using them

**Claude Code:**

```
/plugin marketplace add 5wHN28Dg/Personal-LLM-prompts
/plugin install llm-prompts@personal-llm-prompts
```

Then call a skill with `/llm-prompts:<name>`, e.g. `/llm-prompts:cinema-pick`. You can pass inputs right after the name, attach files, or let the skill ask for what's missing. Most skills only run when you call them. Two, `translate` and `evidence-first-engineering`, can also load on their own when the task fits.

To use a single skill without the plugin, copy its folder into `~/.claude/skills/` (all projects) or `.claude/skills/` (one project) and call it as `/<name>`.

**Any other LLM:** open the skill's `SKILL.md`, copy everything below the second `---` line, paste it, and then give it your inputs. Each skill lists the inputs it needs.

**Web search:** `cinema-pick`, `movie-forecast`, `employer-due-diligence`, `cover-letter-research` and `company-intel` depend on current information, so use them where the model can search the web.

## General

- **`epistemic-standards`**: the system prompt I use with every LLM except coding agents. It consults rather than teaches: it reasons without flattery, says when it's unsure, and states the criteria behind any judgment so I can check the reasoning instead of trusting it. It works best as a system prompt or custom instructions. In Claude Code you can import it from a `CLAUDE.md` with `@path/to/skills/epistemic-standards/SKILL.md`, or invoke it to switch a session over.

- **`socratic-tutor`**: a Socratic tutor for coding agents. I don't use coding agents to write code for me. I use them as a thinking partner that pushes back, adapts to what I actually understand, and doesn't trade truth for comfort. By default it guides instead of answering; it gives a direct answer for plain lookups, boilerplate, code reviews, or when I say "just show me". TLDR: if you want a prompt that makes your coding agent do the coding for you, this isn't it. Don't use it, you'll hate it.

- **`handoff`** and **`pickup`**: carry a conversation into a new chat. `handoff` writes a state-transfer document (goals, constraints, decisions, rejected approaches, open problems, the latest state of the work); `pickup` takes that document in the new chat, tells you in 1–3 sentences what it understood so you can correct it, and carries on without re-arguing settled decisions.

- **`translate`**: translation that transfers meaning, effect, register and cultural weight rather than words, with extra rules for English ↔ Arabic (dialects, religious formulas, grammatical gender, root-based wordplay, legal text). It adds translator's notes only when it made a real judgment call. For long technical documents, put a terminology table first (`Terminology (use exactly):` followed by `term → translation` lines) to keep terms consistent.

- **`synthesize`**: give it several takes on one topic (answers from different models, articles) and it maps where they agree and disagree, classifies each disagreement as factual, definitional or values-based, keeps ideas only one source raised, and writes one synthesis that's more useful than any single take, without faking consensus.

- **`unslop`**: rewrites existing text to remove generic AI-writing patterns without flattening the author's voice. It targets causes (generic phrasing, flat emphasis, unfalsifiable words) rather than a list of banned words, and never invents detail to sound specific.

- **`evidence-first-engineering`**: for coding agents. Before adding a dependency, a framework or custom code, find out what the platform already provides, and add only what it doesn't, while keeping accessibility, security and measurement discipline. `SKILL.md` is the one-page rule set; the full reasoning is in two essays in its `reference/` folder (native platforms and the web), which the agent opens only when it needs them.

## Job applications

These work as a pipeline; each one's output is the next one's input.

1. **`employer-due-diligence`**: is this a safe, stable and honest place to work, and is this specific job posting real? Every conclusion is labeled by evidence strength. Notes:
   - Area 6 (relocation, sponsorship or remote-work risk) applies only when you describe your situation.
   - If the company is very small or very new, thin evidence is itself a finding; the skill says so rather than padding the report.
   - Re-run it before a final round or an offer, not just before applying: layoff or lawsuit news can surface in between.
2. **`master-cv`**: builds a complete, factual master CV from messy inputs (old resumes, notes), and lists every conflict, gap and inferred skill for you to confirm.
3. **`tailor-resume`**: checks a job description against your master CV. If a hard requirement is unmet, it stops and says NO FIT. If you fit, it maps the job's requirements to your evidence and writes a tailored resume with nothing invented.
4. **`cover-letter-research`**: finds the specific, sourced, recent facts about the company that a "why this company, right now" paragraph needs. No mission-statement filler.
5. **`cover-letter`**: writes the cover letter and/or the application email and subject line from the job description, `tailor-resume`'s strategy map and the tailored resume.
6. **`company-intel`**: a fuller company briefing for interview prep: what they do, size and ownership, recent news, culture evidence, the team or hiring manager, and why they're probably hiring now. Every claim is sourced and dated.
7. **`interview-prep`**: answers to your interview questions in your own voice, grounded only in your real experience and consistent with the resume you submitted, with salary-negotiation turns, delivery notes and likely follow-up questions. Send all your questions and documents at once so it builds the whole picture before answering. In other LLMs, Part 1 can go in the system prompt field and Part 2's inputs in your first message.

Also for job hunting:

- **`linkedin-review`**: evaluates your LinkedIn profile against your goal and target audience, both on whether the right people can find it and on how they'll judge it, with the top 3 fixes written out.
- **`linkedin-reader`**: role-plays the average, silent LinkedIn reader and gives a gut reaction to a post or headline: would they stop scrolling, read it, engage?

## Everything else

- **`cinema-pick`**: picks one film to see at the cinema from your shortlist, based on your mood and who you're with, with a backup. Why it's built this way:
  - **Mood and company** come before genre on purpose: a model can reason about "tired, alone, want absorbing-not-devastating" far more usefully than "I like thrillers".
  - **The negative review requirement** is the single highest-leverage line. Without it, the model defaults to whatever has the shiniest aggregate score.
  - **No confidence percentage:** those numbers look rigorous but aren't grounded in anything real for an LLM. The sacrifice statement (what you give up with each pick) surfaces the uncertainty honestly.

  > You could make a version for streaming at home, where the big-screen-value criterion doesn't apply.

- **`movie-forecast`**: predicts whether an upcoming film will be good, critically, as entertainment and commercially, using only evidence dated before release: a reference class, weighted signals, discounted noise, and what would prove the prediction wrong.

- **`training-program`**: builds a training program as a feedback-driven system rather than a fixed template: structure, progression, an objective rule for adjusting it, deload triggers, and what to track. On later passes, give it the previous program and your training log and it revises only what the data calls into question. Version history is in its `CHANGELOG.md`.
