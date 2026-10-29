# drill

drill is a skill pack for coding agents that turns vague ideas into recorded decisions, one hard question at a time.

![Banner: the word "drill" in monospace type, surrounded by cartoon construction workers drilling, hammering, and cutting on a scaffolding site.](assets/drill.gif)

**Credits**
- `drill-me` ← [grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) crossed with [wayfinder](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder), both by Matt Pocock
- `adhd` skill ← [github.com/uditakhourii/adhd](https://github.com/uditakhourii/adhd)

Verify the install worked:

```sh
test -f ~/.agents/skills/drill/SKILL.md && test -f ~/.agents/skills/drill-me/SKILL.md && echo "drill installed"
```

## Contents

- [Why](#why)
- [How it works](#how-it-works)
- [Install](#install)
- [Usage](#usage)
- [Graceful degradation](#graceful-degradation)
- [Contributing](#contributing)
- [License](#license)

## Why

Agents say "done" as a claim, not a fact. Plans get nods, not stress tests. What a person needs out of a planning session is a **decision**, not another page of notes — and the path to it kept on record.

drill flips the roles: the human decides, the agent asks. It was built by crossing three ingredients:

- **grill-me's form** — one hard question at a time, each with a recommended answer, until the decision is explicit.
- **wayfinder's map** — a typed question-graph (`.docs/drill/graph.json`) that any session can claim, grow, and resume.
- **a ban on the obvious** — the first two obvious answers to every question are rejected outright, so the discussion can't stall on hand-waving.

Scope: decision-making and idea stress-testing for coding agents. Non-scope: writing or reviewing code, and ideation beyond the drill — those hand off to `adhd` / `research` / `prototype`.

Known limit: saturation thresholds (`K=2` / `K=5`) are first guesses — tune them on live drills.

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

Prerequisites: **None.** No dependencies. Any coding agent that loads `SKILL.md` skills works — the skills live in the standard `~/.agents/skills/` directory (pi, Claude Code, and others).

1. Copy `drill/` and `drill-me/` into `~/.agents/skills/`.
2. Run the check from the top of this file — it should print `drill installed`.

Handoff skills are not bundled: `adhd` is a third-party ideation skill ([optional install](https://github.com/uditakhourii/adhd)); `research` and `prototype` come from your own setup.

## Usage

Load the endless drill — in pi: `/skill:drill` (force-load; the phrases "drill deeper" / "megadrill" only work as routing context, not as invocation). In other agents: load `drill/SKILL.md` and say what you want drilled. For a single decision, use `drill-me`.

A quick taste of a drill:

```
agent: What exactly does "fast" mean for this endpoint?
 you: Under 200 ms p95.
agent: You said "under 200 ms" — on what data volume? At 10× rows the join
       alone blows past it. RESOLVED, REJECTED, or WONTFIX?
 you: REJECTED — benchmark first, then set the number.
```

Criticism ends in a decision: `drill` appends RESOLVED / REJECTED / WONTFIX to the ledger, never a polite note; `drill-me` confirms or drops every criticism with a reason.

## Graceful degradation

Every feature works at the tier you can support:

| Feature | Needs | Without it |
|---|---|---|
| `drill-me` Converge (core) | nothing extra | — |
| Diverge + Prototype | `prototype` skill from your setup | diverge runs; no throwaway prototype |
| Full ADHD | `adhd` skill ([optional install](https://github.com/uditakhourii/adhd)) | "go deeper" unavailable |
| Endless drill map | `.docs/drill/graph.json` (created on first run) | no cross-session memory |

## Contributing

File issues in this repository. There is no test suite — skills are validated by running them against a live planning session; development and contributions follow the MIT license.

## License

MIT — see [LICENSE](LICENSE).
