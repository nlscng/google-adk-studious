# google-adk-studious

A learning and exploration project for the [Google Agent Development Kit
(ADK)](https://google.github.io/adk-docs/), built around a small robotics
simulation as a concrete playground.

## What this is

Two intertwined goals:

1. **Learn Google ADK** by using it, not just reading about it.
2. **Simulate a rover/UAV trash-pickup mission** (see
   [`docs/MISSION.md`](docs/MISSION.md)) and, somewhere along the way, find
   natural seams where an ADK-based agent makes the simulation smarter or
   more autonomous.

We don't yet know *when* or *how* agents will get plugged in — that's part
of the exploration. The simulation comes first; the agentic pieces get
introduced once the seams are obvious.

## How we work

This project follows the spirit of **spec-driven development**, with a
small three-doc hierarchy living in `docs/`:

1. [`docs/MISSION.md`](docs/MISSION.md) — **why**. The motivation and
   the scenario. Drives everything else.
2. [`docs/SPEC.md`](docs/SPEC.md) — **what**. Features, components,
   required behaviors. Derived from the mission.
3. [`docs/DESIGN.md`](docs/DESIGN.md) — **how**. Architecture, module
   boundaries, decisions, tradeoffs. Must satisfy the spec.

Rules of thumb:

- Write/update the doc *before* (or alongside) the code that implements
  it.
- A change at a higher level may require updates at lower levels;
  keep them reconciled.
- All changes — including doc changes — go through PRs so the reasoning
  is reviewable.

Start with [`docs/MISSION.md`](docs/MISSION.md) for the high-level "why".

## Stack

- Python ≥ 3.12 (managed with `uv`)
- `google-adk` for agent work
- `jupyter` for notebook-driven exploration
