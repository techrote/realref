# Fluorescent tracers

## Available starter-kit materials

Known labels from the existing artist/tracer kit:

- Rhodamine B500
- Erythrosine B
- Fluorescein
- Bromofluorescein
- Pyronine Y
- Optical Brightener

These names are sufficient for an experiment shortlist, but **not yet sufficient for quantitative chemical assumptions**. Artist/tracer products can differ in formulation, salt form, purity, additives and naming. `B500` in particular should be treated as a product label until the original supplier information or SDS is recovered.

Before repeated use, record for every material:

- manufacturer/supplier;
- product name and catalogue identifier;
- lot/batch if available;
- approximate purchase date;
- SDS or original safety sheet;
- listed chemical identity and concentration/purity;
- storage history;
- visual condition of powder/liquid;
- known staining or vessel-compatibility behaviour.

## Why empirical screening should come before dye selection

The existing illumination spans 365–450 nm, the camera is monochrome, and the exact camera/window/filter response is not yet known. Therefore the best tracer for this rig is the one that gives the best **measured signal-to-background ratio and useful dynamic range**, not necessarily the one whose literature excitation maximum appears closest to an available LED.

Human-visible vividness remains valuable information. Pyronine Y was specifically remembered as exceptionally striking in prior experiments and should therefore remain in the first screening set even if its nominal spectral optimum is not the most obvious match to the available sources.

Likewise, prior experiments showed that adding powdered dye directly to water can create visually complex dissolution plumes and strong concentration-dependent colour changes. Those effects are interesting in their own right, but they mean that a powder-dissolution recording should not automatically be interpreted as a calibrated concentration or velocity field.

## Measurement modes and tracer requirements

### Water-geometry mode

Goal: make the whole water volume easy to segment.

Preferred tracer properties:

- strong fluorescence at low concentration;
- low background from the empty cell;
- low excitation leakage into the camera;
- broad exposure headroom before saturation;
- minimal wall adsorption/staining;
- acceptable photostability for the run duration;
- repeatable response over the intended pH range.

Absolute concentration calibration is not initially required if the goal is a binary occupancy mask.

### Scalar-transport mode

Goal: follow mixing and advection from a localized addition.

Additional requirements:

- fluorescence intensity should be monotonic with concentration over the useful range;
- self-absorption/inner-filter effects should be characterized;
- injection volume and concentration should be known;
- illumination non-uniformity should be corrected or at least measured.

### Dissolution-plume mode

Goal: intentionally observe powder dissolution, plume formation and concentration gradients.

This is a distinct experiment rather than a shortcut to velocity measurement. It can be highly informative for qualitative transport, especially given the striking prior observations, but the source term is changing in time as the powder dissolves.

## Initial screening matrix

Each tracer should be tested against each available excitation source:

| Excitation | Available source |
| --- | --- |
| 365 nm | resin lamp |
| 385 nm | resin lamp |
| 395 nm | resin lamp |
| 410 nm | resin lamp |
| 420 nm | resin lamp |
| 450 nm | 20 W XHP |

For each pair, capture at minimum:

1. empty-cell frame;
2. clear-water frame;
3. very low tracer concentration;
4. low concentration;
5. moderate concentration;
6. high concentration or practical saturation point;
7. short time series to check bleaching/flicker.

Use fixed camera settings during a comparison series.

## What to score

A simple 0–5 score or measured metric can be recorded for:

- camera signal above clear-water background;
- excitation leakage;
- saturation headroom;
- vessel/background fluorescence;
- apparent photobleaching;
- wall staining after rinse;
- ease of cleanup;
- spatial uniformity;
- pH sensitivity observed in ordinary test water;
- qualitative visual usefulness;
- suitability for occupancy segmentation;
- suitability for concentration mapping.

The best geometry tracer and the best transport tracer do not need to be the same material.

## Concentration series

Avoid starting with arbitrary scoop-sized additions if the goal is quantitative comparison. Once a promising tracer is identified, make a simple stock solution and dilute by known ratios.

Record:

- stock preparation mass/volume if a suitable scale is available;
- stock container and date;
- dilution ratios;
- test-water source;
- approximate temperature;
- pH if convenient and relevant;
- cell fill depth.

For early screening, relative dilution ratios are more important than laboratory-grade absolute molarity.

## Filters

The rig may work without an emission filter if the tracer signal dominates the excitation background, but a suitable camera-side optical filter can dramatically improve segmentation.

Before purchasing filters, first determine empirically:

- which excitation/tracer pairs are promising;
- whether the camera window passes the desired fluorescence;
- how much direct LED light reaches the sensor;
- whether geometry can reduce glare sufficiently.

Only then choose a long-pass or band-pass filter. This avoids buying a theoretically correct filter for a tracer that performs poorly in the actual cell.

## Known optical complications to watch

### Self-absorption and inner-filter effects

Very concentrated fluorescent solutions can become less linearly related to concentration and can even appear darker in the interior. Do not assume brighter powder or stronger colour means a better quantitative tracer.

### pH response

Some fluorescein-family dyes can change fluorescence strongly with pH. This may be useful later as a sensor but is a confounder for concentration measurements unless controlled.

### Adsorption and staining

Some dyes can strongly stain plastics, silicone, seals, work surfaces and skin. A dedicated sacrificial test cell and spill tray are preferable.

### Photobleaching

High-intensity near-UV/blue illumination can reduce fluorescence over time. A short fixed exposure window and an illumination-on-only-during-capture policy may reduce this.

### Camera spectral response

A monochrome/IR-sensitive sensor is advantageous because there is no Bayer colour mosaic, but the installed window, lens coatings and any IR filter can dominate the actual spectral response. Characterise the complete assembled camera, not the bare sensor specification.

## Recommended first-pass shortlist

Do not permanently select a tracer yet. For the first bench session, prioritize:

- Fluorescein — obvious candidate for blue excitation and geometry work.
- Optical Brightener — obvious candidate for 365–395 nm excitation.
- Pyronine Y — include because prior subjective visibility was exceptional.
- Rhodamine B500 — include because rhodamine-family materials are often optically strong, but verify the exact product identity.

Then test Erythrosine B and Bromofluorescein in the same matrix rather than excluding them from literature assumptions.

The result of this screening should be a repository table with actual camera measurements and representative stills, not a purely theoretical ranking.
