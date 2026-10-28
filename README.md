# drill

![Banner: the word "drill" in monospace type, surrounded by cartoon construction workers drilling, hammering, and cutting on a scaffolding site.](assets/drill.gif)

drill is a skill pack for coding agents that turns vague ideas into recorded decisions, one hard question at a time.

Not grill-me: drill-me bans the first two obvious answers and stress-tests your plan; grill-me only asks you questions about it.

Try it: copy `drill/` and `drill-me/` into `~/.agents/skills/`, then load the drill skill. Any agent that reads `SKILL.md` works — pi, Claude Code, and others.

**Credits**
- `drill-me` ← [grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) crossed with [wayfinder](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder), both by Matt Pocock
- `adhd` skill ← [github.com/uditakhourii/adhd](https://github.com/uditakhourii/adhd)

## What you get

- **Banned hand-waving** → every answer faces one attack drawn from a five-category weakness taxonomy (unclear terms, hidden assumptions, unverified facts, missing criteria, scale not considered).
- **Criticism ends in a decision** → in `drill`: RESOLVED / REJECTED / WONTFIX, never a polite note. In `drill-me`: every criticism is confirmed or dropped with a reason.
- **Ideas survive across sessions** → a typed question-graph grows in `.docs/drill/graph.json`, claimed and resumed by any session.

## Why / the problem

Agents say "done" as a claim, not a fact. Plans get nods, not stress tests.

Agents have never fallen, so they have never learned to walk — and a drill can't teach them. What it can do is hand you the raw material: facts, side-paths, scope. The structure feeds you facts; you create the idea.

drill flips the roles: the human decides, the agent asks. The path to the decision stays recorded.

## How it works

### Mode 1: `drill-me` — one session, one decision

```
 you: "be critical" / load drill-me
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

No dependencies. Any coding agent that loads `SKILL.md` skills works — the skills live in the standard `~/.agents/skills/` directory.

1. Copy `drill/` and `drill-me/` into `~/.agents/skills/`.
2. Load the endless drill — in pi: `/skill:drill` (force-load; the phrases "drill deeper" / "megadrill" only work as routing context, not as invocation). In other agents: load `drill/SKILL.md` and say what you want drilled. For a single decision, use `drill-me`.

Quick taste of a drill:

```
agent: What exactly does "fast" mean for this endpoint?
 you: Under 200 ms p95.
agent: You said "under 200 ms" — on what data volume? At 10× rows the join
       alone blows past it. RESOLVED, REJECTED, or WONTFIX?
 you: REJECTED — benchmark first, then set the number.
```

Handoff skills are not bundled: `adhd` is a third-party ideation skill (research/prototype handoffs) and is not part of this pack — installing it from [github.com/uditakhourii/adhd](https://github.com/uditakhourii/adhd) is optional; `research` and `prototype` come from your own setup.

Graceful degradation — every feature works at the tier you can support:

| Feature | Needs | Without it |
|---|---|---|
| `drill-me` Converge (core) | nothing extra | — |
| Diverge + Prototype | `prototype` skill from your setup | diverge runs; no throwaway prototype |
| Full ADHD | `adhd` skill ([optional install](https://github.com/uditakhourii/adhd)) | "go deeper" unavailable |
| Endless drill map | `.docs/drill/graph.json` (created on first run) | no cross-session memory |

## Honest status

Status: **working**. Saturation thresholds (`K=2` / `K=5`) are first guesses. Tune them on live drills. `.docs/drill/graph.json` is the only store of drill state — the logic lives in the skill, the graph is the operational interface.

## Contributing

File issues in this repository. Development and contributions follow the MIT license.

## License

MIT — see [LICENSE](LICENSE).
