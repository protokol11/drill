# Reference — drill-me

Consulted on demand. The converge procedure and mode details live here so SKILL.md stays small.

## Mode selection

Read the session for the signals, then pick one:

- Converge signals: closed phrasing, a canonical answer exists, low cost of being wrong, the human
  said "drill-me" / "be critical" / "one question at a time" without asking for ideas.
- Diverge + Prototype signals: all four checks — open-ended, high-stakes, state/behavior/flow,
  human available. Prior-art first: run `research` with `mode=prior-art` before the first question.
- Full ADHD signals: "go deeper", "ADHD mode", "explore frames", or a high-stakes wide problem where
  the cheap answer is dangerous. Run `research` with `mode=prior-art` first, then call `/adhd` with
  the problem statement, the prior-art form, and the context.

## Converge procedure

1. **Scope lock.** State the single decision this drill resolves and its sources (files, PRDs, ADRs,
   research). Done when the decision is named in one line.
2. **Ask one question** through the `ask` tool. Include a recommended answer with a one-line
   reason. The option text carries the question only — no preamble. Done when the human answers.
3. **Stop.** Wait for the answer. Never answer for the human.
4. **Be critical.** Challenge the answer: trade-offs, edge cases, contradictions. If the answer is
   vague, ask a clarifying question with a concrete scenario.
5. **Capture pointer.** If a term or hard-to-reverse decision crystallized, offer `to-context` or
   `to-adr`. Do not create files mid-drill.
6. **Next or close.** If the decision is not clear, ask the next one-question drill. If it is clear,
   state the final decision and the next concrete step.

## Diverge + Prototype outline

- Pick 3 frames matched to the problem (minimal viable, remove the load-bearing assumption,
  inversion, regulator, speedrunner, $0 budget, competitor, 10-year-old).
- Generate 4 ideas per frame. The first two obvious answers are banned. One idea = one phrase.
- Cluster the 12 ideas into 3–5 groups by underlying angle. Label each cluster by angle.
- Flag traps: `TRAP: <one-line reason>` on attractive ideas hiding hidden costs.
- Pick top 3 by novelty, viability, fit. Mark the non-obvious-but-viable pick with `★`.
- For each top-3 idea: how it works, load-bearing risk, first concrete step, child ideas.
- Present, recommend one, let the human pick via `ask`. The survivor goes to `/prototype`
  with the question it must answer, the project context, and the path.

## Ask tool format

The tool carries the question and the options. Each option = one branch with a short description.
The recommended option says so with a one-line reason. Render no markdown lists in chat.

## Working agreements

- Use Russian for explanations and English for code terms, paths, and templates when the project
  convention asks for it.
- Related skills: `drill` (endless drill), `pathfinder` (pure one-question scoping), `research`
  (prior-art), `adhd` (full divergent ideation), `prototype` (throwaway validation), `to-adr`,
  `to-context`, `wayfinder` (huge decision spaces), `legs-off`, `mental-record`.
