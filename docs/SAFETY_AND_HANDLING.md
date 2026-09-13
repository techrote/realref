# Safety and handling

This document is deliberately conservative. The existing equipment is capable of producing intense near-UV/blue light, moving mechanical loads and persistent fluorescent contamination. Exact chemical controls must follow the SDS for the actual products once identified.

## Chemical handling

Until each tracer is positively identified from its supplier label/SDS:

- treat powders as laboratory/artist chemicals rather than food-safe colourants;
- avoid inhaling dust;
- avoid eye and skin contact;
- do not pipette by mouth or use food utensils;
- use dedicated containers and tools;
- work over a washable or disposable spill tray;
- label stock solutions clearly;
- keep tracer solutions away from food preparation areas;
- dispose of solutions according to the product SDS and local requirements rather than assuming sink disposal is acceptable.

Some fluorescent dyes stain aggressively even at low concentration. Assume work surfaces, seals, silicone, clothing and porous plastics can be permanently marked until proven otherwise.

## Powder additions

Powder-dissolution experiments are visually valuable but create the highest chance of airborne dust and uncontrolled local concentration.

Prefer:

- tiny quantities;
- low drop height;
- draft-free setup;
- pre-weighed/pre-portioned samples;
- eye protection;
- gloves appropriate to the product SDS.

For ordinary flow experiments, prepared dilute stock solution is preferable to handling dry powder repeatedly.

## Near-UV and blue illumination

Available wavelengths include 365, 385, 395, 410, 420 and 450 nm. The shorter channels are particularly easy to underestimate because brightness perception is a poor measure of optical hazard.

Design the rig so direct viewing of LEDs is unnecessary:

- use physical shielding/enclosure around the test cell;
- prevent direct or mirror-like reflected beams from reaching eyes;
- keep illumination off except during setup/capture when practical;
- use optical protection appropriate to the actual wavelengths and intensity when exposure cannot be engineered out;
- do not rely on tinted glasses without known spectral attenuation;
- avoid placing highly reflective metal or glass surfaces in uncontrolled beam paths.

The 20 W 450 nm source should also be treated as a high-intensity source despite being visible.

## Camera filters are not eye protection

Any long-pass/band-pass filter mounted on the camera is an imaging component. It does not make the surrounding bench safe to view.

## Electrical safety

High-power LEDs and servos can draw substantial current.

- power the servo from a supply appropriate to its model rather than from a microcontroller regulator;
- share grounds only where the design requires it;
- add suitable fusing/current limiting;
- strain-relieve wiring near the moving mechanism;
- keep liquid below and physically separated from exposed power electronics where possible;
- provide a simple means to remove actuator/LED power quickly.

## Mechanical safety

A 5 kg-rated servo can produce enough torque to spill liquid, trap fingers or break a poorly mounted test cell.

The Mk1 mechanism should include:

- hard mechanical travel limits that prevent inversion/spill;
- conservative software angle limits inside the mechanical limits;
- low initial speed/acceleration;
- rigid cell retention;
- a secondary catch tray;
- enough clearance that cables cannot snag;
- a physical stop or power cut that does not depend on the host PC.

Do not infer safe dynamic loads from the servo's marketing torque number alone.

## Spill containment

At minimum:

- primary test cell;
- larger secondary tray;
- absorbent material nearby;
- electronics elevated or physically separated;
- no mains connectors directly below the fluid path.

Fluorescent dye makes tiny leaks easy to see but can also spread contamination far beyond the apparent spill under UV illumination.

## Thermal camera considerations

If a thermally tagged experiment is attempted later, keep temperatures close enough to ambient that neither the vessel nor fluid presents a burn/thermal-shock hazard. Large temperature differences are unnecessary for proving the imaging concept.

## Test-cell compatibility

Before committing to a vessel material, expose a sacrificial sample to each candidate tracer and cleaning method.

Check for:

- staining;
- crazing/clouding;
- swelling of seals;
- persistent fluorescence;
- residue that changes wetting behaviour.

This matters scientifically as well as cosmetically: surface contamination can alter meniscus and wetting behaviour between runs.

## Cleaning protocol

Once a tracer/cell combination is selected, define a repeatable cleaning procedure and blank check:

1. rinse/clean using the approved method;
2. refill with clear water;
3. illuminate using the experimental channel;
4. record a blank frame;
5. reject or flag the cell if residual fluorescence exceeds the allowed background threshold.

## Safety information still required

Before quantitative experimentation, recover or photograph:

- each dye container label;
- manufacturer/supplier names;
- SDS links/files if available;
- servo model and electrical rating;
- LED driver/supply details;
- camera and lens model numbers.

These details should be committed as inventory metadata or summarized in the repository without publishing any unnecessary personal purchase information.
