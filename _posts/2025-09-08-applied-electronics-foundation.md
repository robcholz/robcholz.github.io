# [Foundation] Applied Electronics

## 1. Resistor

### 1.1 Voltage Division
Resistors can be connected in series to divide voltage, commonly used for ADC inputs or op-amp biasing.

- Consider the **resistance ratio** and **ADC resolution** when designing a divider.
- If **low quiescent current** is required, the divider’s output impedance increases, which affects accuracy:
  - The ADC’s internal sampling capacitor may not fully charge.
  - The measured voltage may have error due to the **RC time constant**.
- When measuring **high currents**, use a **high-power resistor** to handle heat dissipation.

---

### 1.2 Current Limiting
Used to limit current to safe levels.

- Typical use cases: LED current control, MOSFET gate protection, transistor base drive.

---

### 1.3 Pull-Up / Pull-Down
Used to define a stable logic level on floating pins (e.g., MCU inputs, I²C lines).

- Provides source current for **open-drain/open-collector** circuits.
- Typical resistance ranges:
  - **I²C:** 2.2k–400kΩ (commonly 4.7k–10kΩ)
  - **MCU GPIO:** ~10kΩ
- When low-power operation is critical, choose higher resistance to reduce **quiescent current**.

---

### 1.4 Stabilization / Damping
Used to isolate and stabilize signal lines.

- Known as **isolation resistors** or **damping resistors**.
- Reduces ringing, EMI, and cross-coupling on high-speed or sensitive traces.

---

## 2. Capacitor

### 2.1 Filtering / Decoupling
Used to smooth voltage and suppress high-frequency noise.

- Place **as close as possible** to IC power pins.
- Typical range: **0.01 µF – 100 µF**.
- Pay attention to **ESR** (Equivalent Series Resistance) and **stability**.

---

### 2.2 Timing / Oscillator
Used in RC or LC timing and oscillator circuits.

- Time constant: **τ = R × C**
- Consider **tolerance**, **temperature drift**, and **leakage current** when selecting values.

---

### 2.3 Coupling / AC Blocking
Used to **pass AC** signals while **blocking DC** bias.

- Common in **audio** and **amplifier** stages.
- Choose capacitors with appropriate **voltage ratings** and **low distortion**.

---

### 2.4 Bypass / Noise Reduction
Used to shunt high-frequency noise and improve signal integrity.

- Small ceramic capacitors (e.g., 0.01 µF, 0.1 µF) are placed close to active components.
- Use **multiple capacitors in parallel** (e.g., 0.1 µF + 10 µF) to cover a wide frequency range.

---

### 2.5 Energy Storage / Pulsing
Used to store and release energy for short bursts.

- Common in **power supplies** and **motor drivers**.
- Use **large electrolytics** or **supercapacitors** with sufficient **voltage** and **ripple current** ratings.

---

### 2.6 Snubber / Damping
Used to suppress voltage spikes, ringing, and protect switches.

- Typically **RC series** networks.
- Values depend on **transient energy**, **switching frequency**, and **load characteristics**.
