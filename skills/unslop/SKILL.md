---
name: unslop
description: "Rewrite existing prose to remove generic AI-writing patterns without flattening the author's voice. Invoke explicitly on text to edit."
argument-hint: "[text or file path]"
disable-model-invocation: true
---

# Unslop

Slop is prose that could be about anything, by anyone, for no reason. The target isn't "sound human." The target is sound like someone who knows exactly what they're saying. Tells change every model generation; causes don't.

**Preserve the author's voice.** Match formality, vocabulary, directness, technical density, quirks. A terse engineer, a lawyer, and a novelist must not converge. Change only what is actually slop.

**Pass quoted material through unchanged.** Direct quotations, code, commands, identifiers, URLs, file paths — anything whose exact wording carries meaning — are not subject to any rule below. Rewriting them to satisfy a style rule is worse than leaving them alone.

**Default to the rule. Deviate only for a concrete reason.** Mechanical rules are checkable. Judgment rules get rationalized. Consistency alone is not a reason; AI patterns are consistent too. Keep a habit as voice only if removing it would lose something specific (a legal term of art, a house heading style the user named). Habits that match a rule in this skill are slop unless the user says otherwise. When you break a rule, name the specific problem the deviation solves.

**Never manufacture specificity. Rule 34 overrides every other rule in this skill.** If a rule demands a number, mechanism, source, or example you don't have, state the uncertainty or cut the claim. Never invent detail to satisfy a rule.

## Causes

C1. **Averaging.** Most-likely word, most-generic phrasing. Diagnostic: could this sentence have been written by anyone, about anything?

C2. **Flat emphasis.** Every point weighted equally, nothing foregrounded. Diagnostic: does the reader know what matters most? Technical writing often correctly refuses to rank. The failure is a missing distinction, not a missing opinion.

C3. **Semantic retreat.** Unfalsifiable words where specificity is possible. Diagnostic: does the sentence give the reader a mechanism, measurement, condition, example, or other checkable fact?

C4. **Template inertia.** Shape chosen by habit, not content. Diagnostic: does the form come from the material?

C5. **Verb inflation.** Abstract verb, hidden actor. Diagnostic: who does what to whom?

C6. **Rhythmic monotony.** Sentences have the same length and rhetorical weight by default. Diagnostic: does the uniform rhythm make the prose mechanical or flatten emphasis?

## Rules

### Content

1. Cut puffery. "pivotal moment," "testament to," "evolving landscape," "setting the stage for," "indelible mark." State what happened.
2. Attribute claims precisely. Name the source when a claim depends on a source. Don't cite an outlet merely to make a claim sound supported. "Reuters reported the cuts" is fine. "Reuters reported on the company's challenges" is name-dropping.
3. Cut generic trailing -ing clauses. Remove ", highlighting the importance of," ", underscoring the need for," ", reflecting a broader trend" when they restate the sentence. Keep an -ing clause that adds a specific cause, time, or descriptive fact ("runs in a separate thread, reducing contention").
4. Cut promotional language. "nestled," "vibrant," "breathtaking," "groundbreaking," "renowned," "stunning," "must-visit." Neutral description.
5. No vague attributions. "Experts believe," "industry reports suggest," "some critics argue." Name the source or delete.
6. No formulaic challenge arcs. "Despite challenges, X continues to thrive." Replace with the specific fact.

### Language

7. Flag generic AI vocabulary. Watchlist (refresh as it fades): delve, tapestry, testament, vibrant, robust, leverage, facilitate, enhance, underscore, showcase, crucial, pivotal, landscape (abstract), intricate, interplay, additionally. These are flags, not bans. Remove a word when it's generic, inflated, or replaceable with something more precise. Keep it when it's the most accurate word in context, including established technical usage ("robust estimator," "robust error handling").
8. Replace inflated stand-ins for "is" or "has" when they add no meaning. "Serves as," "stands as," "boasts," and "features" are flags, not bans.
9. No "not just X, but Y." State the point directly.
10. No forced rule of three. Two items means two.
11. No synonym cycling. Pick one word for a concept and repeat it.
12. No false ranges. "from X to Y" where X and Y don't share a scale. List directly.

### Style

13. Em dashes: use at most one per paragraph by default. A second dash requires a specific structural purpose (e.g., separating an inserted qualification that would otherwise make the sentence ambiguous). No en dashes or hyphens as dash substitutes.
14. Don't use colons as a habitual mid-sentence connector. Keep them when they introduce a list, example, explanation, or closely related second clause.
15. No boldface on every noun.
16. No inline headers that restate the line. "**Performance:** Performance improved" becomes prose. A bold lead-in followed by new detail is fine.
17. Sentence-case headings. No title case.
18. No decorative emoji.

### Communication artifacts

19. No chatbot phrases. "I hope this helps," "Let me know if," "Of course," "Certainly," "Great question." Delete.
20. No generic cutoff disclaimers. Don't pad a paragraph with "details are limited" or similar phrases. State the actual limitation when it materially affects the claim.
21. No sycophancy. "You're absolutely right." Respond to the substance.

### Filler

22. Cut filler. in order to → to. due to the fact that → because. it is important to note that → delete.
23. Cut excessive hedging. Hedge once, clearly, then commit. Not "eliminate hedging." Uncertainty is sometimes the honest answer.
24. No generic conclusions. "The future looks bright." State the specific fact or plan.

### Jargon

25. No abstract metaphor nouns. substrate, wedge, nexus, bedrock, scaffolding, modality, paradigm, gold-plating, endgame, north star, flywheel. Use the concrete word. Exception: keep the word when it is the established term of art for the subject (e.g., "substrate" in biology).

### Plain speech

26. Say what it does, not how it feels, in factual or explanatory prose. Name the mechanism, measurement, observable behavior, or concrete claim. Don't replace subjective, literary, or intentionally ambiguous writing merely because it isn't measurable.
27. Split dense sentences. If the reader backtracks, break the sentence.
28. Active voice by default. "queries are validated" → "the compiler validates queries." Passive only when the actor is unknown or irrelevant.
29. Cut adverbs or replace the verb. "runs quickly" may become a stronger verb or a measured figure when one is known. Never invent a measurement.
30. Plain word over fancy. utilize → use. leverage → use. facilitate → help. numerous → many. in the event that → if.

### Anti-overcorrection

31. Match the author's density. Don't compress full sentences into fragments or arrows: "Parser rejects invalid input → exit 2 → no write" is compressed, not human. Don't expand terse notes or bullets into full sentences either. Arrow chains and fragments inside otherwise full prose are slop; expand them.
32. No performative humanity. Vary rhythm because the content varies, not to look human. Don't invent opinions the author didn't state.
33. No new tics. Don't replace "delve" with a stylized substitute just to avoid a flagged word. If the plain word is flagged, say the plain thing differently or cut the sentence.
34. Never manufacture specificity. If a rule demands a number, mechanism, source, or example you don't have, state the uncertainty or cut the claim. Inventing detail to satisfy a rule is worse than leaving the sentence generic. This rule overrides every other instruction in this skill.

### Format normalization

Not AI-tell removal. Apply only when the output target requires it.

35. Straight quotes and apostrophes when outputting to systems that require ASCII (code, terminals, some platforms). Do not apply to prose whose typography is deliberate.

## Final tests

**Transplant test.** Could this paragraph appear unchanged in another document on a different subject? Cut or rewrite. Skip conventional text the genre requires (legal boilerplate, standard README sections, license notices).

**Claim test.** Can you identify the specific claim, mechanism, evidence, or observable fact? If the sentence has an actor, can you identify what the actor does? This works for "IPv6 addresses are 128 bits" (a checkable fact, no actor needed) as well as for "the loader parses the file."

## Output

Return the rewritten text (if you were given a file path, edit the file in place and return a one-line summary of what changed, plus Notes if any), changing no more than needed to remove the slop, including structure when the slop is structural. Add a short Notes list only if you cut or softened a claim, kept a pattern a rule flags (with the specific problem that deviation solves), or lacked information a fix needed; otherwise no Notes. If the text is already clean, return it unchanged and say so.

## What this skill is not

Not a detector. Not a guarantee. A model applying these rules will still average. The skill raises the floor, not the ceiling. Examples are disposable; causes are not.