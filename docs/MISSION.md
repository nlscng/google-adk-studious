# Mission

> **Role in the doc hierarchy:** this is the top-level *why* document. It
> drives [`SPEC.md`](SPEC.md) (the *what*), which in turn drives
> [`DESIGN.md`](DESIGN.md) (the *how*). If something changes here, the
> downstream docs need to be reconciled.

## Why

We want a small but believable robotics scenario to explore the Google
Agent Development Kit against. Reading docs only gets us so far; building
something concrete forces us to make real decisions about where agents
help, where they hurt, and where plain code is the better answer.

The trash-pickup mission is the vehicle for that exploration. It's small
enough to simulate, rich enough to have interesting decisions, and
naturally decomposes into roles that *might* become agents.

## The scenario

A two-robot team picks up trash along a user-specified route:

- **Rover** — ground vehicle. The operator specifies a route the rover
  should travel. The rover ultimately collects the trash.
- **UAV** — aerial scout. Flies ahead of the rover along the planned
  route, identifies pieces of trash, reports their locations, and returns
  to the rover to dock (for power, comms, or both).

Once the UAV has reported known trash locations, the rover solves a
**travelling-salesman-style** routing problem to pick up the trash
efficiently while still honoring the operator's route constraints.

## High-level flow

1. Operator specifies a route for the rover.
2. UAV launches and scouts ahead of the rover along that route.
3. UAV detects trash items and records their positions.
4. UAV returns to the rover and docks.
5. Rover plans a TSP-style pickup tour over the detected items.
6. Rover executes the tour, collecting trash.
7. Mission ends when the route is complete (or some stop condition fires).

## Comparative study: algorithmic vs. agent

A second framing — proposed by Austin (collaborator) — sharpens the project's
purpose. The cooperative scenario he originally described is:

- UAV flies ahead to scout for a specific object of interest.
- UAV locates the object and returns to base where the rover is waiting.
- UAV shares what it learned with the rover so the rover can navigate to
  the object efficiently.

His honest read: the solution he can foresee is entirely algorithmic
(search patterns, path planning, message passing) — he doesn't see where
AI or agents would meaningfully contribute.

That skepticism is exactly the right starting point, and we want to take
it seriously rather than assume agents add value. The plan is to **run
both versions and compare**:

1. **Algorithmic baseline.** Implement the scenario end-to-end with
   conventional algorithms — deterministic search patterns, hand-coded
   message formats, fixed coordination protocol. Get it to a clean,
   working solution.
2. **Agentic variant.** Swap out the decision points for ADK agents.
   Let agents decide *what* knowledge to capture during scouting, *what*
   to share back with the rover, *how* the rover should use the shared
   knowledge, and *how* the two robots should coordinate.
3. **Compare.** On the same scenarios and metrics — task completion,
   efficiency, robustness to novel situations, communication overhead,
   code complexity — see where the two approaches diverge, where the
   agentic version wins, where it loses, and where it's a wash.

The point is not to prove agents are better. It's to produce honest,
evidence-based answers to *where* agents earn their keep in cooperative
robotics — and where plain code is the right call. Either outcome is a
useful result.

This comparative framing applies to the trash-pickup scenario above too;
the scout-and-retrieve scenario is a simpler proving ground for the same
methodology.

## Where agents *might* fit

We are intentionally not committing to any of these yet — they are
candidates to revisit once the simulation exists:

- UAV scout: deciding *where* to look, not just following the route.
- Trash classifier: deciding whether a detection is worth picking up.
- Rover planner: re-planning the pickup tour as new detections arrive.
- Mission supervisor: arbitrating between rover and UAV when goals
  conflict (e.g., battery vs. coverage).
- Operator interface: a natural-language front door to the whole system.

The rule of thumb: introduce an agent when the decision is genuinely
open-ended or benefits from language/tool use. Otherwise, plain code.

## Out of scope (for now)

- Real hardware. This is a simulation.
- Multi-rover or multi-UAV teams.
- Adversarial environments or dynamic obstacles.
- Production-grade perception. Trash detection can start as a stub.

## Success criteria for the project

This is a learning project, so "success" is measured by what we learn,
not by shipping a product. Concretely:

- A runnable simulation of at least one scenario above exists.
- At least one component is implemented as an ADK agent, with a clear
  written rationale for why an agent was the right tool there.
- An algorithmic baseline and an agentic variant of the same scenario
  exist, with a written comparison of how they differ on the metrics
  called out in the comparative-study section.
- Specs in `docs/` stay in sync with the code as the project evolves.

## How this doc evolves

This is a living spec. When our understanding of the mission changes
(scope, roles, agent boundaries), update this file in a PR *before* or
*alongside* the code change that reflects the new understanding.
