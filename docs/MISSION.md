# Mission

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

- A runnable simulation of the scenario above exists.
- At least one component is implemented as an ADK agent, with a clear
  written rationale for why an agent was the right tool there.
- Specs in `docs/` stay in sync with the code as the project evolves.

## How this doc evolves

This is a living spec. When our understanding of the mission changes
(scope, roles, agent boundaries), update this file in a PR *before* or
*alongside* the code change that reflects the new understanding.
