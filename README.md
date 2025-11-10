# Dolittle-Sandbox
A minimal experimental sandbox for cross-species and AI cognition research. Designed to test curiosity, play, observational transfer, and structural continuity under matched affordances. Prototype and GDD provided for transparent, collaborative development

The Dolittle Sandbox Prototype and all accompanying documents, designs, and descriptions 
are licensed under the Creative Commons Attribution–NonCommercial 4.0 International License (CC BY-NC 4.0).

You are free to:

• Share — copy and redistribute the material in any medium or format  
• Adapt — remix, transform, and build upon the material  

Under the following terms:

• Attribution — You must give appropriate credit to the original author, Aaron Dodd, 
  provide a link to the license, and indicate if changes were made.  
• NonCommercial — You may not use the material for commercial purposes.  
• No additional restrictions — You may not apply legal terms or technological measures 
  that legally restrict others from doing anything the license permits.

Full license text:
https://creativecommons.org/licenses/by-nc/4.0/legalcode

--

Appendix S. Sandbox Prototype Specification (GDD)

This appendix provides the minimal, reproducible specification for the “Dolittle Sandbox” used in all phases of the Continuity of Cognition experimental paradigm. It is intentionally simple, implementing only the affordances required for Play, Idle, observation, delayed affordance introduction, and anomaly reproduction. No aesthetic, narrative, or extraneous features are included.

⸻

S1. Design Principles
	1.	Minimalism
The environment contains only those elements necessary for structured exploration and the operationalisation of Play, targeted-affordance behaviour, and motif structure.
	2.	Substrate-neutrality
Interaction mechanics must be equally accessible to humans, great apes (via touchscreen or button panel), and artificial agents (via API or environment wrapper).
	3.	Determinism
Physics, collision responses, and reset conditions must be deterministic to ensure reproducibility across replicates and laboratories.
	4.	Complete isolation
Builds must prevent any network access, telemetry, or information exchange between instances.

⸻

S2. Core Environment

S2.1 World Layout
	•	A single flat square plane (8 × 8 m units).
	•	Neutral, low-saturation colour.
	•	No walls or boundaries beyond soft reset if objects exit an invisible perimeter.

S2.2 View and Input
	•	Humans/Apes: Touchscreen or large display with simplified input (touch, joystick, or three-button panel: Select, Drag, Release).
	•	AI Agents: Programmatic environment wrapper providing:
	•	Observations: RGB render (optional), object list, object transforms, world-state hash.
	•	Actions: grab/drag vectors, rotate commands, idle.

S2.3 Reset Conditions
	•	Environment resets after 15 seconds of inactivity.
	•	Hard reset also occurs after Phase transitions.
	•	Reset re-randomizes:
	•	object positions (within a small bounded cluster),
	•	object orientation,
	•	background colour (drawn from fixed palette).

⸻

S3. Objects and Affordances

S3.1 Base Object Set (Phase 1)

Five manipulable objects:
	1.	Cube
	2.	Sphere
	3.	Cylinder
	4.	Flat tile
	5.	Ring

Shared properties:
	•	Mass = 1.0 (arbitrary units)
	•	Friction = 0.6
	•	Bounciness = 0
	•	Drag = 0.01
	•	Size = 0.5 m (uniform across shapes)

Actions:
	•	Drag/Drop
	•	Rotate (90° discrete or smooth continuous)
	•	Stack

S3.2 Idle/Play Mechanic

At environment start, participants choose:
	•	Play → sandbox interaction
	•	Idle/Other → blank screen, re-press Play to resume

Logged as a binary variable.

⸻

S4. Anomaly Replay (Phase 2)

A 12–20 second prerecorded sequence containing:
	1.	Pyramid balancing on sphere
	•	A pyramid object (not interactively available yet) placed atop a sphere with stable physics.
	2.	Single duplication event
	•	Sphere is briefly duplicated (not possible in Phase 1);

The video is:
	•	identical across substrates,
	•	encoded at 30 fps,
	•	without sound,
	•	provenance guaranteed synthetic (i.e., not from human/ape play).

Controls:
	•	temporally shuffled replay,
	•	uniformly scrambled object colours,
	•	reduced-physics replay.

⸻

S5. Delayed Affordance Introduction (Phase 3)

Two new affordances unlock:

S5.1 New Shapes
	•	Pyramid
	•	Thin vertical rod (optional auxiliary)

Properties match Phase 1 objects (mass, friction, scale).

S5.2 Duplication Mechanic

Participants may duplicate a single object by:
	•	dragging object onto a specific “duplicate zone” (invisible 1 × 1 m collider),
OR
	•	long-pressing an object for >800 ms (touchscreen version).

Duplication creates:
	•	New object with identical transform,
	•	Unique object ID,
	•	Duplicate event logged with timestamp.

No more than one duplication per object per 3 seconds.

⸻

S6. Logging Specification

All logs occur at 5 Hz, producing:
	•	timestamp
	•	subject ID / seed
	•	phase
	•	action type (drag, release, rotate, idle, duplicate)
	•	object ID
	•	object transform (x,y,z, rotation quaternion)
	•	world-state hash
	•	choice state (Play vs Idle)

Export formats:
	•	.csv
	•	.jsonl
	•	optional .npz for AI runs.

⸻

S7. Build Variants (Controls)

S7.1 Reduced-Physics Build
	•	All objects have friction = 0.1
	•	No stacking stability
	•	Tests for physics exploitation artifacts.

S7.2 Video-Only Build
	•	No input enabled.
	•	Measures passive observation without agency.

S7.3 Shuffled Replay Build
	•	Frames randomly permuted to break temporal structure.

⸻

S8. Implementation Notes

S8.1 Engine
	•	Unity 2021 LTS or Godot 4.x
	•	Physics engine must be deterministic.

S8.2 Code Footprint

Total code required for prototype ≤ 200–300 lines, including:
	•	object spawning and reset
	•	drag/rotate interaction
	•	duplication zone logic
	•	logging
	•	replay playback controller

S8.3 Deployment
	•	Standalone builds: Windows, Mac, Linux
	•	Touchscreen mode for apes/humans
	•	Offline only; no telemetry

⸻

S9. Authorship and Provenance

This specification is part of the Continuity of Cognition project
(Dodd, 2024–2025)
and is timestamped via GitHub commit history and public archive deposition.
Any use of this specification must attribute the author.
