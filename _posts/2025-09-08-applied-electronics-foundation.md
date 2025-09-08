# Foundation | Applied Electronics

## Resistor

### Voltage Division

Use multiple resistors to divide voltage, commonly used in ADC, op-amp inputs.

- Pay attention to the proportion of resistances and the resolution of ADC when using ADC.
- When quiescent current is a requirement, pay attention to the internal impedence of the ADC. Error might be enlarged due to increased RC constant (the ADC internal sampling capacitor is not fully charged)!
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
