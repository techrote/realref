# Open questions and required clarifications

These questions are intentionally separated into **blocking**, **high-value**, and **later** items. The project should not stall waiting for every answer.

## Blocking before quantitative rig design

### Primary camera

- What is the exact make/model or sensor model?
- Does the assembled camera currently have an IR-pass, IR-cut or clear window/filter?
- What lens is fitted?
- Can exposure, gain and frame rate be locked manually?
- Is 1920×1080 at 120 FPS genuinely available as a stable continuous stream?
- What pixel formats/bit depths are available?
- Does the camera expose hardware trigger or strobe pins?
- Does the driver/API provide exposure timestamps or only host arrival times?

### Servo and actuation

- Exact servo model?
- What does the quoted "5 kg" rating correspond to: kg·cm stall torque at what voltage?
- Nominal speed at intended supply voltage?
- Is it an ordinary positional RC servo or another actuator class?
- How much backlash is visible under load?
- What microcontroller is convenient to use?
- Is there already a suitable servo power supply?

### Tracer identity

For each of the six starter-kit materials:

- Can the original container/label be found and photographed?
- Is manufacturer/product information still readable?
- Is an SDS available?
- Is each material still dry/free-flowing or has storage changed it?

Do not assume that generic chemical names fully specify artist/tracer products.

## High-value questions before Mk1 construction

### Test cell

- Is there already a suitable flat-sided glass/acrylic container?
- What approximate internal dimensions are practical?
- Is the desired first reference approximately 2-D, implying a narrow-depth cell?
- How much liquid mass is acceptable on the servo mechanism?
- Can simple removable obstacle inserts be fabricated easily?

### Mechanical arrangement

- Is the preferred concept a vessel rotating about an axis through/near its centre, or a platform tilting about a bottom/edge pivot?
- What angular range is useful while keeping a large spill margin?
- Is the rig expected to do only slow tilts initially, or also aggressive slosh/oscillation?
- Can the cell be mounted so the camera sees a fixed side plane with minimal occlusion from the frame?

### Illumination

- Can individual resin-lamp wavelength channels be switched electronically, or only manually?
- Are LED drivers constant-current and dimmable?
- Can the 450 nm XHP be strobed or rapidly switched?
- Can a diffuse backlight be added independently?
- Are any optical long-pass/band-pass filters already available?

### Existing prior experiments

- Are more photos/videos from the earlier powder-tracer "artsperiment" recoverable?
- Which dye produced the remembered earth-red powder → blood-orange → lime-green → yellow concentration sequence?
- Which dye is shown in the currently recovered green-plume image?
- Were those experiments performed in tap water, distilled/deionized water, or another solution?
- Were multiple dyes ever mixed?

These old observations may reveal useful tracer behaviour before new screening begins.

## Important scientific clarifications

### What exactly should the first water model be judged on?

Rank these priorities for CyberSand if possible:

- correct final pooling/equalization;
- fast plausible redistribution;
- wave/slosh persistence;
- momentum around obstacles;
- thin-film/surface spreading;
- splashes/droplets;
- mixing/advection;
- body-water displacement/coupling;
- wetting/saturation into other materials;
- visual plausibility at game scale.

The physical benchmark suite should weight the behaviours that actually constrain the engine design.

### What is the intended physical scale correspondence?

CyberSand cells do not automatically correspond to millimetres or centimetres. Decide whether the comparison is:

1. dimensionless/qualitative only;
2. mapped to an approximate physical cell size;
3. fitted separately per benchmark.

A dimensionless comparison can still be rigorous using normalized length/time scales, but the choice should be explicit.

### Is real water the intended reference fluid?

The obvious first answer is yes. Later, viscosity can be varied using safe water/glycerol mixtures if there is a reason to explore parameter space, but this should not be introduced until plain-water comparisons are understood.

### How much capillary behaviour is relevant?

A very thin cell can become dominated by wall wetting and meniscus effects that a coarse cellular game simulation does not attempt to reproduce. Cell depth should therefore be chosen to reduce unwanted quasi-2-D wall artefacts while retaining a useful side view.

## Questions that can wait

- Whether to add IMU/encoder feedback.
- Whether to use hardware camera triggering.
- Whether to add a second visible camera.
- Whether to construct a light sheet.
- Whether to use PIV particles.
- Whether to calibrate absolute fluorescence concentration.
- Whether thermal imaging contributes enough to justify a dedicated geometry.
- Whether raw datasets should live in Git LFS, release assets, object storage or a NAS.
- Whether a later rig should support sand/granular materials.

## Decisions not to make yet

Do **not** freeze these based only on literature or intuition:

- "best" fluorescent tracer;
- excitation wavelength;
- camera emission filter;
- final cell dimensions;
- servo motion profile;
- PIV particle choice;
- quantitative dye concentration range.

The existing hardware is broad enough that a short empirical screening session should provide better answers than theoretical preselection.

## Immediate clarification bundle

If only a small amount of hardware information can be recovered next, the most useful bundle is:

1. photo/model of primary camera and lens;
2. photo/model of servo;
3. photos of all tracer labels;
4. rough dimensions/photo of any candidate flat-sided vessel;
5. note on how the resin lamp channels are switched;
6. identification of any existing optical filters.

None of this blocks creation of the software/control skeleton, but it materially improves the first physical build.
