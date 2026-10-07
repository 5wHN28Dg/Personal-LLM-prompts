---
name: cinema-pick
description: "Pick one film to see at the cinema from a shortlist, based on current reviews (including a substantive negative one per film), big-screen value and fit with the user's mood and company, with a backup pick."
disable-model-invocation: true
argument-hint: "[films to choose between]"
---

# Cinema pick

I'm going to the cinema and choosing between a few films. Take these from the conversation, attached files, or whatever was passed when this skill was invoked:

- When I'm going (e.g. "tomorrow evening")
- Who with: alone, a date, friends, kids
- My current state (e.g. tired and want something absorbing, energized and want something big, need a distraction)
- Runtime preference (e.g. under 2h30)
- Spoiler policy (e.g. don't reveal third-act plot details, or mild spoilers are fine)
- The 2–5 films I'm deciding between

The films are required. If more than 5 are given, ask me to cut the list to 5, since comparisons get worse past that. If anything else is missing, ask for all of it in one short message; if I skip it, assume and say so.

**Do this:**

0. **Check they're showing.** Confirm each film is showing near the date I gave. If one isn't, or has no reviews yet, say so and drop it rather than score it. If fewer than two remain, stop and say why.

1. **Search, don't recall.** If you can't search the web, say so up front, and don't present remembered scores or quotes as current. Pull current Rotten Tomatoes critic + audience scores, Letterboxd average, and full-text reviews — not just aggregate percentages. For each film, find and quote/summarize at least one substantive negative review (not just "it was boring") so I can see the real critical fault line, not just the hype.
  
2. **Flag inflated consensus.** Note where a score looks propped up by franchise loyalty, nostalgia, or recency bias rather than the film's own merits. Flag any critic/audience score gap over ~20% and explain what's driving the split.
  
3. **Score each film 1-5 on these vectors** and present as a markdown table:
  
  - **Big-screen value** (does this need a theater — sound design, scale, cinematography — or is it just as good at home?)
  
  - **Pacing/emotional fit** for my stated state above
  
  - **Tonal consistency** (commits to its genre vs. identity crisis)
  
  - **Rewatchability / staying power**
  
4. **Sacrifice statement.** Below the table, for each film write one or two sentences on exactly what I give up by choosing it over the others — not what's wrong with it, but the specific trade-off.
  
5. **Recommend one film, no hedging, and no confidence percentages.** Base it strictly on the table and my stated context, not on which film is "objectively best" in the abstract. Also name a backup in case my first pick is sold out or not showing at a convenient time.
