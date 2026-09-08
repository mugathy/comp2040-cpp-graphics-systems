# comp2040-cpp-graphics-systems
C++/SFML projects covering 2D graphics, recursive algorithms, dynamic programming, and design patterns (Factory, Composite)

Graphics & Systems Projects (C++ / SFML)

A collection of C++ projects built for a systems/graphics programming course, covering 2D rendering, recursive algorithms, dynamic programming, design patterns, and text-based log parsing. Each project includes unit tests (Boost.Test) and a Makefile build.

Projects
AniPlayer — JSON-Driven Keyframe Animation Player

A playback engine that loads a scene graph from JSON and animates components (circles, rectangles, images, text, and nested groups) with linear interpolation between keyframes.

Factory pattern (Component::fromJson) builds the correct component subclass from a JSON shape field with no type-switch elsewhere in the codebase
Composite pattern lets a CompositeComponent hold child components and propagate sf::RenderStates transforms down the tree, so nested objects inherit parent rotation/scale/position without manual coordinate math
Playback controls: pause/resume, restart, optional background music via sf::Music
Stack: C++17, SFML 3, nlohmann/json, Boost.Test
DNA Alignment — Edit Distance via Dynamic Programming

Computes the minimum edit distance between two strings (mismatch cost 1, gap cost 2) using a 2D DP table, then traces back through the table to reconstruct a full character-by-character alignment.

Standard bottom-up DP with a 3-way min helper
Backtracking reconstructs the actual alignment, not just the distance
Tested against E. coli genome fragments up to 2,500 characters; identified and documented an out-of-memory failure mode on the largest test inputs (50k/100k) caused by the O(n·m) table size, a real constraint of the dense-matrix approach
Stack: C++17, SFML (timing), Boost.Test
Sokoban — Puzzle Game with Undo/Redo

A playable Sokoban implementation: level loading from text files, box-pushing physics, win detection, and full undo/redo via saved game-state snapshots.

Custom TileType enum handles compound tile states (e.g., a box sitting on a storage goal) without a multi-layer rendering system
Movement logic validates walls and box-pushing before mutating state
Undo/redo implemented with two stacks of captured game states
Stack: C++17, SFML 3, Boost.Test
SpriteBuilder — Procedural Character Generator

Randomly assembles layered character sprites (body, head, accessories) from tile sheets using a seeded Mersenne Twister for reproducible output.

Built test-first: interface decisions (e.g., out-of-range handling) were locked in via Boost unit tests before implementation
shared_ptr-backed texture views avoid redundant texture copies across layers
CLI flags for seed, scale, and input file; supports re-roll and PNG export
Stack: C++17, SFML 3, Boost.Test
Pythagoras Tree — Recursive Fractal Renderer

Renders a Pythagorean tree fractal to an arbitrary recursion depth, with branch color interpolating from green at the trunk to pink at the tips.

Uses SFML's transform stack (rotate/scale/translate composition) instead of manually computing absolute coordinates at each recursion level
Auto-scales the window to fit the full tree at any depth
Stack: C++17, SFML 3
RandWriter — Order-k Markov Text Generator

Generates text that statistically mimics an input corpus using an order-k Markov model over character sequences.

Custom weighted-random selection (kRand) over a frequency map, using std::for_each with a lambda predicate
Demonstrates how model order affects output coherence (order 2 ≈ noise, order 7–8 on English text produces plausible words and phrases)
Stack: C++17, Boost.Test
Kronos Log Parser — Boot Sequence Analysis

Parses system logs from a Kronos time-clock device, identifies boot start/complete event pairs via regex, computes boot duration, and flags incomplete boots.

Two compiled regex patterns model boot state as a minimal (start, complete) pair sequence; any unmatched start is reported as incomplete
Timestamps parsed and diffed with Python's datetime
Stack: Python

Each project directory contains its own Makefile (make to build, make test where applicable, make lint for style checks) and a short breakdown of design decisions in-code.
