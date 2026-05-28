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

This project follows the spirit of **spec-driven development**:

- Write the spec (the "what" and "why") before the code.
- Keep specs in `docs/` alongside the code they describe.
- Treat specs as living documents: update them as understanding evolves,
  and let code changes follow from spec changes rather than the other way
  around.
- Use PRs for all changes (including spec changes) so the reasoning is
  reviewable.

Start with [`docs/MISSION.md`](docs/MISSION.md) for the high-level "why".

## Stack

- Python ≥ 3.12 (managed with `uv`)
- `google-adk` for agent work
- `jupyter` for notebook-driven exploration
