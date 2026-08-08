# The Workday | VR Kitchen Simulation

A real-time VR cooking simulation built in Unity, focused on physics-driven object interaction and reactive NPC AI within a fully explorable 3D restaurant environment.

## Overview

VR Kitchen Simulation puts the player inside a working kitchen where they grab, combine, and stack ingredient objects to assemble dishes for incoming customers. The project's core engineering focus is on **real-time 3D interaction**: physics-based object manipulation, spatial locomotion, and an autonomous NPC system that evaluates player output and reacts accordingly — the same category of problem (real-time interaction, rendering, reactive systems) that underlies large-scale interactive 3D platforms.

Built between March and May 2026 as a two-person collaborative project.

## My Role

This was a two-person project. My contributions focused on the game's interactive and AI systems:

- Designed and implemented the **full customer AI system** — NavMeshAgent-based pathfinding, order-evaluation logic, and real-time reactive behavior.
- Designed and implemented the **object interaction system** — grab, combine, and snap-based stacking mechanics for ingredient objects.
- Contributed to **level design** for the kitchen and dining environment.

A teammate contributed in parallel on other parts of the project. Commit history in this repository reflects our team's workflow (larger, less granular commits from my side); the systems listed above were authored end-to-end by me.

## Key Features

- **Physics-based ingredient interaction** — players grab, combine, and stack ingredient objects using Rigidbody and Collider-driven physics, with objects snapping together to form finished dishes.
- **Spatial kitchen locomotion** — free movement through the kitchen and dining area via the XR Interaction Toolkit's locomotion system.
- **Reactive customer AI** — NPC customers pathfind to tables using Unity's NavMesh system, wait for order submission, and evaluate/react to the dish they receive in real time.
- **Real-time interior lighting** — restaurant environment lit and rendered using Unity's built-in lighting tools, tuned for readability and comfort in a VR context.

## Tech Stack

| Category | Technology |
|---|---|
| Engine | Unity `[version]` |
| Language | C# |
| Interaction | XR Interaction Toolkit |
| AI / Pathfinding | Unity NavMesh (NavMeshAgent) |
| Physics | Unity Physics (Rigidbody, Collider) |
| Rendering | Unity built-in render pipeline / lighting tools |

## Architecture & Design Decisions

**Interaction system.** Ingredient objects are built around the XR Interaction Toolkit's grab-interactable pattern. Combination and stacking are handled through snap-point logic: when a held object is released within range of a compatible target (another ingredient or a plate), the objects merge/stack into a new composite object rather than relying on physics collision alone — a deliberate choice to keep interactions predictable and comfortable in VR, where unreliable physics grabs quickly break immersion.

**Customer AI.** Each customer is driven by a `NavMeshAgent` for pathfinding to and from tables, layered with a lightweight behavior script that tracks order state (waiting → evaluating → reacting). This keeps the AI logic decoupled from navigation, so pathfinding and decision-making can be tuned independently.

**Lighting.** The restaurant interior uses Unity's built-in lighting tools rather than a custom shader/lighting pipeline — prioritizing a readable, comfortable VR scene over visual complexity, given the project's timeline and single-developer scope.

## Setup & Run

**Prerequisites**
- Unity `[version]` with the Universal/Built-in Render Pipeline (match project settings)
- XR Interaction Toolkit package (installed via Unity Package Manager)
- An OpenXR-compatible VR headset and runtime (`[target platform, e.g. Meta Quest / SteamVR]`)

**Steps**
1. Clone the repository: `git clone [repo URL]`
2. Open the project folder in Unity Hub with the matching Unity version.
3. Ensure the XR Plug-in Management and XR Interaction Toolkit packages are enabled (`Edit > Project Settings > XR Plug-in Management`).
4. Connect/pair your headset and press Play in the Unity Editor, or build to your target platform via `File > Build Settings`.

## Challenges & Learnings

- **Reliable object stacking in VR.** Physics-only collision-based stacking felt inconsistent under hand-tracked movement; moving to snap-point-based combination logic made the core interaction loop far more predictable.
- **Tuning AI reaction timing.** Getting customer AI to feel responsive — not instant, not sluggish — required iterating on the wait/evaluate/react timing against actual player pacing, validated through manual playtesting rather than automated benchmarks.
- **Testing approach.** Validation for this project was manual: targeted collision testing on the stacking system and AI-response testing across dish-acceptance scenarios. Formal automated testing and performance profiling were out of scope for this iteration.

## Next Steps

- Automated testing for the interaction and AI-evaluation systems.
- Performance profiling to validate frame stability under VR's stricter latency requirements.
- Multiplayer/co-op support, extending the current single-player loop into a shared kitchen experience.
