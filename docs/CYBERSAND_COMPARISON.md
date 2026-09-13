# CyberSand comparison methodology

## Purpose

The physical bench is useful only if its observations can constrain design choices in CyberSand. This document defines how to compare physical recordings with simulation output without pretending that CyberSand is a continuum CFD solver.

## Compare observables, not rendering

Do not compare a photograph directly with the game's rendered water. Convert both physical and simulated states into common observables.

Preferred observables:

- occupied/wet region;
- free-surface contour;
- water mass centroid;
- leading-front position;
- final pool height;
- slosh frequency;
- damping/settling time;
- tracer centroid and spread;
- later, coarse velocity fields if required.

The simulation should export its state directly. A small observation layer can rasterize or resample it into the same canonical physical coordinate system used by the camera analysis.

## Candidate-model workflow

When several water approaches are plausible:

1. Freeze a physical benchmark definition before tuning candidates.
2. Record several physical repeats.
3. Run every candidate against the same forcing and geometry.
4. Extract the same metrics from physical and simulated data.
5. Report errors per metric rather than only a single aggregate score.
6. Tune only parameters that are legitimately part of the candidate model.
7. Re-run against withheld physical conditions before selecting a model.

This reduces the risk of overfitting one attractive video.

## Physical repeat envelope

For each promoted benchmark, summarize physical variation before comparing simulation models.

Example:

```text
W02, 15° step tilt
physical dominant period: mean ± repeat spread
physical settling time: mean ± repeat spread
physical peak surface angle: mean ± repeat spread
```

A simulation difference smaller than ordinary run-to-run physical variation should not drive architectural complexity unless it matters perceptually or interacts with another system.

## Static tilt as a calibration benchmark

W01 should be nearly trivial for the simulation. Its value is in exposing coordinate, gravity-direction, pose and mass-conservation mistakes.

If a candidate cannot reproduce equilibrium geometry under slow tilt, dynamic comparisons should not be trusted yet.

## Step/slosh as an energy-transport benchmark

W02 is a strong early test because it exposes several common cellular-fluid errors:

- excessive damping;
- momentum that disappears too quickly;
- persistent oscillation with too little damping;
- grid-direction bias;
- implausible free-surface breakup;
- delayed or overly rapid redistribution;
- spurious mass loss/gain.

No single number is enough. Retain surface trajectories plus derived period/damping metrics.

## Obstacle tests as game-relevance benchmarks

W04 is especially important for CyberSand because gameplay geometry is discrete and obstacle-rich.

Useful questions:

- Does water fill connected basins in the correct order?
- Does it equalize levels reasonably?
- Does a narrow connection transmit water too fast or too slowly?
- Does the model create artificial trapped pockets?
- Does it leak through corners or diagonal contacts?
- Does moving around blocks destroy too much momentum?

These can matter more to the game than matching fine wave physics.

## Dam-break test as a transport benchmark

W05 provides a clean front-propagation problem.

Compare:

- front x(t);
- column collapse;
- arrival time at a wall/obstacle;
- reflected-wave timing;
- final distribution.

A model that matches final equilibrium but reaches it through implausible transport should be distinguishable here.

## Dynamic tilt and reference frames

A critical distinction:

- **slow tilt:** changing gravity direction in the vessel frame is a useful approximation;
- **rapid physical rotation:** vessel angular acceleration and moving boundaries contribute to the real response.

For rapid motion, choose one of three comparison strategies:

1. reproduce measured vessel kinematics in the simulation;
2. derive the appropriate non-inertial forcing terms if the simulation remains vessel-fixed;
3. explicitly use the run as a qualitative/system-identification benchmark and avoid claiming one-to-one forcing equivalence.

Do not silently compare a physically accelerated cell against a simulation with only a rotated gravity vector.

## Parameter fitting

If candidate models expose tunable parameters, fit them on a designated training subset of experiments and evaluate on separate validation runs.

Potential training set:

- one W01 angle series;
- one W02 amplitude;
- one W04 geometry.

Potential validation set:

- different W02 amplitude or transition time;
- W03 frequency not used during fitting;
- different W04 obstacle;
- W05 dam break.

The exact split can change, but the concept should remain.

## Behaviour-per-compute-cost

A candidate should not win merely because it is most physically elaborate.

Record at least:

- simulation wall-clock time;
- update cost per active cell/chunk if available;
- memory/state cost;
- determinism/reproducibility;
- compatibility with existing body/material coupling;
- benchmark error profile.

The useful selection criterion is approximately:

> perceptually and mechanically useful physical behaviour per unit of compute/state complexity.

## Model-selection report template

For each candidate:

```text
Candidate:
Revision/commit:
Parameters:

W01 static tilt:
  geometry error:
  mass error:

W02 step/slosh:
  period error:
  damping error:
  contour error:

W04 obstacle:
  final pool error:
  transport timing:

W05 dam break:
  front RMSE:
  arrival-time error:

Performance:
  update time:
  memory/state:

Known qualitative failure modes:
Decision:
```

## Stop condition

The physical programme has done its job when additional measurement fidelity is no longer likely to change the simulation architecture choice.

At that point, preserve the benchmark suite for regression testing rather than continuously expanding the rig for its own sake.
