# SN74AXC8T245PWR

- **Manufacturer:** Texas Instruments
- **Function:** 8-bit dual-supply bus transceiver, 0.65–3.6 V on each port, two direction-control pins, tri-state outputs
- **Package:** TSSOP-24 (PW), 7.8 × 6.4 mm nominal, 0.65 mm pitch
- **Datasheet:** SN74AXC8T245, SCES875C (March 2018, revised January 2024), sha256 `6cf4003c438c…` in `manifest.toml`
- **BOM v1 line:** 95 (TDM input path)

## Summary

The SN74AXC8T245 is an 8-bit non-inverting translator with independent supplies VCCA and VCCB (each 0.65–3.6 V). DIR1 sets the direction of bits 1–4 and DIR2 that of bits 5–8; OE (active low) disables all outputs. The control pins are referenced to VCCA (SCES875C §3, §7.3.2, Table 7-1, pp. 1, 20). Ioff and a VCC-isolation feature put the outputs in high impedance when either supply is off (§3, p. 1). In the T1 it buffers the HAT TDM input (BCLK_IN, FS_IN, DIN0–3) from the HAT's 3.3 V side to the SoC's 1.8 V VCCIO6 bank (BOM v1 line 95).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, VCCA, VCCB | — | −0.5 | 4.2 | V | SCES875C p. 4, §5.1 |
| Input voltage, VI (A port, B port, control) | — | −0.5 | 4.2 | V | p. 4 |
| Output voltage, high-impedance or power-off state | A or B port | −0.5 | 4.2 | V | p. 4 |
| Output voltage, high or low state | A port / B port | −0.5 | VCCA + 0.2 / VCCB + 0.2 | V | p. 4 |
| Input clamp current, IIK | VI < 0 | −50 | — | mA | p. 4 |
| Output clamp current, IOK | VO < 0 | −50 | — | mA | p. 4 |
| Continuous output current, IO | — | −50 | 50 | mA | p. 4 |
| Continuous current through VCCA, VCCB or GND | — | −100 | 100 | mA | p. 4 |
| Junction temperature, TJ | — | — | 150 | °C | p. 4 |
| Storage temperature | — | −65 | 150 | °C | p. 4 |
| ESD, HBM | JS-001 | — | ±8000 | V | p. 4, §5.2 |
| ESD, CDM | JESD22-C101 | — | ±1000 | V | p. 4, §5.2 |

## Recommended operating conditions

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VCCA, VCCB | — | 0.65 | 3.6 | V | p. 5, §5.3 |
| VIH, data inputs | VCCI 1.1–1.95 V | 0.65 × VCCI | — | V | p. 5 |
| VIH, data inputs | VCCI 3–3.6 V | 2 | — | V | p. 5 |
| VIL, data inputs | VCCI 1.1–1.95 V | — | 0.35 × VCCI | V | p. 5 |
| VIL, data inputs | VCCI 3–3.6 V | — | 0.8 | V | p. 5 |
| VIH, control inputs (DIR, OE) | VCCA 1.1–1.95 V | 0.65 × VCCA | — | V | p. 5 |
| VIL, control inputs (DIR, OE) | VCCA 1.1–1.95 V | — | 0.35 × VCCA | V | p. 5 |
| Input voltage, VI | — | 0 | 3.6 | V | p. 5 |
| Output voltage, active / tri-state | — | 0 | VCCO / 3.6 | V | p. 5 |
| Input transition rate, Δt/Δv | — | — | 10 | ns/V | p. 5 |
| Operating free-air temperature | — | −40 | 125 | °C | p. 5 |

Unused data inputs must be held at VCCI or GND (§5.3 note 3, p. 5); the integrated pull-downs (below) do that. Control inputs must never float (§7.4, p. 20).

### Electrical characteristics (selected, −40 to 85 °C)

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VOH | IOH = −8 mA, VCC = 1.65 V | 1.2 | — | V | p. 6, §5.5 |
| VOH | IOH = −12 mA, VCC = 3 V | 2.3 | — | V | p. 6 |
| VOL | IOL = 8 mA, VCC = 1.65 V | — | 0.45 | V | p. 6 |
| VOL | IOL = 12 mA, VCC = 3 V | — | 0.7 | V | p. 6 |
| Control input leakage, II | VI = VCCA or GND | −0.5 | 0.5 | µA | p. 6 |
| Ioff, A or B port | Own supply at 0 V, VI or VO 0–3.6 V | −4 | 4 | µA | p. 6 |
| IOZ, A or B port | OE = VIH | −4 | 4 | µA | p. 6 |
| Ci, control | VCC = 3.3 V | — | 4.5 typ | pF | p. 6 |
| Cio, data I/O | VCC = 3.3 V | — | 5.7 typ | pF | p. 6 |

Integrated static pull-down on every data I/O, 288 kΩ typical; an external pull-up, if any, must be ≤ 30 kΩ (§7.3.4, p. 20). Thermal (PW): RθJA 92.0 °C/W (p. 5, §5.4).

## Power by mode

Static supply current, VI = VCCI or GND, IO = 0 (p. 6, §5.5):

| Condition | VCCA | VCCB | Max, −40 to 85 °C | Max, −40 to 125 °C | Unit |
|---|---|---|---|---|---|
| ICCA, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 19 | 40 | µA |
| ICCB, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 18 | 38 | µA |
| ICCA + ICCB | 0.65–3.6 V | 0.65–3.6 V | 25 | 55 | µA |
| ICCB, VCCA off | 0 V | 3.6 V | 12 | 25 | µA |
| ICCA, VCCB off | 3.6 V | 0 V | 12 | 25 | µA |

Dynamic power uses the power-dissipation capacitance per transceiver at 25 °C (§5.14, pp. 15–16). For B → A with outputs enabled at VCCA = VCCB = 1.8 V: CpdA 13 pF, CpdB 1.7 pF; at 3.3 V: CpdA 18.1 pF, CpdB 2.5 pF. The datasheet gives no figure for the mixed 1.8/3.3 V case.

## Pinout and package

PW pin numbers (Figure 4-1, Table 4-1, pp. 2–3):

| Pin | Name | Description |
|---|---|---|
| 1 | VCCA | A-port supply, 0.65–3.6 V |
| 2 | DIR1 | Direction of bits 1–4, referenced to VCCA |
| 3–10 | A1–A8 | A-port I/Os, referenced to VCCA |
| 11 | DIR2 | Direction of bits 5–8, referenced to VCCA; tie to GND for SN74AVC8T245 compatibility |
| 12, 13 | GND | Ground |
| 14–21 | B8–B1 | B-port I/Os (B8 on 14 … B1 on 21), referenced to VCCB |
| 22 | OE | Output enable, active low; high places all outputs in high impedance; referenced to VCCA |
| 23, 24 | VCCB | B-port supply, 0.65–3.6 V |

Outline PW0024A (drawing 4220208/A, p. 29): body 7.7–7.9 × 4.3–4.5 mm, lead span 6.2–6.6 mm, 0.65 mm pitch, leads 0.19–0.30 mm, 1.2 mm maximum height; JEDEC MO-153. MSL Level-1-260C-UNLIM, NiPdAu, −40 to 125 °C, reel 2000 (p. 25).

## Recommended footprint / land pattern

PW0024A example board layout (p. 30, drawing 4220208/A, scale 10:1): 24 pads 1.5 × 0.45 mm (reference), 0.65 mm pitch, 5.8 mm between pad-row centres (reference); non-solder-mask-defined preferred, 0.05 mm maximum mask clearance. Stencil example on p. 31.

## Application circuit and required passives

- 0.1 µF bypass capacitor on VCCA and on VCCB (Figure 8-1, p. 21; §8.4.1, p. 23).
- OE to VCCA through a pull-up resistor so the I/Os stay in high impedance during power-up and power-down; the minimum value is set by the current-sinking capability of the OE driver (§3, p. 1).
- DIR1 and DIR2 driven or strapped to a valid level (§7.4, p. 20).
- Optional pads for series resistors or loading capacitors on signal paths to adjust edges (§8.4.1, p. 23).
- Power sequencing: ground first; no other sequencing requirement (§8.3, p. 23).

## Interfaces and timing

Function table (Table 7-1, p. 20):

| OE | DIR1 | DIR2 | Bits 1–4 | Bits 5–8 |
|---|---|---|---|---|
| H | X | X | High impedance | High impedance |
| L | L | L | B → A | B → A |
| L | L | H | B → A | A → B |
| L | H | L | A → B | B → A |
| L | H | H | A → B | A → B |

Simultaneous up- and down-translation in one part needs both VCCA and VCCB ≥ 1.40 V (§7.3.2, p. 20). Up to 380 Mbps from 1.8 V to 3.3 V (§1, p. 1).

Switching, VCCA = 1.8 V, VCCB = 3.3 V ± 0.3 V, maximum (§5.11, p. 12):

| Parameter | −40 to 85 °C | −40 to 125 °C | Unit |
|---|---|---|---|
| tpd, A → B | 5 | 5 | ns |
| tpd, B → A | 4 | 4 | ns |
| tdis, OE → A | 37 | 40 | ns |
| tdis, OE → B | 57 | 60 | ns |
| ten, OE → A | 17 | 19 | ns |
| ten, OE → B | 9 | 10 | ns |

Minimum tpd in all cases is 0.5 ns.

## Linux driver

None.

## Simulation models available

None listed in `manifest.toml`. Whether TI publishes an IBIS model for this device is **UNVERIFIED**.

## Design notes for the T1

- **Direction.** All six TDM-in lines go HAT (3.3 V) → SoC (1.8 V). With A = 1.8 V side and B = 3.3 V side, DIR1 = DIR2 = L gives B → A on all eight bits (Table 7-1). Strap both DIR pins to GND; the two spare channels stay as inputs held low by the internal 288 kΩ pull-downs (§7.3.4, p. 20). If the A and B sides are swapped in the schematic, the straps invert.
- **Supply side assignment.** BOM v1 puts VCCIO6 (1.8 V) on one side and "HAT 3.3 V" on the other. Whether VCCB is the HAT's own 3.3 V rail (gated with the HAT) or the T1's always-present 3.3 V is not stated: **UNVERIFIED**. Both work: if VCCB is off, VCC isolation forces all outputs to high impedance (§3, p. 1) and Ioff limits back-current to ±4 µA per pin (p. 6).
- **OE.** OE is active low and referenced to VCCA (1.8 V). Pull it up to VCCA and let the SoC or the TCA6416A drive it low only when a HAT with audio is present. The recommended input-voltage range (0–3.6 V, p. 5) covers the control inputs, so a 3.3 V TCA6416A port may drive OE; its thresholds stay at 0.65/0.35 × VCCA. Whether the inputs stay within the Ioff/back-current limits when VCCA is off and a 3.3 V port still drives OE is **UNVERIFIED**; an open-drain drive with the pull-up to VCCA avoids the question.
- **Timing.** With a 4–5 ns propagation delay (p. 12), BCLK and FS are delayed equally; DIN-to-BCLK skew through one package is not specified (**UNVERIFIED**) and should be checked against the I2S/TDM setup and hold of the SoC at the highest HAT sample rate.
- **Edge rate.** Δt/Δv ≤ 10 ns/V on inputs (p. 5): HAT-side clock edges over the flat cable must stay inside that limit.

## Sources

- TI, *SN74AXC8T245 8-Bit Dual-Supply Bus Transceiver With Configurable Voltage Translation and Tri-State Outputs*, SCES875C, revised January 2024, <https://www.ti.com/lit/ds/symlink/sn74axc8t245.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 95, §4.2
