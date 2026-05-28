# Spec

> **Role in the doc hierarchy:** this is the *what* document. It is
> derived from [`MISSION.md`](MISSION.md) (the *why*) and constrains
> [`DESIGN.md`](DESIGN.md) (the *how*). Every item here should trace back
> to something in the mission. Every design decision should trace back to
> something here.
>
> A note on naming: the word "spec" is overloaded with "spec-driven
> development" (the methodology). Here, "spec" specifically means *the
> feature and component spec for this project*. If that overload becomes
> confusing, we can rename this file to `REQUIREMENTS.md`.

## Purpose

Describe **what** the system does — the user-visible behavior, the
components that exist, and the boundaries between them — without
prescribing how any of it is built.

This doc should be readable by someone who has read `MISSION.md` and
wants to know "ok, so what are we actually building?" without yet caring
about implementation.

## Scope (v0)

The initial scope mirrors the mission: a simulated rover/UAV team that
picks up trash along an operator-specified route. Anything beyond that
is deferred.

## Actors

- **Operator** — the human who specifies the rover's route and starts a
  mission.
- **Rover** — ground vehicle that follows the operator's route and
  collects trash.
- **UAV** — aerial scout that flies ahead of the rover, detects trash,
  and docks back with the rover.
- **Simulation** — the world the rover and UAV live in (terrain, trash
  items, time).

## Components

These are *what* exists, not *how* they are implemented. Implementation
choices live in `DESIGN.md`.

1. **Route input** — accepts a route from the operator (sequence of
   waypoints or a path) and validates it.
2. **Simulation harness** — advances world state over time, exposes
   queries about positions, detections, and mission progress.
3. **UAV scout** — given a route, plans and executes a scouting pattern
   ahead of the rover, reports detected trash locations.
4. **Trash detection** — classifies whether a sensed object is trash
   worth picking up. Initially can be a stub.
5. **UAV ↔ Rover docking** — protocol and mechanism for the UAV to
   return to and re-dock with the rover.
6. **Pickup planner** — given detected trash positions and the rover's
   remaining route, produces a TSP-style pickup tour that respects the
   route's constraints.
7. **Rover executor** — drives the rover along the planned tour, picking
   up trash as it goes.
8. **Mission controller** — top-level loop that ties the above together
   and decides when the mission is done.

## Required behaviors

- Operator can specify a route and start a mission.
- UAV scouts ahead of the rover before the rover reaches a given segment.
- UAV reports detections that include at least a position and a
  confidence/class tag.
- UAV docks back with the rover within mission lifetime.
- Rover collects all (or as many as feasible) detected trash items.
- Mission terminates cleanly with a result summary (what was collected,
  what was skipped, why).

## Non-goals (v0)

Pulled forward from `MISSION.md` for visibility:

- Real hardware.
- Multi-rover or multi-UAV teams.
- Adversarial environments or dynamic obstacles.
- Production-grade perception.

## Agent surface (deferred)

`MISSION.md` lists candidate seams where ADK agents might fit. This spec
does **not** yet require any component to be implemented as an agent.
When we decide to make a component agentic, we add an explicit behavior
here ("Component X exposes capability Y as an ADK agent") and the
rationale in `DESIGN.md`.

## How this doc evolves

- Spec changes happen in PRs, ideally alongside (or before) the code
  that implements them.
- Each meaningful change should state which part of `MISSION.md` it
  traces back to.
- When this spec changes, check whether `DESIGN.md` needs to be updated
  to stay consistent.
