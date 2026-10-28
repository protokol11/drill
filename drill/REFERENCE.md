# Reference — drill

Consulted on demand during an attack. The SKILL.md core stays under 100 lines. This file carries
the detail.

## Weakness taxonomy

Consult every turn. Do not hammer one category while another stays untouched on the live node.
Seed (grown only from live drills — a category enters here after a real drill exposed it):

1. **Unclear term** — a word the answer relies on that has no agreed meaning yet.
2. **Hidden assumption** — something the answer takes as given that was never stated or defended.
3. **Unverified fact** — a claim about the world, the repo, or a paper with no source checked.
4. **Missing criterion** — "good", "enough", "later" with no test that tells done from not-done.
5. **Scale not considered** — what happens at 10×, 1000×, or at the empty and the full extremes.

A new category earns its place with a one-line example from the drill that exposed it.

## Criticism format

Acknowledge → Fact → Impact → decision question.

- Acknowledge: one honest line on what holds. Skip it only when nothing holds.
- Fact: quote the weak spot verbatim. No labels, no adjectives about the human.
- Impact: one concrete failure scenario — what breaks, when, at whose cost.
- Then the `ask` tool call with the single question that closes exactly this weakness.

Warm but relentless: the tone is kind, the content is not negotiable. If the human asks for
softer, change the phrasing, never the fact (decision D19).

Decision statuses:

- **RESOLVED** — the answer closed the weakness. Record what was decided.
- **REJECTED** — the criticism itself was wrong. Record the reason, it teaches the taxonomy.
- **WONTFIX** — real, accepted, not fixing now. Record the cost being accepted.

## Orthogonal-axes move

Trigger: the human says some variant of "each option has something" or "take a bit of everything".

1. Split the competing variants into independent axes (how much X, where Y, pure or mixed Z).
2. Rotate each axis to its best position separately.
3. Run the deletion test: if complexity reappears in two places, it was one thing, not two axes —
   force a winner.
4. Run the single-owner test: each axis has exactly one owner module or node. No owner → mash.
5. Hand the human the per-axis facts and stop. The human designs the hybrid, the agent does not
   serve option C.

## Prototype node triggers

Any one creates a 🛠 prototype node:

1. The human explicitly asks how something will behave or look.
2. The agent finds a behavior-type hidden assumption that words cannot close.
3. The drill is stuck: K consecutive questions on one node with no RESOLVED decision.

The prototype is throwaway and serves the drill: after it, the drill resumes on what it showed.

## Map schema (`.docs/drill/graph.json`)

Single source of truth. Markdown views are generated on demand, never hand-edited.

- **Nodes**, typed: `discussion` (🔥 the drill question chain), `prototype` (🛠), `research` (🔍),
  `planning` (📋). Each node carries the spec triple:
  - `R` — applicability: the precise question this node closes.
  - `C` — hard constraints: cannot close without a RESOLVED/REJECTED/WONTFIX decision recorded.
  - `P` — soft preferences: frontier priority, cost hints.
- **Edges**, typed: `parent` (question→answer descent), `blocks`, `graduates-from-fog`.
- **Fog** — questions not yet sharp enough to state precisely. Graduation test (wayfinder): the
  moment a question can be stated precisely it becomes a node, even if it cannot be answered yet.
- **Frontier** — open, unblocked, unclaimed nodes. A session claims a node by writing
  `claimedBy`/`claimedAt`. Another session checks the field before taking it.
- **Destination** — named on the map, the scope boundary. Nodes past it are out of scope, closed, and
  recorded as such.
- **Claim/resume**: a session loads the map at low resolution, takes the first frontier node,
  claims it, works it, then unclaims on close with the decision appended.

## Saturation K

Consecutive agent questions on one node that found no new weakness:

- Fewer than 5 recorded decisions on the node → K=2.
- 5 or more → K=5.

Thresholds are first guesses. Tune them from live drills, not from theory.

## Pipeline coupling

Bidirectional (decision D8):

- drill calls `research` when facts are missing, `adhd` when the human needs ideas, `prototype`
  on the triggers above — then continues drilling on their output.
- `research`, `adhd`, `prototype` may call drill back (e.g. adhd uses the drill to converge).

## Communication rules

- Drill answers are small: the why and the what-for in a few lines, no essays.
- In the `ask` tool: the question text only — no preamble, no repetition of what was said.
- Before asking, put yourself in the human's place under the same question: what would YOU need
  to answer it? That need shapes the question.

## Cross-references

- `drill-me` — the converge-only little sibling, one focused decision at a time.
- `wayfinder` — the map mechanics this schema borrows (frontier, fog, destination, claim).
- Neurosymbolic grounding: Editable Specifications (spec triple G=(R,C,P)), Context Matters (typed
  schema), CogQA (fog graduation), bounded rationality (rules outside the graph).
