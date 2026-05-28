# Design

> **Role in the doc hierarchy:** this is the *how* document. It must
> satisfy [`SPEC.md`](SPEC.md) (the *what*), which is derived from
> [`MISSION.md`](MISSION.md) (the *why*). Every non-trivial design
> decision here should point back to the spec item it serves.

## Purpose

Describe **how** the system is built: architecture, module boundaries,
data flow, key algorithms, and — most importantly — the decisions and
tradeoffs that got us there.

If `SPEC.md` says "the UAV scouts ahead and reports detections," this
doc answers "ok, but how? In what process? Over what interface? With
what data shape? Why that choice and not the alternatives?"

## Status

Empty by design. We have a mission and a spec; we have not yet made
implementation decisions. This file exists so that the first design
decision has an obvious home and a consistent shape to follow.

## Suggested sections (fill in as decisions are made)

### Architecture overview

A short narrative + (optional) diagram of how the major components in
`SPEC.md` fit together at runtime. What is one process vs. many? What
is synchronous vs. event-driven? Where does the simulation clock live?

### Module layout

Where each spec component lives in the codebase, and the public surface
each module exposes.

### Data shapes

The handful of core types that flow between components (e.g., `Route`,
`Detection`, `PickupPlan`, `MissionResult`). Defined once here, used
everywhere.

### Algorithms

Notable algorithmic choices and their rationale (e.g., which TSP
heuristic for the pickup planner, which scouting pattern for the UAV).

### Agent integration

When and where we introduce ADK agents:

- Which spec component is being made agentic.
- What capability the agent exposes (tools, prompts, I/O contract).
- Why an agent is the right tool here vs. plain code.
- How it is tested and what its failure mode looks like.

### Decision log

Append-only list of meaningful decisions. Suggested entry shape:

```
### YYYY-MM-DD — <short title>

**Context:** what problem / spec item prompted this.
**Decision:** what we chose.
**Alternatives considered:** what else we looked at.
**Tradeoffs:** what we gave up.
**Trace:** which SPEC.md item this serves.
```

Keeping decisions inline (rather than scattered ADR files) for now —
the project is small, and one file is easier to read end-to-end. We can
graduate to a `docs/adr/` directory if this section gets unwieldy.

## How this doc evolves

- Design changes go through PRs.
- A design PR should reference the SPEC item(s) it serves. If no SPEC
  item covers it, the SPEC needs to change first (or in the same PR).
- When the SPEC changes, sweep this doc for items that no longer make
  sense and update or remove them.
