# realref

`realref` is a physical-reference and experiment-control project for comparing simulated material behaviour with repeatable real-world observations.

The first target is **water behaviour for CyberSand**. The immediate concept is a small transparent test cell driven by a serial-controlled microcontroller/servo, observed by a 1080p 120 FPS monochrome global-shutter camera. A co-aligned 256×192 25 FPS FLIR camera is available as a secondary instrument. Fluorescent tracers and controlled illumination are intended to make image extraction deliberately easy rather than relying on fragile general-purpose computer vision.

This repository is intentionally broader than one water experiment: if the workflow proves useful, it can later host granular, mixed-material, wetting, settling, and other physical-reference benches.

## Current hardware and materials

Known available equipment:

- 1080p, 120 FPS monochrome/IR USB camera with global shutter.
- 256×192, 25 FPS FLIR USB camera mechanically aligned in the same housing.
- 5 kg-rated servo.
- Microcontroller suitable for deterministic serial control from the development PC.
- Custom illumination with 365, 385, 395, 410 and 420 nm LEDs.
- 20 W 450 nm XHP LED with approximately 30° reflector.
- Fluorescent/tracer kit containing:
  - Rhodamine B500
  - Erythrosine B
  - Fluorescein
  - Bromofluorescein
  - Pyronine Y
  - Optical Brightener

The exact chemical identity, formulation, age, source and SDS for each tracer still need to be recorded before quantitative or repeated experiments.

## Core idea

Do not ask computer vision to infer transparent water from arbitrary imagery. Engineer the scene so the desired physical quantity is easy to observe.

The first programme therefore separates several measurement goals:

1. **Water geometry:** occupancy, free-surface contour, splashes, droplets, pool shape and front propagation.
2. **Dynamic response:** wave period, damping, settling time, centre-of-mass motion and response to known forcing.
3. **Internal transport:** dye concentration fields, mixing and advection.
4. **Velocity:** later, sparse tracer particles and PIV/optical-flow-style measurements if needed.

A uniformly fluorescent volume is excellent for geometry but usually poor for measuring internal velocity; a localized dye pulse or seeded particles are separate instruments.

## Initial document pack

- [`docs/SCOPE_AND_PRINCIPLES.md`](docs/SCOPE_AND_PRINCIPLES.md) — what `realref` is for and what it should not become.
- [`docs/HARDWARE_AND_OPTICS.md`](docs/HARDWARE_AND_OPTICS.md) — current hardware, optical layout and bench-characterisation needs.
- [`docs/TRACERS.md`](docs/TRACERS.md) — tracer inventory, selection strategy and empirical screening plan.
- [`docs/EXPERIMENTS.md`](docs/EXPERIMENTS.md) — first water benchmarks and why each exists.
- [`docs/MEASUREMENT_AND_CV.md`](docs/MEASUREMENT_AND_CV.md) — extraction targets, metrics and computer-vision strategy.
- [`docs/CONTROL_SYNC_AND_DATA.md`](docs/CONTROL_SYNC_AND_DATA.md) — servo control, timing, calibration and data layout.
- [`docs/CYBERSAND_COMPARISON.md`](docs/CYBERSAND_COMPARISON.md) — how physical observations should constrain or select simulation models.
- [`docs/SAFETY_AND_HANDLING.md`](docs/SAFETY_AND_HANDLING.md) — minimum optical, electrical, mechanical and chemical controls.
- [`docs/OPEN_QUESTIONS.md`](docs/OPEN_QUESTIONS.md) — clarifications required before hardware design is frozen.
- [`docs/ROADMAP.md`](docs/ROADMAP.md) — staged path from inventory to useful physical-model discrimination.

## Near-term priority

The highest-value next step is **not** building a complex rig. It is bench-characterising the existing camera, light sources and dye kit together. Human-visible vividness is useful but camera SNR, excitation leakage, vessel fluorescence, pH response, self-absorption and exposure headroom determine which tracer is best for each measurement mode.

The first physical rig should remain deliberately simple, cheap and reversible until the measurement pipeline has demonstrated that it can discriminate between competing CyberSand water behaviours.
