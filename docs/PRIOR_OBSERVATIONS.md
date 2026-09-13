# Prior tracer observations

This file records qualitative observations from earlier informal fluorescent-dye experiments so they are not lost before formal bench screening begins.

## Recovered image

One recovered photograph shows powdered fluorescent tracer added directly to water in a glass jar under strong excitation. The image has not yet been added to this repository; it currently exists only in the conversation that initiated `realref`.

Visible qualitative features:

- a small amount of undissolved powder remains near the centre;
- highly fluorescent filamentary plumes extend away from the source region;
- some plumes appear as narrow curls/sheets before diffusing into the bulk;
- the bulk liquid remains much darker than the newly dissolved tracer region, giving very high visual contrast;
- the image demonstrates that direct powder addition can generate strong spatial texture without seeded particles.

This is potentially useful for qualitative transport and dissolution studies, but should not be mistaken for a clean velocity field because the source term is changing as solid tracer dissolves.

## Remembered concentration-dependent colour sequence

A separate prior experiment is remembered as especially striking:

- the dry tracer appeared earth red;
- concentrated solution initially appeared deep blood orange;
- at lower concentration it appeared lime green;
- at still lower concentration it became yellow.

The identity of that tracer is not currently known. Recovering the original photos/videos and identifying the product would be valuable because strong concentration-dependent apparent colour may indicate a useful combination of absorption, fluorescence, self-absorption and camera/illumination response.

For the monochrome scientific camera, colour itself is not directly available, but the same concentration-dependent optical behaviour could produce a strong non-linear intensity response. That could be either useful or problematic depending on the measurement goal.

## Pyronine Y recollection

Pyronine Y is specifically remembered as the most strikingly vivid tracer in the old kit.

This subjective observation is worth preserving as a screening priority, even though final tracer selection should be empirical with the actual 365/385/395/410/420/450 nm sources and the assembled monochrome camera.

## Thermal imaging vessel observations

Prior practical testing also established a strong vessel/material dependency for thermal imaging:

- **Thermal camera + glass jar:** effectively useless for this purpose because reflections dominate/interfere with the desired observation.
- **Thermal camera + box made from suitable plastics + halogen backlighting:** produced excellent silhouetting. This configuration may also contain quantitative information around object/fluid boundaries and thin regions, potentially supporting alpha/occupancy estimation and depth/thickness inference from edge/transmission response.

The plastic type, wall thickness, geometry, halogen placement and thermal-camera settings were not recorded here and should be characterized before treating intensity as quantitative depth or alpha evidence. The key empirical observation is nevertheless strong: suitable plastic plus halogen backlighting is a promising thermal/transmission imaging geometry, whereas the glass-jar geometry is not.

## Why these observations matter

The old experiments suggest two distinct optical modes may be available using materials already on hand:

1. **Uniform low-concentration fluorescence** for easy water segmentation.
2. **Localized powder/stock addition** for visually rich transport fields.

The second mode may provide enough spatial texture to estimate plume motion without adding particles, but dissolution kinetics and intensity non-linearity make it a different measurement from PIV.

The thermal observations add a third potentially useful measurement channel: a deliberately selected plastic vessel/enclosure with halogen backlighting may provide a high-contrast silhouette and possibly edge/thin-region transmission information suitable for calibrated alpha or depth/thickness estimation.

## Recovery tasks

When practical:

- find remaining photos/videos from the earlier experiments;
- identify which tracer appears in the recovered green-plume photograph;
- identify the tracer responsible for the red/orange/lime/yellow sequence;
- record the excitation source used, if remembered;
- record whether the experiments used tap, distilled or other water;
- record whether any pH modifier or other additive was present;
- identify/test the plastic materials that work well with the thermal camera and halogen backlight;
- characterize reflection/transmission behaviour for candidate vessel materials;
- test whether edge/thin-region thermal intensity can be calibrated against known thickness/depth or occupancy/alpha;
- add representative media to an appropriate dataset/media location without placing large raw videos into ordinary Git history.

Until those details are recovered, these observations should remain explicitly qualitative rather than being used as calibration evidence.
