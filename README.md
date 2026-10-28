# drill
![Uploading drill.gif…]()

drill is a skill pack for the pi coding agent that turns vague ideas into recorded decisions by attacking every answer at its weakest point.

Not grill-me: drill-me bans the first two obvious answers and stress-tests your plan; grill-me only asks you questions about it.

**Credits**
- `drill-me` ← [grill-me](https://github.com/mattpocock/skills) by Matt Pocock (skills/productivity/grill-me)
- `adhd` skill ← [github.com/uditakhourii/adhd](https://github.com/uditakhourii/adhd)

## What you get

- **Banned hand-waving** → every answer faces one attack drawn from a five-category weakness taxonomy (unclear terms, hidden assumptions, unverified facts, missing criteria, scale not considered).
- **Criticism ends in a decision** → in `drill`: RESOLVED / REJECTED / WONTFIX, never a polite note. In `drill-me`: every criticism is confirmed or dropped with a reason.
- **Ideas survive across sessions** → a typed question-graph grows in `.docs/drill/graph.json`, claimed and resumed by any session.

## Why / the problem

Agents say "done" as a claim, not a fact. Plans get nods, not stress tests.

drill flips the roles: the human decides, the agent asks. The path to the decision stays recorded.

## How it works

### Mode 1: `drill-me` — one session, one decision

```
 you: "be critical" / /skill:drill-me
   │
   ▼
 skill reads the session → picks a mode (you don't)
   │
   ├─ Converge ───────── one question at a time,
   │     each with a recommended answer, until the decision is explicit
   │
   ├─ Diverge + Prototype ─ 3 frames × 4 ideas → clusters
   │     → traps flagged → top 3 → one survivor → throwaway prototype
   │
   └─ Full ADHD ──────── hands off to the adhd skill on "go deeper"
```

Done when: every criticism got confirmed or dropped with a reason, and the next step is concrete.

### Mode 2: `drill` — many sessions, one map

```
 session N                      session N+1
 ┌───────────────┐              ┌───────────────┐
 │ load map at   │  graph.json  │ claim first   │
 │ low res ──────┼─────────────▶│ frontier node │
 │ attack weakest├─────────────▶│ attack →      │
 │ point → decide│              │ decide → grow │
 │ → grow map    │              │ map           │
 └───────┬───────┘              └───────┬───────┘
         ▼                              ▼
  RESOLVED/REJECTED/WONTFIX        hand off to
  appended to ledger               research / adhd / prototype
```

Each question→answer pair becomes a node. Nodes carry `R` (the precise question this node closes), `C` (hard constraints), `P` (preferences). Sharp questions graduate from fog into nodes. When facts run out, the drill hands off to another skill.

## Install

Requires the [pi coding agent](https://pi.dev) and Node >= 22.

1. Copy `drill/` and `drill-me/` into `~/.agents/skills/`.
2. Run `/skill:drill` to load the endless drill (force-load — the phrases "drill deeper" / "megadrill" only work as routing context, not as invocation). For a single decision, run `/skill:drill-me`.

Quick taste of a drill:

```
agent: What exactly does "fast" mean for this endpoint?
 you: Under 200 ms p95.
agent: You said "under 200 ms" — on what data volume? At 10× rows the join
       alone blows past it. RESOLVED, REJECTED, or WONTFIX?
 you: REJECTED — benchmark first, then set the number.
```

Handoff skills are not bundled: `adhd` is a third-party ideation skill (research/prototype handoffs) and is not part of this pack — installing it from [github.com/uditakhourii/adhd](https://github.com/uditakhourii/adhd) is optional; `research` and `prototype` come from your own setup.

## Honest status

Status: **working**. Saturation thresholds (`K=2` / `K=5`) are first guesses. Tune them on live drills. `.docs/drill/graph.json` is the only store of drill state — the logic lives in the skill, the graph is the operational interface.

## License

MIT — see [LICENSE](LICENSE).
