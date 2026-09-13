# Measurement and computer vision strategy

## Objective

The computer-vision pipeline should be designed around **specific measurable quantities**, not around a general ambition to "understand the water." The optical setup should simplify extraction until the first useful pipeline is little more than calibrated image processing.

## Primary derived products

### 1. Water occupancy mask

A binary or probabilistic per-pixel estimate of water presence.

Useful for:

- pool geometry;
- wet/dry boundaries;
- front position;
- occupied area as a 2-D volume proxy;
- detached droplets;
- comparison with CyberSand cell occupancy.

### 2. Free-surface contour

An ordered sub-pixel or pixel-level curve describing the water/air interface.

Useful for:

- surface angle;
- crest/trough motion;
- wave amplitude;
- dominant spatial modes;
- settling time.

### 3. Vessel pose

Rigid transform of the cell/frame relative to the camera/world.

Useful for:

- correcting servo error and backlash;
- transforming free surfaces into world coordinates;
- stabilizing the image before comparison;
- recovering actual forcing.

### 4. Scalar tracer field

An intensity-derived field associated with fluorescent tracer concentration.

Useful for:

- plume centroid;
- mixing;
- advection;
- residence and transport between regions.

Do not call it concentration until linearity and illumination correction have been characterized.

### 5. Velocity field

Deferred product from seeded-particle optical flow/PIV.

Useful only if occupancy, free-surface and scalar-transport metrics cannot discriminate the simulation candidates sufficiently.

## Proposed Mk1 processing chain

For fluorescence geometry mode:

1. decode raw frame;
2. subtract dark/background frame;
3. flat-field illumination if necessary;
4. detect vessel fiducials;
5. rectify to a canonical vessel coordinate system;
6. threshold or classify fluorescent water pixels;
7. morphological cleanup with minimal kernel size;
8. extract connected water region(s);
9. extract free-surface contour;
10. compute experiment-specific metrics;
11. retain both raw and derived data for audit.

The pipeline should avoid opaque ML segmentation unless simple calibrated thresholding demonstrably fails. Deterministic processing is easier to validate and reproduce.

## Background subtraction

Capture reference states for each optical mode:

- LEDs off / dark;
- LEDs on with empty cell;
- clear water if relevant;
- uniform tracer fill at a known level.

A static empty-cell image can remove scratches, reflections and non-uniform fluorescence from the vessel. If the vessel moves relative to the camera, either rectify by pose before subtraction or attach the background correction to vessel coordinates.

## Flat-field correction

The 30° reflector and curing-lamp geometry may produce strong brightness gradients. A uniform fluorescent fill can be used to estimate a gain field.

Avoid aggressive correction near pixels where the illumination is extremely weak; it amplifies noise. Mechanical repositioning of the lights is preferable to correcting a very poor illumination field in software.

## Segmentation

Preferred initial hierarchy:

1. fixed intensity threshold after background correction;
2. threshold normalized by flat-field response;
3. hysteresis thresholding if edges are weak;
4. simple temporal consistency if necessary;
5. only then consider learned segmentation.

A key acceptance criterion is that the chosen threshold should remain stable across an entire experiment and preferably across repeat runs with identical settings.

## Free-surface extraction

For a side-view narrow cell, a practical method is:

- rectify vessel coordinates;
- for each x-column, identify the uppermost connected water pixel;
- reject wall/meniscus regions;
- fit or smooth only enough to remove isolated segmentation noise;
- retain the unsmoothed contour too.

For splashing experiments, a single-valued height function may fail. In those cases retain the full occupancy contour and separately identify the dominant bulk free surface.

## Sub-pixel estimation

Sub-pixel edge position can be estimated from fluorescence intensity gradients if it materially improves comparisons. This should be postponed until pixel-level extraction uncertainty is smaller than experiment-to-experiment physical variation.

## Pose estimation

Use rigid fiducials outside the wetted region.

The output should include at least:

- rotation angle;
- x/y translation;
- confidence or residual error;
- timestamp/frame index.

Perspective or lens distortion should be calibrated once using a grid if measurable at the working distance.

## Temporal measurements

From free-surface or occupancy time series, derive:

- crest/trough tracks;
- centre of occupied area;
- principal surface angle;
- dominant oscillation frequencies;
- damping envelope;
- settling time;
- front position and speed.

Definitions must be fixed before comparing simulation candidates. For example, "settled" might mean all selected metrics remain within a tolerance band for a fixed duration.

## Scalar tracer imaging

Raw fluorescence intensity is affected by more than tracer concentration:

- excitation intensity;
- path length;
- self-absorption;
- camera response;
- bleaching;
- pH;
- reflections;
- vessel geometry.

For early qualitative transport, background-corrected normalized intensity may be sufficient. For quantitative concentration, prepare calibration images across known relative dilutions under identical geometry.

Potential scalar metrics that do not require perfect absolute calibration:

- intensity-weighted centroid;
- second spatial moment/spread;
- normalized entropy/mixing index;
- fraction of tracer signal in predefined regions;
- time to cross a threshold at a downstream location.

## PIV / optical flow later

A 120 FPS global-shutter camera is promising for coarse PIV-like work if suitable tracer particles and illumination are available.

However, adding particles introduces additional questions:

- buoyancy and settling velocity;
- particle size;
- particle-fluid coupling;
- wall adhesion;
- depth-of-field ambiguity;
- whether particles alter the fluid or surface behaviour.

Therefore velocity-field measurement is explicitly Phase 2+, not required for initial water-model selection.

## Comparing real and simulated imagery

The strongest comparison uses the same derived quantities on both sides rather than comparing raw appearance.

Examples:

- physical occupancy mask vs simulated occupancy mask;
- physical free-surface contour vs simulated free-surface contour;
- centre-of-mass trajectory vs simulated mass centroid;
- physical front x(t) vs simulated front x(t);
- physical damping curve vs simulated damping curve.

The simulation renderer should be considered an observation model: convert simulation state into the same canonical coordinate system and resolution as the extracted physical data.

## Error metrics

Candidate metrics include:

- intersection-over-union of occupancy masks;
- symmetric contour distance;
- RMS free-surface height error;
- front-position RMSE over time;
- centre-of-mass trajectory error;
- oscillation-frequency error;
- damping-time error;
- final-pool-height error;
- tracer-centroid trajectory error.

Do not collapse everything into one weighted score too early. A per-metric profile is more informative when deciding why one simulation model differs from another.

## Uncertainty

Every derived metric should eventually carry at least a practical uncertainty estimate derived from:

- repeat runs;
- pose-estimation residuals;
- segmentation threshold sensitivity;
- calibration uncertainty;
- frame timing uncertainty.

The central model-selection question is not whether a simulation is numerically identical to one physical run, but whether the difference between candidate models is larger than the uncertainty and run-to-run variability of the reference bench.
