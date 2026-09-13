# Roadmap

## Phase A — inventory and recovery

Goal: turn the remembered hardware/material set into a documented, reproducible inventory.

Tasks:

- identify primary camera, sensor, lens and installed optical window/filter;
- identify FLIR model;
- identify servo and its electrical/mechanical specifications;
- identify convenient microcontroller and power arrangement;
- photograph/record tracer labels and recover SDS/product information;
- recover any previous fluorescent-tracer photos/videos;
- identify candidate flat-sided cells or containers;
- record available optical filters, diffusers and mounting hardware.

Exit criterion:

- enough information exists to run a safe optical screening session without guessing critical hardware or chemical details.

## Phase B — optical/tracer bench screening

Goal: determine which existing tracer/light combinations actually work best with the assembled camera.

Tasks:

- verify stable 1080p/120 FPS capture;
- disable automatic camera controls;
- capture dark/empty/clear-water references;
- screen all six tracers against 365, 385, 395, 410, 420 and 450 nm excitation;
- test several relative concentrations for promising pairs;
- score signal, background, headroom, staining and stability;
- decide whether an emission filter is needed;
- preserve representative frames and measurements.

Deliverable:

- `TRACER_SCREENING` results table plus recommended geometry tracer and optional scalar-transport tracer.

Exit criterion:

- one optical mode produces a robust water/air segmentation signal with fixed camera settings.

## Phase C — static reference cell

Goal: prove quantitative image extraction before adding actuation.

Tasks:

- choose a flat-sided cell;
- add fiducials and calibration scale;
- build fixed lighting/background geometry;
- implement capture manifest;
- implement background/flat-field correction;
- extract occupancy masks and free-surface contours;
- run W00 static calibration;
- run manually positioned W01 tilt tests if convenient.

Exit criterion:

- repeat captures produce stable geometry metrics in physical units or normalized vessel coordinates.

## Phase D — deterministic servo rig

Goal: make forcing repeatable and logged.

Tasks:

- build conservative mechanical tilt mount with spill containment;
- implement serial microcontroller protocol;
- execute motion profiles locally on MCU;
- add RUN_START synchronization LED or equivalent;
- recover actual vessel pose from fiducials;
- characterize backlash, repeatability and maximum safe motion envelope;
- run automated W01 quasi-static tilt sequence.

Exit criterion:

- repeated commanded inputs yield measured pose trajectories with known repeatability.

## Phase E — first CyberSand discriminators

Goal: use real measurements to rank competing water implementations.

Priority tests:

- W02 step tilt/slosh;
- W04 obstacle/pooling geometry;
- W05 dam break.

Tasks:

- capture multiple physical repeats;
- export equivalent CyberSand observables;
- align physical and simulated coordinate systems;
- compute per-metric error profiles;
- record performance/state cost of each simulation candidate;
- produce a model-selection report.

Exit criterion:

- the physical rig changes or materially strengthens a CyberSand water-model decision.

If it cannot discriminate candidates, do not automatically add more hardware. First ask whether the chosen observables or experiments are targeting the wrong behaviour.

## Phase F — dynamic system identification

Goal: test frequency response and model generalization if still useful.

Tasks:

- W03 oscillatory forcing;
- multiple amplitudes/frequencies;
- phase/amplitude response extraction;
- withheld-condition validation after parameter fitting;
- investigate grid bias and damping failure modes.

Exit criterion:

- candidate water parameters/models remain credible outside the conditions used for tuning.

## Phase G — internal transport

Goal: extend beyond gross water geometry only if CyberSand design questions require it.

Tasks:

- W06 localized fluorescent pulse;
- characterize intensity/dilution response;
- track tracer centroid/spread/mixing;
- test transport around obstacles;
- optionally revisit visually rich powder-dissolution experiments as W07.

Exit criterion:

- scalar-transport measurements resolve a simulation question that geometry metrics could not.

## Phase H — velocity fields, thermal and other modalities

Optional work, evidence-driven only:

- fluorescent or high-contrast particles;
- coarse PIV/optical flow;
- thin light sheet;
- interleaved fluorescence/backlight imaging;
- thermal surface measurements;
- thermally tagged injections;
- additional sensors if a specific uncertainty justifies them.

No phase-H item is required for a successful initial programme.

## Phase I — generalize realref

Once water reference work is productive, consider whether the same architecture should support:

- granular/sand angle-of-repose and avalanche tests;
- wet granular transitions;
- sediment transport;
- body/fluid coupling objects;
- settling and suspension;
- viscosity families;
- multi-material reference experiments.

Generalization should reuse the established principles:

- controlled input;
- engineered observability;
- synchronized acquisition;
- common physical/simulation observables;
- explicit uncertainty;
- model selection rather than hardware accumulation.

## Immediate next action

Do **Phase A just far enough to enable Phase B**.

The highest-leverage practical session is to find the camera, lights and dye kit, identify their labels/models, and make a simple stationary cup/cell screening scene. The servo can remain in a drawer until the optical pipeline proves that fluorescent water can be extracted robustly from the primary camera.
