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
  - Impedence: ~90ohm.
- Design traces and planes to handle the maximum current.
- Place a unidirectional TVS diode across VBUS and GND.

#### AGND, DGND, P(Power)GND isolation

- Isolate AGND, DGND, and PGND.
- Either connect by a single plane, or *star ground*.
- For analog circuits, AGND should be as close as to analog ref voltage, filter capacitor or amps.
- For digital circuits, DGND should be as close as to digital power source and output payload.
- For PGND, delegated GND can be used, and it can be connected to A/DGND by capacitor or at a *star ground*.

#### DC-DC

- Minimize SW(switch)–FB(feedback) trace length to reduce noise.
- Keep the inductor away from sensitive analog, high speed digital traces.
- Use GND via fences around the inductor to contain switching noise.
- Place capacitors close to IC pins, largest to smallest (bulk → high-frequency).
- Estimate the temp rise using the chip’s *thermal resistance (°C/W)* and account for ventilation or airflow (copper pour/vias/thermals).

#### SDRAM

##### Single SDRAM

- Point to point layout
- Place next to BGA
  - Distance: 600-800mil (no resistors between), 800-1000mil (has resistors between)
- As always, put filter capacitors next to pins.

##### Dual SDRAM

- Symmetric to CPU
- When there is enough space, put them on the same layer.
- When there isn't enough space, put them on the top and bottom respectively.
- The distance between them is as same as the one for single SDRAM.

##### Notes

- Impedence: ~50ohm.
- Try to keep each 9 traces on the same layer (D0-D7, LDQM, D8-D15, HDQM).
- Keep 3W principle, and the distance between data lines, address lines, and clock lines should be at least 20mil or at least 3W.
  - Add a GND trace between them if possible, width is around 15-30mil.
- Lower 8bit data lines should be length-matched: tolarence~50mil.
- Higher 8bit data lines should be length-matched: tolarence~50mil.
- Address, control, and clock lines should be length-matched: tolarence~100mil.

#### TF Card

- Speed: <=25Mhz: Single-ended impedence: ~50ohm
- Speed: >25Mhz: Differential impedance: ~95ohm
