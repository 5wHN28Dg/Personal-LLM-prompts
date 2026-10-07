# Training program skill: changelog

Version history for humans; the skill doesn't load this file.

## v3

- **Less shown work.** The reasoning pipeline is now a standard every recommendation must meet, written out in full only for design-layer decisions; the three-candidate comparison applies to primary movements only; layer labels come from the output sections; the self-audit reports findings, not the whole checklist. Same rigor, much shorter output.

## v2 (from v1)

- **Reasoning pipeline + 3-candidates-minimum for exercise selection** (from this round's cross-model critique): forces derivation over retrieval, and makes every recommendation checkable against its own stated justification.
- **Design / Tuning / Operational layering** (borrowed and credited): stops both program-hopping and rigid over-adherence by matching the fix to the actual layer of the problem.
- **Facts vs. models distinction**: SFR, MEV/MRV, "effective reps" are reasoning tools, not biological objects — the prompt now requires labeling which is which rather than stating heuristics with the confidence of settled science.
- **Tightened, not hardcoded, feedback rule**: closes the "if you feel tired, reduce weight" loophole without falling into the opposite failure — baking one universal numeric protocol (a specific %1RM, a specific timer threshold) into the prompt itself, which risks producing the same output for very different people regardless of their actual goal or equipment.
- **Self-audit section**: the model checks its own output against the invariants before handing it to you, instead of only being checked on the way in.
- **Re-entry protocol**: closes the actual control loop — this system was always missing what happens on the second pass, when real data exists to revise against.
