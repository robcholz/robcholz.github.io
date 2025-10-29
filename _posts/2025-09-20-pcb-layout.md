# [Foundation] PCB Layout Guidelines

## 1. Background

### Trace Width vs Current (1 oz Copper)

| Current | Typical Trace Width | Notes |
|----------|--------------------|-------|
| GPIO / Low current | 6 mil | Standard signal width |
| 0.5 A | 10 mil | Suitable for LEDs, small sensors |
| 1 A | 20 mil |  |
| 2 A | 40 mil |  |
| 5 A | 100 mil |  |
| 10 A | 200 mil | Use solder mask opening and tin coverage |
| 50 A | 500 mil |  |
| 100 A | 1000 mil |  |
| 200 A | 2000 mil |  |
| 500 A | 5000 mil | Use ≥4.5 oz copper or bus bars |

> For high-current paths, widen the trace, increase copper thickness, or apply solder coverage.

### Additional Notes

- On compact boards, silkscreen reference designators can be omitted.
- Follow the **3W rule** for high-speed signal integrity:
  → Distance between traces ≥ 3× trace width.

---

## 2. Layer Stack and Net Allocation

### Two-Layer Board
- Bottom layer should be as continuous **GND plane** as possible.

### Four-Layer Board Options

| Type | Stackup | Characteristics |
|------|----------|----------------|
| **Type 1** | GND / SIG-1 / SIG-2 / PWR | Simple, but discontinuous impedance |
| **Type 2** | SIG-1 / PWR / GND / SIG-2 | Good for top-side components or signals |
| **Type 3** | SIG-1 / GND / PWR / SIG-2 | Good for bottom-side components |

---

## 3. Layout Process

### EMC Improvement

#### 20H Rule
- Shrink the **PWR plane** by:
  - **20 mil** → reduces electric field by ~70%
  - **100 mil** → reduces electric field by ~98%

### Recommended Workflow

1. Place mechanically constrained components first (USB, connectors, mounting holes).
2. Plan functional regions: **power**, **digital**, **analog**.
3. Route critical or high-speed signals first.
4. Add **fanout vias** for low-current power nets.
5. Complete all routing.
6. Optimize critical traces (short, direct, orthogonal).
7. Add **teardrops** and **copper pour**.
8. Refine and balance copper planes.
9. Run **DRC checks**, verify silkscreen and text orientation.
10. Export **Gerber**, **Pick & Place**, and **BOM** files.

---

## 4. Component Placement and Routing

### General
- Align designators consistently (e.g., all facing same direction).

---

### Quartz Crystal
- Guard crystal traces with a **10 mil GND ring**.
- Do **not** route as differential pairs.
- Place **as close as possible** to MCU pins.
- Maintain a **solid GND plane** beneath.

---

### USB 2.0 Interface
- D+/D− are **differential pairs** (~90 Ω differential impedance).
- No copper pour or vias underneath pair.
- Add **bidirectional TVS diode** across D+/D−.
- Add **unidirectional TVS diode** across VBUS and GND.
- Ensure trace widths and planes handle expected **VBUS current**.

---

### Ground Domains
- Separate **AGND**, **DGND**, and **PGND** to minimize interference.
- Connect via:
  - Single point (star ground), or
  - Capacitive coupling between domains.

| Domain | Recommendation |
|---------|----------------|
| **AGND** | Close to analog reference voltage, filters, and amplifiers |
| **DGND** | Near digital ICs and loads |
| **PGND** | For high-current or power circuits; connect to star point or via capacitor |

---

### DC-DC Converter
- Keep **SW** and **FB** traces as short as possible.
- Isolate inductor from analog and high-speed regions.
- Surround with **GND via fence** to confine EMI.
- Place input/output capacitors **close to pins** — from bulk → ceramic.
- Check chip’s **thermal resistance (°C/W)** and ensure adequate copper area or vias for heat dissipation.

---

### SDRAM Design

#### Single SDRAM
- Point-to-point routing.
- Place close to MCU/BGA (600–800 mil without resistors; 800–1000 mil with).
- Decoupling capacitors must be **adjacent to power pins**.

#### Dual SDRAM
- Place **symmetrically** relative to CPU.
- Prefer both on the same layer if space allows; otherwise, top/bottom mirrored.
- Maintain same routing length as single SDRAM layout.

#### Routing Notes
- Target impedance ≈ **50 Ω**.
- Keep each 9-bit group (D0–D7 + LDQM, D8–D15 + HDQM) on one layer.
- Maintain **≥3W spacing** or **20 mil** between data, address, and clock lines.
- Add GND guard traces (15–30 mil) where possible.
- Length-match tolerances:
  - Data lines: ±50 mil
  - Addr/Ctrl/Clock: ±100 mil

---

### TF (MicroSD) Card

| Speed | Impedance Requirement |
|--------|----------------------|
| ≤ 25 MHz | ~50 Ω single-ended |
| > 25 MHz | ~95 Ω differential |
