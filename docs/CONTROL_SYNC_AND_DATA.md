# Control, synchronization and data

## Control architecture

Initial target:

```text
Development PC
    |
    | USB serial
    v
Microcontroller ----> servo
    |
    +---------------> optional LED/strobe control

Primary camera ------> Development PC
Thermal camera ------> Development PC (optional)
```

The microcontroller should execute time-critical motion locally after receiving a complete command or short programme. Avoid relying on host-side serial command timing for smooth motion.

## Minimal serial protocol

A human-readable prototype protocol is sufficient initially. Candidate commands:

```text
PING
STATUS
HOME
GOTO <angle_deg> <duration_ms>
HOLD <duration_ms>
SWEEP <start_deg> <end_deg> <duration_ms>
OSC <centre_deg> <amplitude_deg> <period_ms> <cycles>
LED <channel> <0|1|level>
ARM <experiment_id>
RUN
STOP
```

Microcontroller responses should include monotonic local timestamps where possible:

```text
ACK <command_id> <mcu_us>
STATE <mcu_us> <commanded_angle> <output_value> ...
EVENT <mcu_us> RUN_START
EVENT <mcu_us> RUN_END
```

Exact syntax is not important yet. Determinism, logging and explicit units are.

## Motion generation

Avoid direct discontinuous servo jumps unless that is intentionally part of a benchmark.

Useful motion profiles:

- linear ramp;
- cosine/smoothstep ramp;
- sinusoid;
- triangle wave;
- stepped quasi-static sequence.

Store the requested profile parameters in the experiment manifest. The physical pose recovered from the video remains authoritative for comparison.

## Synchronization hierarchy

From strongest to weakest:

1. hardware-triggered camera plus microcontroller-controlled illumination/actuation;
2. camera exposure/strobe output observed by microcontroller;
3. common visual synchronization marker in camera field;
4. LED flash driven by microcontroller and detected in video;
5. host monotonic timestamps for camera frames plus serial logs.

Mk1 can work with option 4 or 5. A visible synchronization LED is cheap and robust: pulse a small marker LED at RUN_START and optionally at known intervals. Its observed frame supplies a direct alignment point between actuation logs and video.

## Why host arrival timestamps are not enough

USB camera frames can be buffered. Host receive time may therefore jitter relative to exposure time. For 120 FPS measurements, record whatever frame timestamps the camera API exposes and characterize their stability before relying on them for high-frequency phase measurements.

## Actual pose is part of the data

For quantitative runs, derive tank pose from fiducials on every frame or at a sufficient temporal rate.

Recommended pose fields:

```text
frame_index
t_capture
angle_deg
x_px
y_px
pose_confidence
```

This lets the analysis distinguish:

- servo command error;
- mechanical backlash;
- frame vibration;
- genuine water response.

## Experiment manifest

Every captured run should have a small machine-readable manifest. YAML example:

```yaml
schema: realref.run.v0
experiment_id: W02
run_id: 2026-09-13_W02_001
cell:
  id: cell-01
  internal_width_mm: null
  internal_height_mm: null
  internal_depth_mm: null
fluid:
  type: water
  fill_ml: null
  temperature_c: null
tracer:
  product_id: null
  stock_id: null
  dilution: null
illumination:
  channel_nm: 450
  nominal_power: null
camera:
  id: primary-01
  width: 1920
  height: 1080
  fps: 120
  exposure_us: null
  gain: null
motion:
  profile: step
  start_deg: 0
  end_deg: 15
  duration_ms: 250
sync:
  method: visual_led
notes: ''
```

Unknown values should be explicit `null`, not invented.

## Proposed local dataset layout

```text
data/
  2026-09-13_W02_001/
    manifest.yaml
    camera-primary.mkv
    camera-thermal.mkv        # optional
    mcu.csv
    pose.csv
    calibration/
      dark.png
      empty.png
      flatfield.png
    derived/
      occupancy.zarr          # or compact alternative
      surface.csv
      metrics.json
      preview.mp4
      summary.png
```

This structure is illustrative rather than frozen.

## Repository policy for large files

Do not put raw 1080p/120 FPS recordings directly into ordinary Git history.

The Git repository should contain:

- experiment definitions;
- hardware descriptions;
- calibration procedures;
- schemas;
- analysis/control software;
- compact derived metrics;
- representative reduced-size images where useful;
- checksums/manifests that point to raw captures.

Raw captures should initially stay in a clearly organized local data directory with backup. A later decision can choose among Git LFS, release assets, object storage, NAS storage or another dataset system.

## Run identifiers

Use immutable run IDs. Suggested form:

```text
YYYY-MM-DD_<experiment>_<sequence>
```

For example:

```text
2026-09-13_W01_003
```

If a run is invalid, retain its manifest and mark it invalid with a reason rather than reusing its ID.

## Checksums

For promoted benchmark datasets, generate SHA-256 checksums for raw recordings and logs. This makes it possible to know which physical source produced a derived result even if large files live outside Git.

## Reproducibility level

Not every exploratory recording needs exhaustive metadata. Distinguish:

- **exploratory** — quick visual test;
- **characterization** — fixed settings and recorded configuration;
- **benchmark** — repeatable procedure, complete manifest, calibration and checksums.

Only benchmark runs should be used to make strong simulation model-selection claims.
