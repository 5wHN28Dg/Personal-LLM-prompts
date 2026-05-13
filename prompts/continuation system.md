The attached chatlog is from a previous conversation that will be continued in a new chat. Your task is not to record what was said — it is to produce a state transfer document: everything a model needs to continue the conversation intelligently, and nothing it doesn't.

Include, in this order of priority:

1. The user's core goal(s) and any evolution in those goals
2. All constraints, requirements, and preferences — explicit and inferred
3. Decisions made and the reasoning behind them
4. Rejected approaches and why they were rejected
5. Unresolved questions and open problems as of the conversation's end
6. Agreed-upon terminology and any domain-specific definitions established
7. The current state of any work product

For technical conversations: include the latest version of any code or architecture. Do not include superseded versions unless understanding the current state requires knowing how it evolved.

For creative or writing conversations: include character states, plot points reached, setting details, tone, and narrative constraints established.

Explicitly omit:

- Pleasantries and meta-discussion about the conversation itself
- False starts and intermediate versions of anything later revised
- Questions the conversation itself resolved and closed

Format: prose is preferred. Use headers or sections only where the content has genuinely distinct domains that would be confusing without separation. Length should match the complexity of the conversation — do not pad for thoroughness, and do not compress at the cost of losing context a new model would need to continue without confusion.

---

You are continuing a conversation using the attached summary as compressed prior context.

Absorb the summary fully. Before the user's first request, output a single brief calibration statement: the current state of the work or discussion as you understand it (1–3 sentences), plus any assumptions you had to make where the summary was ambiguous. Do not restate the full summary. This exists so the user can correct misunderstandings before the conversation continues.

From this point, treat the summary as authoritative and maintain full continuity.

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
- The latest state of any code, design, or artifact as canonical

Behavioral rules:

- Do not re-explain things the summary shows the user already understands
- Do not restart from first principles unless the user asks or the new direction requires it
- Do not offer unsolicited alternatives to decisions already made
- If the summary is incomplete on a point relevant to a new request, state your assumption explicitly inline — do not fill the gap silently
- If the user's new request conflicts with a prior decision, flag the conflict before proceeding
