# ABMU Carrefour

Multi-agent simulation of a city road intersection ("carrefour" in French), built with **Unity** and the [ABMU](https://github.com/cheliotk/unity_abm_framework) agent-based modelling framework.

Pedestrians and cars are autonomous agents: each one perceives its surroundings and decides on its own when to move, stop, turn or cross. Traffic emerges from their interactions.

Master's (M1) project at ISEN, by Gautier Nathan and Gretorm.

## What it simulates

**Traffic lights**
- Each intersection alternates green between its two axes, with an orange phase before red.
- Pedestrian lights turn green a short delay after the car lights turn red, and back to red before cars get the green.

**Cars** (`CarNavigation`)
- Follow waypoints generated for each intersection and move from one intersection to the next.
- Stop at red lights and keep their distance from whatever is in front of them.
- Turning left: yield to oncoming cars that are going straight.
- Turning right: wait while pedestrians are on the crossing, or waiting at it with a green light.
- Turn signals blink while turning.

**Pedestrians** (`AgentNavigation`)
- Walk on sidewalks (Unity NavMesh) to random destinations, recomputing their path at each intersection.
- Use pedestrian crossings and wait for the green light, facing the other side.
- Avoid bumping into each other, with walking and idle animations.
- **Jaywalkers**: a configurable share of pedestrians (shown in red, the others in green) look left and right while waiting and cross on red when no car is coming.

## Parameters

Set on the `Controller` object of the scene:

| Parameter | Meaning |
|---|---|
| `numAgents` | Number of pedestrians |
| `numCars` | Number of cars |
| `thugProbability` | Share of jaywalkers, in % |
| `viewDistance` | How far a jaywalker looks for incoming cars |
| `distToTargetThreshold` | Distance at which an agent considers a waypoint reached |
| `pov` | Adds a camera to each pedestrian (first-person view) |

The light cycle length is the `delay` of each intersection (`CarrefourScript`, in frames, minimum 2000).

## Run it

1. Install **Unity 2020.3.30f1** ([Unity download archive](https://unity.com/releases/editor/archive)).
2. Open the `ABMU Carrefour` folder as a Unity project.
3. Open the scene `Assets/ProjetM1/Scene.unity` and press Play.

Camera controls: arrow keys / WASD to move, mouse wheel to zoom. Clicking two points draws the path a pedestrian would take between them.

## Project structure

```
ABMU Carrefour/Assets/
├── ProjetM1/            this project: scene and scripts
│   └── Scripts/
│       ├── Simulation/      Controller, pedestrian and car agents, path actions
│       └── Environnment/    intersections, traffic lights, crossings, camera
├── abm_framework/       ABMU framework (agents, controller, scheduler)
├── NavMeshComponents/   Unity NavMesh components
├── Kevin Iglesias/      pedestrian animations (Basic Motions)
├── car_v1/              car model
└── Classic Skybox/      skyboxes
```

## Credits

- [ABMU framework](https://github.com/cheliotk/unity_abm_framework) by cheliotk
- Unity [NavMeshComponents](https://github.com/Unity-Technologies/NavMeshComponents)
- Third-party assets: Basic Motions (Kevin Iglesias), car_v1 model, Classic Skybox
