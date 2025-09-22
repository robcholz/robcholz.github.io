# [Foundation] PCB Layout

## Background

### Trace Width vs Current (1oz)

- Normal GPIO: 6mil
- 500mA: 10mil
- 1A: 20mil
- 2A: 40mil
- 5A: 100mil
- 10A: 200mil

For larger current, the trace should be covered with solder in practice(or 4.5+oz copper).

- 50A: 500mil
- 100A: 1000mil
- 200A: 2000mil
- 500A: 5000mil

### Notes

- For small-size pcbs, silkscreen referemce designators can be removed.
- Follow 3W principles to improve signal integrity for high-speed traces.

## Layer Net Allocation

- 2 Layer Board: All GND
- 4 Layer Board
  - Type 1: GND, SIG-1, SIG-2, PWR
    - Uncontinuous impedance.
  - Type 2: SIG-1, PWR, GND, SIG-2
    - Useful when key components or signals are on the top.
  - Type 3: SIG-1, GND, PWR, SIG-2
    - Useful when key components or signals are on the bottom.

## Layout

### Increase EMC

#### 20H Rule

- Shrinking the inner PWR plane zone by 20mil can make electric field decrease by 70%, while 100mil can make decrease by 98%.

### Steps

1. Place the constrained components first (USB, wire to wire connectors, mechanic holes...).

2. Plan the power, digital, and analog area.

3. Start with important signal traces.

4. Add fanout vias for small current power.

5. Complete all the traces.

6. Optimize the traces.

7. Add teardrops, copper pour.

8. Optimize the planes.

9. Check DRC, check silk layer(designators), texts and icons.

10. Export Gerber, Pick and Place, BOM.

### DC-DC

- Minimize SW(switch)–FB(feedback) trace length to reduce noise.
- Keep the inductor away from sensitive analog, high speed digital traces.
- Use GND via fences around the inductor to contain switching noise.
- Place capacitors close to IC pins, largest to smallest (bulk → high-frequency).
- Estimate the temp rise using the chip’s *thermal resistance (°C/W)* and account for ventilation or airflow (copper pour/vias/thermals).

### Components

#### Designators

- Face the same directions.

#### Quartz

- Use a 10 mil trace to guard the crystal with GND.
- Do not use differential pair.
- Place the oscillator as close as to MCU.
- Keep a solid GND plane under it.

#### USB 2.0

- Differential pair rule should be applied to D+/D- pair.
  - Keep out area under it.
  - Place a bidirectional TVS diode across them.
- Design traces and planes to handle the maximum current.
- Place a unidirectional TVS diode across VBUS and GND.

#### AGND, DGND, P(Power)GND isolation

- Isolate AGND, DGND, and PGND.
- Either connect by a single plane, or *star ground*.
- For analog circuits, AGND should be as close as to analog ref voltage, filter capacitor or amps.
- For digital circuits, DGND should be as close as to digital power source and output payload.
- For PGND, delegated GND can be used, and it can be connected to A/DGND by capacitor or at a *star ground*.
