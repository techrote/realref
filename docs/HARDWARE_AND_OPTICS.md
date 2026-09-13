# Hardware and optics

## Known hardware inventory

### Primary camera

- USB monochrome/IR camera.
- 1920×1080.
- 120 FPS.
- Global shutter.

This is the primary scientific camera because the global shutter and high frame rate are well suited to slosh, splashes, front propagation and stroboscopic illumination.

Items still to identify:

- exact sensor model;
- pixel size;
- lens focal length and aperture range;
- whether an IR-cut, IR-pass or clear window/filter is installed;
- supported exposure/gain ranges at 120 FPS;
- whether auto-exposure/auto-gain can be fully disabled;
- whether hardware trigger input/output is exposed;
- whether frame timestamps are device-derived or host-arrival timestamps;
- raw pixel formats and bit depth;
- usable frame rate at full resolution with uncompressed capture.

### Secondary thermal camera

- FLIR USB camera.
- 256×192.
- 25 FPS.
- Mechanically aligned with the primary camera in the same housing.

Treat this as optional during the first water programme. Typical long-wave thermal cameras cannot observe bulk water through ordinary glass or acrylic because those materials are opaque in the relevant infrared band. It may still be useful for open-surface temperature fields, vessel-wall response, thermally tagged additions, or later experiments specifically designed around its optical path.

Items to identify:

- exact FLIR model and spectral band;
- whether radiometric frames are available;
- exact relative camera geometry and parallax;
- minimum focus distance;
- synchronization possibilities.

### Actuation

- 5 kg-rated servo available.
- Microcontroller can be controlled over serial from the development PC.

The quoted servo rating should not be treated as a complete mechanical specification. Required checks include actual model, torque units and voltage, speed, deadband, gear backlash, duty-cycle limits and current draw.

For quantitative work, do not assume commanded servo angle equals cell angle. Use visual fiducials, an encoder or an IMU/angle sensor to estimate actual pose.

### Illumination

Available custom resin-curing lamp channels:

- 365 nm
- 385 nm
- 395 nm
- 410 nm
- 420 nm

Additional source:

- 20 W 450 nm XHP LED
- approximately 30° reflector

This is an unusually useful excitation set because it allows empirical screening across near-UV to blue rather than selecting tracers from datasheet maxima alone.

## Recommended Mk1 geometry

Prefer a **flat-sided transparent cell** over a cylindrical jar for quantitative imaging.

Reasons:

- reduced lensing/refraction;
- simpler geometric calibration;
- simpler free-surface extraction;
- easier obstacle placement;
- easier dimensional measurements;
- better correspondence with a 2-D cellular simulation.

A narrow-depth rectangular cell is especially attractive if the desired reference is approximately two-dimensional. Depth should still be large enough to avoid wall-dominated capillary behaviour becoming the primary phenomenon.

Record internal width, height and depth precisely. The useful geometry is the inside wetted volume, not nominal outside dimensions.

## Optical layout candidates

### Mode A — fluorescence geometry

- dark, non-fluorescent background;
- excitation incident from the side/back/top as appropriate;
- fluorescent water volume;
- camera-side long-pass or band-pass filter if available;
- fixed manual exposure/gain.

Target: high-contrast occupancy mask and free surface.

### Mode B — backlit silhouette

- diffuse bright panel behind vessel;
- clear or lightly dyed water;
- short exposure.

Target: water/air interfaces, droplets and gross geometry using refraction/attenuation rather than fluorescence.

### Mode C — localized fluorescent scalar tracer

- mostly clear water;
- small injected tracer pulse;
- excitation/filter combination optimized for tracer.

Target: mixing, advection and recirculation patterns.

### Mode D — particle tracking

- sparse approximately neutrally buoyant particles;
- high-contrast illumination;
- optional thin light sheet.

Target: optical flow or PIV-like velocity fields. Deferred until geometry metrics are insufficient.

## Interleaved illumination

If LED switching can be controlled with microsecond-to-millisecond timing, a single 120 FPS global-shutter camera may support alternating illumination modes, for example:

- even frames: fluorescence excitation;
- odd frames: backlight/silhouette.

That could yield two synchronized effective 60 FPS measurement channels without a second visible camera.

This requires confirmation of exposure timing, LED rise/fall time, camera buffering and frame timestamps. It should be treated as an optimization, not a Mk1 dependency.

## Camera characterisation before rig construction

Run a short bench test for each candidate illumination channel and tracer before designing around it.

Measure or record:

- dark frame;
- empty-cell background;
- clear-water background;
- tracer signal at several concentrations;
- saturation point;
- excitation leakage into the camera;
- vessel/background fluorescence;
- spatial illumination non-uniformity;
- photobleaching over a representative recording duration;
- frame-to-frame exposure stability;
- maximum exposure compatible with 120 FPS.

A visually spectacular tracer can still be a poor quantitative tracer if it saturates immediately, strongly self-absorbs, reacts to pH, leaves persistent wall staining, or produces little camera contrast after excitation rejection.

## Fiducials

Put machine-readable or easily trackable fiducials on the rigid moving frame, not on the fluid cell interior.

They can provide:

- actual angle;
- translation;
- perspective correction;
- motion timing;
- crop registration;
- independent evidence of servo backlash or vibration.

A simple high-contrast geometric marker may be preferable to a complex tag at 120 FPS if exposure is very short.

## Mechanical note: tilt is not always equivalent to rotating gravity

For quasi-static experiments, tilting the cell slowly is approximately equivalent to changing the gravity direction in the cell frame.

For rapid servo motions, this equivalence breaks down. Angular acceleration, translational acceleration of the cell, centrifugal effects, compliance and wall motion can contribute to the fluid response.

Therefore:

- use slow tilt for clean static/gravity-direction tests;
- measure actual pose during dynamic tests;
- either reproduce vessel kinematics in the simulation or explicitly treat rapid-tilt tests as system-response benchmarks rather than pure gravity-vector tests.

This distinction should be preserved in all later experiment definitions.
