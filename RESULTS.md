# Results and interpretation

## Native measurements

| Repeat | Frame wall P95 | GPU span P95 | Valid samples |
|---|---:|---:|---:|
| 1 | 16.053 ms | 5.859 ms | 300/300 |
| 2 | 15.954 ms | 5.791 ms | 300/300 |
| 3 | 15.932 ms | 5.793 ms | 300/300 |

900 measured frames, all valid GPU timestamps; 60 warm-up frames per repeat. Platform: RTX 3070 Ti Laptop, 1280×720 display, 640×360 volume integration, 64³ simulation. These are repeats of one scene, not independent generalization scenes.

Wall timing includes drawing, GPU-query waiting and Present. Outer message handling, JSON record append and final log writing are excluded. GPU span includes the simulation, lighting cache, optional local indirect approximation, integration, full-resolution surfaces/composite and UI. GPU span is not display latency. Frozen R1 results do not certify a later changed executable.

The full 24-second event clock is accelerated across the benchmark frames while simulation advances about six seconds. The video instead presents twelve seconds of normal simulated time, exported offline at 15 fps. It is a visual demonstration, not performance evidence or a browser-based simulation.

## Numerical checks

- Uniform-medium analytic transmittance max absolute difference: 7.02471188e-06 (threshold 1e-4).
- View refinement relative RGB L1: 0.000229508574; shadow refinement: 0.0001132055019 (threshold 1% for this fixed-state screening).
- Native/Unity initial density: 1,048,576 finite FP32 values, bitwise equal. This does not establish evolved-state or radiance parity.
- Programmatic pause/resume/reset, light change and inside-medium camera checks passed. Physical keyboard/mouse acceptance remains pending.

The figures were checked against existing private records before preparation. This public package provides aggregate evidence, not raw volumes, complete experiment reproduction or undisclosed algorithms.

## Current scope

Single scattering and a fixed lighting cache; optional indirect light is a visual diffusion approximation. Pressure projection is not tightly converged (about 5.89% divergence reduction in the diagnostic state); the moving boundary treatment is simplified. Cache spatial convergence, physical multiple scattering, independent Unity GPU timing and real Unity mesh-depth integration remain unverified. No matched-cost superiority over state-of-the-art methods is claimed.

High-level framework reference: [GPU Gems 3, Chapter 30](https://developer.nvidia.com/gpugems/gpugems3/part-v-physics-simulation/chapter-30-real-time-simulation-and-rendering-3d-fluids). This is an independent engineering project using established ideas, not a complete reproduction of the chapter.
