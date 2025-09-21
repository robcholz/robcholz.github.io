# [Foundation] Applied Electronics

## Resistor

### Voltage Division

Use multiple resistors to divide voltage, commonly used in ADC, op-amp inputs.

- Pay attention to the proportion of resistances and the resolution of ADC when using ADC.
- When quiescent current is a requirement, pay attention to the internal impedence (increased Thevenin eq resistance) of the ADC. Error might be enlarged due to increased RC constant (the ADC internal sampling capacitor is not fully charged).
- When measuring large payload currents, use a large power resistor due to dissipation.

### Current Limiting

Used before LED... gate of MOSFET.

### Pull Up/Down

Give a defined logic level of some floating pins (MCU, I2C...).

Provide source current for open-drain/collector buses.

- 2.2k-400k, 4.7k-100k, 10k are commonly used for I2C; 10k is common for MCU.
- Pay attention to the quiescent current if required.

### Stablize / Damping

Isolation resistor.

## Capacitor

### Filtering / Decoupling

Smooth voltage, reduce high-frequency noise.
	•	Place near IC power pins, typical 0.01µF–100µF.
	•	Watch ESR and stability.

### Timing / Oscillator

- RC/LC for timing or oscillation.
  - τ = R × C, consider tolerance and temperature.

### Coupling / AC Blocking

- Pass AC, block DC.
  - Used in audio/amplifier circuits, watch voltage rating.

### Bypass / Noise Reduction

- Shunt high-frequency noise, improve signal integrity.
  - Small ceramics, parallel multiple values for wide frequency.

### Energy Storage / Pulsing

- Store energy for short bursts.
  - Supercapacitors or large electrolytics, check voltage and ripple current.

### Snubber / Damping

- Suppress spikes/ringing, protect switches.
  - Often RC in series; choose values based on transient energy and frequency.
