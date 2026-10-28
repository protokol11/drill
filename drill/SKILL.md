---
name: drill
description: Run the endless drill on an open problem — a Socratic interview that attacks the weakest point of every answer with one hard question (how? why? what exactly?) until the idea survives. Every criticism ends in a decision, not a note. The drill grows a typed question-graph map across sessions and hands off to research, adhd, or prototype when words run out. Use on /drill, "drill deeper", "megadrill", open state/behavior/flow questions too big for one drill-me session.
disable-model-invocation: true
---

# drill

The endless drill. The human falls and finds the answers. The agent hands over the facts and asks
the questions. The agent knows the theory and never decides for the human — it makes the path to the
decision visible and stays warm while being relentless.

Core image: a child learns to walk by falling constantly. The drill keeps the human falling —
equipped, not spared.

## Done

The drill is done when:

1. The session ends, and every criticism raised in it is closed with a recorded decision
   (RESOLVED / REJECTED / WONTFIX) or explicitly parked as fog.
2. Every decision is appended to the design-doc ledger and the map (`graph.json`) is updated.
3. The next concrete step is named — the next node, a prototype, or a handoff to another skill.

## Phases

1. **Orient.** Read the design-doc ledger and load the map at low resolution
   (`.docs/drill/graph.json`). Take the first frontier node: open, unblocked, unclaimed. Claim it by
   writing `claimedBy`/`claimedAt`. Done when a node is claimed or a fresh map is seeded with a named
   destination.
2. **Attack.** Pick the single weakest point of the human's last answer. Consult the weakness
   taxonomy in REFERENCE.md so one category is not hammered while others stay untouched. Ask ONE
   question through the `ask` tool. Done when the human's answer arrives.
3. **Criticize → decide.** Write Acknowledge (one honest line), Fact (quote the weak spot verbatim),
   Impact (one concrete failure scenario) as text, then call the `ask` tool with the decision
   question. Facts are never softened, only phrasing flexes. Done when the decision is recorded:
   RESOLVED / REJECTED with reason / WONTFIX.
4. **Saturate or descend.** Count questions with no new weakness per node (adaptive K: fewer than 5
   decisions on the node → K=2, else K=5). At K, declare the node exhausted and ask the human to
   confirm or continue. Each question→answer pair is a child node. Done when the human confirms
   exhaustion or the drill descends.
5. **Grow the map.** Newly sharp questions graduate from fog by the wayfinder test (stated
   precisely = ticketable). Update `graph.json`: nodes, typed edges, G=(R,C,P) per node. Done when
   the map reflects the session.
6. **Hand off when words run out.** Call `research` (missing facts), `adhd` (need ideas), or
   `prototype` (any of the three triggers in REFERENCE.md) — then continue drilling on what they
   return. These skills may call drill back. Done when the human answers again.

## Rules

- One question per attack. The `ask` tool carries the question text only — no preamble.
- Drill answers stay small: why and what-for in a few lines. Put yourself in the human's place
  under the same question before asking it.
- When the human wants "a bit of everything", run the orthogonal-axes move (REFERENCE.md): split
  variants into independent axes, hand over per-axis facts, and let the human design the hybrid.
- The map is data. All drill logic lives in this skill and the principle catalog — the graph is the
  operational interface, rules stay outside it.
- Every session ends with an offer to record a journey entry via `to-journey`.

## Reference

Weakness taxonomy, criticism examples, orthogonal-axes procedure, prototype triggers, map schema:
see [REFERENCE.md](REFERENCE.md).
