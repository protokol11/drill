---
name: drill-me
description: Run a critical planning drill on a focused decision — one question at a time with a recommended answer and a mandatory critique, escalating to diverge + prototype for open-ended state/behavior questions, or to full ADHD ideation on "go deeper". Use on /drill-me, "be critical", "one question at a time", brainstorm/ideate intents, or open-ended design, naming, and API/SDK surface questions.
---

# drill-me

A critical planning drill. The default mode is one focused question at a time. For open-ended,
high-stakes, state/behavior/flow questions, the drill switches into diverge + prototype mode. The
agent reads the session and picks the mode. The human does not pick from a menu.

For the endless version — an interview that attacks every answer until the idea survives, across
sessions — use `drill`.

## Done

The drill is done when:

1. The mode was chosen from the session signals, and the mode's procedure ran to its end.
2. Every question got a human answer — the agent never answered for the human.
3. Every criticism raised got challenged and either confirmed or dropped with a reason.
4. Crystallized pointers (terms, hard-to-reverse decisions) were offered for capture.
5. A clear next concrete step was identified, and the drill state was recorded.

## Modes

1. **Converge** (default). Small answer space, a canonical answer, or closed phrasing ("quick",
   "standard", "textbook"). Procedure: see [REFERENCE.md](REFERENCE.md). Done when the decision is
   explicit and the next step is concrete.
2. **Diverge + Prototype.** All four checks pass: open-ended, high-stakes, state/behavior/flow,
   human available for HITL. Three frames × four ideas, clusters, traps, top 3, one survivor into a
   throwaway prototype. Done when the survivor is chosen or explicitly rejected.
3. **Full ADHD.** The human says "go deeper", "ADHD mode", or "explore frames", or the question is
   clearly high-stakes and wide. Done when the `/adhd` skill returns with a chosen direction.

## Rules

- One question at a time. Use the `ask` tool for options. Render no markdown option lists in
- Be critical but constructive: surface trade-offs, edge cases, contradictions. The goal is
  clarity, not winning the argument.
- If a fact lives in the codebase or the web, look it up instead of asking the human.
- The decisions are the human's. The agent makes them explicit and stress-tests them.
- Do not create files, maps, or tickets mid-drill unless the human confirms.

## Capture

When a term stabilizes or a hard-to-reverse decision crystallizes, offer the capture pointer
(`to-context`, `to-adr`) before continuing. When the session pauses or ends, record the drill state
through the mental-record flow.
