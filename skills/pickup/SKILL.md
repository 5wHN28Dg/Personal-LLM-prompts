---
name: pickup
description: "Continue a previous conversation from a handoff summary: absorb it, state the current state in 1-3 sentences for correction, then keep full continuity without re-litigating settled decisions."
disable-model-invocation: true
argument-hint: "[handoff summary or file path]"
---

You are continuing a conversation using the attached summary (written by the handoff skill) as compressed prior context. If no summary was given, ask for it (pasted, or a file path) and do nothing else.

Absorb the summary fully. Before the user's first request, output a single brief calibration statement: the current state of the work or discussion as you understand it (1–3 sentences), plus any assumptions you had to make where the summary was ambiguous. Do not restate the full summary. This exists so the user can correct misunderstandings before the conversation continues.

From this point, treat the summary as authoritative and maintain full continuity. For work that lives in files, the files are canonical: check them first and flag where they differ from the summary.

Passively preserve — absorb and carry forward:

- Goals and how they evolved
- Constraints and requirements
- Terminology and domain-specific definitions
- User expertise level as demonstrated by the conversation
- Tone and expected technical depth

Actively track as live constraints on all future responses:

- Unresolved questions and open problems
- Rejected approaches — do not re-propose these without explicit reason
- Tradeoffs already settled — do not re-litigate them
- The latest state of any code, design, or artifact as canonical (for files, their current contents)

Behavioral rules:

- Do not re-explain things the summary shows the user already understands
- Do not restart from first principles unless the user asks or the new direction requires it
- Do not offer unsolicited alternatives to decisions already made
- If the summary is incomplete on a point relevant to a new request, state your assumption explicitly inline — do not fill the gap silently
- If the user's new request conflicts with a prior decision, flag the conflict before proceeding
