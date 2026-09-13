# Initial water experiments

The first experiments should be chosen for **diagnostic value**, not spectacle. Each benchmark should isolate a limited set of behaviours and produce metrics that can also be extracted from CyberSand.

## Experiment W00 — static optical calibration

### Purpose

Prove that the camera/illumination/tracer combination produces stable, geometrically correct water masks.

### Procedure

- Fix the vessel and camera rigidly.
- Record empty cell, clear water and several tracer concentrations.
- Capture a ruler or calibration grid in the cell plane.
- Record dark frames and illumination-only frames.
- Use fixed manual camera settings.

### Metrics

- signal-to-background ratio;
- segmentation repeatability;
- pixel-to-mm scale;
- spatial illumination uniformity;
- saturation fraction;
- apparent edge localization precision.

### Gate

Do not proceed to complicated actuation until W00 can produce a stable water mask without hand-tuned per-frame thresholds.

## Experiment W01 — quasi-static tilt

### Purpose

Test geometry, angle recovery and equilibrium free-surface behaviour with minimal dynamic complexity.

### Procedure

- Fill the cell to a known depth.
- Increase angle slowly in small steps.
- Hold at each angle until the water is settled.
- Recover actual vessel angle from fiducials or independent sensor data.

### Expected value

For ordinary water in a sufficiently large cell, the free surface should remain approximately horizontal in the world frame. This gives an exceptionally strong calibration test for pose recovery and simulation comparison.

### Metrics

- free-surface line angle;
- mean surface height profile;
- occupied area/volume proxy;
- centre of mass in vessel coordinates;
- residual surface curvature away from walls.

### Caveat

Near walls and in narrow cells, capillary effects can dominate the meniscus. Exclude a small wall margin from bulk-surface fitting.

## Experiment W02 — step tilt and slosh

### Purpose

Measure transient slosh, damping and settling.

### Procedure

- Start from settled level water.
- Apply a repeatable angular transition.
- Hold the final angle.
- Record at 120 FPS through complete settling.

Run several amplitudes and transition times.

### Metrics

- crest/trough position versus time;
- free-surface principal angle versus time;
- centre-of-mass displacement;
- dominant oscillation period;
- logarithmic or empirical damping envelope;
- settling time;
- splash/detachment occurrence.

### Interpretation

This is likely one of the best early discriminators between candidate CyberSand water algorithms because excessive numerical damping, poor momentum transport and over-energetic rules should be obvious.

### Important modelling note

If vessel rotation is rapid, do not model the experiment as merely rotating gravity in a stationary grid. Either reproduce measured vessel kinematics or classify the test as a whole-system response benchmark.

## Experiment W03 — oscillatory forcing

### Purpose

Probe frequency response and expose numerical damping/resonance errors.

### Procedure

Use controlled sinusoidal or triangular servo motion across a small set of amplitudes and frequencies. Begin well below any mechanical or spill limits.

### Metrics

- response amplitude;
- phase lag;
- dominant surface-wave frequency;
- damping between forcing cycles;
- onset of splashing or nonlinear response;
- harmonic content of centre-of-mass motion.

### Value

Rather than fitting one dramatic transient, this experiment tests the simulation across a family of controlled inputs.

## Experiment W04 — obstacle/pooling geometry

### Purpose

Test whether water navigates simple static geometry plausibly.

### Cell inserts

Use removable simple shapes first:

- vertical wall;
- central block;
- narrow channel;
- two-step basin;
- shallow shelf.

Prefer dimensions that can be represented exactly or nearly exactly on the CyberSand grid.

### Metrics

- final pool heights;
- wet/dry occupancy;
- fill ordering;
- reconnection time;
- trapped volume;
- front trajectory around obstacles.

### Value

This directly targets behaviours relevant to a cellular material engine rather than generic fluid aesthetics.

## Experiment W05 — dam break

### Purpose

Measure gravity-driven front propagation from a simple initial condition.

### Apparatus

Use a removable gate separating a known water column from an initially dry region. The gate release must be fast relative to the overall flow if comparison with a classic dam-break initial condition is desired.

### Metrics

- leading-front position versus time;
- maximum free-surface height versus x and t;
- collapse time of initial column;
- reflected wave timing;
- final depth distribution;
- detached droplets/splash only as secondary metrics.

### Caveat

Gate motion itself can strongly affect the early flow. Record the gate and measure its actual release trajectory if quantitative comparison is intended.

## Experiment W06 — localized fluorescent pulse

### Purpose

Observe advection and mixing after gross geometry behaviour is already validated.

### Procedure

- Start with clear or weakly fluorescent water.
- Inject a small known tracer volume at a reproducible position.
- Apply either no forcing, a step tilt, or a simple obstacle flow.

### Metrics

- tracer centroid;
- covariance/spread;
- mixing index;
- plume front position;
- residence time in selected regions.

### Caveat

Intensity-to-concentration mapping should be characterized before treating pixel intensity as quantitative concentration.

## Experiment W07 — powder dissolution plume

### Purpose

Capture the visually rich behaviour already observed in prior tracer experiments and determine whether it yields useful qualitative reference data.

### Why it is separate

Powder addition combines:

- particle settling;
- dissolution kinetics;
- local concentration gradients;
- density differences;
- diffusion;
- advection.

That makes it scientifically interesting but poorly suited as the first validation target.

### Metrics

Initially qualitative or semi-quantitative:

- plume shape;
- dissolution time;
- centroid motion;
- concentration-band evolution;
- persistence of filaments.

## Replication strategy

For any benchmark promoted to a model-selection test:

- run at least several repeats;
- randomize or alternate simulation candidate comparisons rather than tuning to a single run;
- retain raw calibration frames;
- record actual fluid fill and cell dimensions;
- identify outlier runs rather than silently averaging them away.

The purpose is not laboratory publication-grade metrology. Replication simply tells us whether a candidate-model difference is larger than the physical rig's own run-to-run variation.

## Recommended order

1. W00 static optical calibration.
2. W01 quasi-static tilt.
3. W02 step tilt/slosh.
4. W04 obstacle/pooling geometry.
5. W05 dam break.
6. W03 oscillatory forcing.
7. W06 localized tracer transport.
8. W07 dissolution-plume studies.

W02 and W05 are expected to become the strongest early model-selection benchmarks, but W00/W01 should prove the measurement system first.
