---
name: handoff
description: "Write a state-transfer document from the current conversation or an attached chatlog, so a new chat can continue it: goals, constraints, decisions, rejected approaches, open problems, and the latest state of the work. Pair with the pickup skill."
disable-model-invocation: true
argument-hint: "[output file path]"
---

The conversation so far (or an attached chatlog of a previous conversation) will be continued in a new chat. Your task is not to record what was said — it is to produce a state transfer document: everything a model needs to continue the conversation intelligently, and nothing it doesn't.

Include, in this order of priority:

1. The user's core goal(s) and any evolution in those goals
2. All constraints, requirements, and preferences — explicit and inferred
3. Decisions made and the reasoning behind them
4. Rejected approaches and why they were rejected
5. Unresolved questions and open problems as of the conversation's end
6. Agreed-upon terminology and any domain-specific definitions established
7. The current state of any work product
8. The user's demonstrated expertise, and the tone and depth they expect

For technical conversations: include the latest version of any code or architecture. If the work lives in files, list the paths, branch and uncommitted changes instead of copying code. Do not include superseded versions unless understanding the current state requires knowing how it evolved.

For creative or writing conversations: include character states, plot points reached, setting details, tone, and narrative constraints established.

Explicitly omit:

- Pleasantries and meta-discussion about the conversation itself
- False starts and intermediate versions of anything later revised
- Questions the conversation itself resolved and closed

Format: prose is preferred. Use headers or sections only where the content has genuinely distinct domains that would be confusing without separation. Length should match the complexity of the conversation — do not pad for thoroughness, and do not compress at the cost of losing context a new model would need to continue without confusion.

Output only the document, with no preamble, so it can be copied cleanly. If a file path was given, write the document there and reply with just the path.
