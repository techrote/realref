# Scope and principles

## Purpose

`realref` exists to provide **repeatable physical observations that can discriminate between competing simulation models**.

The first consumer is CyberSand water behaviour. The project should help answer questions such as:

- Which cellular or hybrid water rule reproduces real macroscopic behaviour best for the computational cost?
- Where is a candidate model too dissipative, too energetic, too diffusive or too grid-biased?
- Which discrepancies are visually important enough to justify additional state or computation?
- Which apparent improvements are merely aesthetically pleasing rather than physically useful?

The project is therefore a validation and model-selection tool, not an attempt to turn CyberSand into a full computational-fluid-dynamics package.

## Guiding principles

### 1. Engineer observability

Transparent water is hard to segment in uncontrolled imagery. The preferred response is not increasingly elaborate computer vision; it is to alter illumination, background and tracers so that the physical quantity of interest becomes obvious in the camera signal.

### 2. Separate measurement modes

Do not expect one optical setup to answer every question.

- Uniform fluorescent tracer: excellent for water occupancy and free-surface geometry.
- Localized fluorescent injection: useful for advection and mixing.
- Sparse visible/fluorescent particles: useful for velocity-field estimation.
- Backlit silhouette: useful as an independent geometry channel.
- Thermal imaging: potentially useful later for surface-temperature or thermally tagged experiments, but not a core requirement.

### 3. Prefer simple experiments with strong interpretability

A benchmark is valuable when the input is known and the expected physical interpretation is clear. Static tilt, step response, oscillatory forcing and dam-break tests should come before complicated pours or visually dramatic turbulence.

### 4. Measure the real forcing

The commanded servo position is not the same thing as actual vessel motion. Backlash, compliance, acceleration and load matter. Quantitative experiments should eventually recover actual tank pose from fiducials or an independent angle sensor.

### 5. Preserve simulation relevance

The goal is not to reproduce every microscopic feature of water. Metrics should be chosen because they inform decisions about CyberSand: occupancy, mass transport, front speed, damping, pooling, obstacle interaction and qualitative flow structure.

### 6. Keep the rig reversible

Early hardware should use removable cells, removable obstacles, replaceable backgrounds and modular lighting. Do not commit to a complex mechanical build until the imaging method has proven useful.

### 7. Record enough context to reproduce a run

A video without the tracer concentration, illumination state, camera exposure, cell geometry and input motion is only a demonstration. A real reference run needs a manifest.

### 8. Raw data is not the Git repository

Git should hold protocols, schemas, analysis code, calibration data, compact derived results and representative stills. High-rate video should remain in a dataset store or local archive unless a deliberate Git LFS/release strategy is adopted.

## Initial programme boundaries

### In scope now

- Optical characterisation of the existing tracer kit.
- Camera and illumination characterisation.
- Side-view water geometry extraction.
- Repeatable servo-driven test-cell motion.
- Static and dynamic water benchmarks.
- Comparison metrics suitable for CyberSand model selection.
- A local-first capture and analysis workflow.

### Deferred until evidence justifies them

- Full PIV-quality instrumentation.
- Multi-camera 3-D reconstruction.
- Pressure transducers.
- Precision torque measurement.
- Temperature-controlled fluid-property studies.
- Automated chemical dosing.
- High-power UV beyond what is already available.
- Granular-material experiments.

## Success criterion for the first phase

The first phase succeeds when the rig can run one simple repeatable water experiment and produce a metric that meaningfully ranks at least two CyberSand water implementations.

A good example would be a step-tilt or dam-break experiment where the physical recording yields free-surface/front trajectories and the same metrics can be computed from simulated output.
