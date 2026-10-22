# SN74AXC1T45DCKR

- **Manufacturer:** Texas Instruments
- **Function:** Single-bit dual-supply bus transceiver, 0.65–3.6 V on each port, direction pin
- **Package:** SC70-6 (DCK), 2 × 2.1 mm nominal, 0.65 mm pitch
- **Datasheet:** SN74AXC1T45, SCES882E (December 2017, revised December 2023), `sn74axc1t45.pdf`, sha256 `41e03bd8f0740ae8bbdf92309e7c82bac1359a768556cbe68de41b0273e49f12` (downloaded 2026-10-22 from <https://www.ti.com/lit/ds/symlink/sn74axc1t45.pdf>). The `manifest.toml` entry for this MPN currently points at the SN74AXC8T245 datasheet (sha256 `6cf4003c438c…`)
- **BOM v1 line:** 96

## Summary

The SN74AXC1T45 is a single-bit non-inverting translator with two supplies, VCCA and VCCB, each 0.65–3.6 V. DIR, referenced to VCCA, selects A → B (high) or B → A (low) (SCES882E §3, Table 7-1, pp. 1, 18). If either supply is below 100 mV, both ports go to high impedance; supplies may ramp in any order (§1, §8.3.1, pp. 1, 22). In the T1 two of them sit on the touch faceplate, between the 3.3 V faceplate bank and the panel's 1.8 V IOVCC: one translates the panel RST (out), the other the TE signal (in) (BOM v1 line 96).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, VCCA, VCCB | — | −0.5 | 4.2 | V | SCES882E p. 4, §5.1 |
| Input voltage, VI (A port, B port, control) | — | −0.5 | 4.2 | V | p. 4 |
| Output voltage, high-impedance or power-off state | A or B port | −0.5 | 4.2 | V | p. 4 |
| Output voltage, high or low state | A port / B port | −0.5 | VCCA + 0.2 / VCCB + 0.2 | V | p. 4 |
| Input clamp current, IIK | VI < 0 | −50 | — | mA | p. 4 |
| Output clamp current, IOK | VO < 0 | −50 | — | mA | p. 4 |
| Continuous output current, IO | — | −50 | 50 | mA | p. 4 |
| Continuous current through VCC or GND | — | −100 | 100 | mA | p. 4 |
| Junction temperature | — | — | 150 | °C | p. 4 |
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
| VIH / VIL, DIR | VCCA 3–3.6 V | 2 | 0.8 | V | p. 5 |
| VIH / VIL, DIR | VCCA 1.1–1.95 V | 0.65 × VCCA | 0.35 × VCCA | V | p. 5 |
| Input voltage, VI | — | 0 | 3.6 | V | p. 5 |
| Output voltage, active / tri-state | — | 0 | VCCO / 3.6 | V | p. 5 |
| Input transition rate, Δt/Δv | — | — | 100 | ns/V | p. 5 |
| Operating free-air temperature | — | −40 | 125 | °C | p. 5 |

### Electrical characteristics (selected, −40 to 85 °C)

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VOH | IOH = −8 mA, VCC = 1.65 V | 1.2 | — | V | p. 6, §5.5 |
| VOH | IOH = −12 mA, VCC = 3 V | 2.3 | — | V | p. 6 |
| VOL | IOL = 8 mA, VCC = 1.65 V | — | 0.45 | V | p. 6 |
| VOL | IOL = 12 mA, VCC = 3 V | — | 0.7 | V | p. 6 |
| DIR input leakage | VI = VCCA or GND | −1 | 1 | µA | p. 6 |
| Data input leakage | VI = VCCI or GND | −4 | 4 | µA | p. 6 |
| Ioff, A or B port | Own supply at 0 V | −5 | 5 | µA | p. 6 |
| CI (DIR) / CIO (A or B) | — | — | 4.4 / 5 typ | pF | p. 6 |

Integrated static pull-down on the data I/Os, 288 kΩ typical; an external pull-up must be ≤ 30 kΩ (§7.3.2, p. 17). Thermal (DCK): RθJA 235.3 °C/W (p. 5, §5.4).

## Power by mode

Static supply current, VI = VCCI or GND, IO = 0 (p. 6, §5.5):

| Condition | VCCA | VCCB | Max, −40 to 85 °C | Max, −40 to 125 °C | Unit |
|---|---|---|---|---|---|
| ICCA, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 8 | 12 | µA |
| ICCB, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 8 | 12 | µA |
| ICCA + ICCB | 0.65–3.6 V | 0.65–3.6 V | 10 | 16 | µA |
| ICCB, VCCA off | 0 V | 3.6 V | 2 | 8 | µA |
| ICCA, VCCB off | 3.6 V | 0 V | 2 | 8 | µA |

Dynamic power: power-dissipation capacitance at 25 °C in §5.7 (p. 11).

## Pinout and package

DCK pin numbers (Figure 4-2, Table 4-1, p. 3):

| Pin | Name | Description |
|---|---|---|
| 1 | VCCA | A-port supply, 0.65–3.6 V |
| 2 | GND | Ground |
| 3 | A | A-port I/O, referenced to VCCA; do not leave floating as an input |
| 4 | B | B-port I/O, referenced to VCCB; do not leave floating as an input |
| 5 | DIR | High: A → B; low: B → A; referenced to VCCA |
| 6 | VCCB | B-port supply, 0.65–3.6 V |

Outline DCK0006A (drawing 4214835/D, p. 30): body 1.85–2.15 × 1.1–1.4 mm, lead span 1.8–2.4 mm, 0.65 mm pitch, leads 0.15–0.30 mm, 0.8–1.1 mm height; JEDEC MO-203 variation AB. MSL Level-1-260C-UNLIM, Sn finish, −40 to 125 °C, reel 3000 (p. 26).

## Recommended footprint / land pattern

DCK0006A example board layout (p. 31, drawing 4214835/D, scale 18:1): 6 pads 0.9 × 0.4 mm (reference), 0.65 mm pitch, 2.2 mm between pad-column centres (reference); non-solder-mask-defined preferred, 0.07 mm maximum mask clearance. Stencil on p. 32.

## Application circuit and required passives

- Bypass capacitors on both supplies (§8.4.1, p. 22). The datasheet gives no value in this section (**UNVERIFIED** value; 0.1 µF per rail is the design choice used for the other AXC parts on this board).
- DIR tied to a fixed level for a unidirectional translator: GND for B → A (Figure 8-1, Table 8-1, p. 19).
- Optional pads for a loading capacitor or pull-up to tune edges (§8.4.1, p. 22).
- Power-up: ground first, then VCCA and VCCB in any order (§8.3.1, p. 22).

## Interfaces and timing

Function table (Table 7-1, p. 18): DIR = L → B data to A bus; DIR = H → A data to B bus. Input circuits of the data I/Os are always active. Up to 500 Mbps from 1.8 V to 3.3 V (§1, p. 1).

Propagation delay, maximum, −40 to 85 °C / −40 to 125 °C (Tables 5-6 and 5-8, pp. 9–10):

| Case | Direction | Max | Unit |
|---|---|---|---|
| VCCA = 1.8 V, VCCB = 3.3 V | A → B | 4 / 5 | ns |
| VCCA = 1.8 V, VCCB = 3.3 V | B → A | 4 / 4 | ns |
| VCCA = 3.3 V, VCCB = 1.8 V | A → B | 4 / 4 | ns |
| VCCA = 3.3 V, VCCB = 1.8 V | B → A | 4 / 5 | ns |

Minimum tpd in all cases is 0.5 ns. Direction-change enable and disable times are in the same tables; they matter only if DIR is switched at run time.

## Linux driver

None. The panel driver controls RST and reads TE through these buffers as plain GPIOs.

## Simulation models available

None listed in `manifest.toml` (and the manifest datasheet entry for this MPN points at the wrong document, see header). Whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **Direction straps.** With VCCA on the 3.3 V faceplate bank and VCCB on the panel IOVCC (1.8 V): the RST part has DIR = VCCA (A → B) and the TE part has DIR = GND (B → A). If the sides are assigned the other way, the straps invert. Because DIR is referenced to VCCA, strapping it to VCCA keeps it valid at any VCCA level.
- **Reset during power-up.** The 288 kΩ internal pull-down (§7.3.2, p. 17) holds an undriven input low. With either supply below 100 mV, the outputs are high-impedance (§1, p. 1), so during faceplate power-up the panel RST input sees only the panel's own bias and the 288 kΩ pull-down on the B pin. Whether that keeps the panel in reset until the SoC drives RST is **UNVERIFIED** against the panel datasheet.
- **Second source.** BOM v1 names the TXU0202 family with direction mapping **UNVERIFIED**; it is a different package and pinout and is not covered by this sheet.
- **Stock.** BOM v1 lists LCSC 702 units at 2026-10-22, the lowest of the AXC parts on this board.

## Sources

- TI, *SN74AXC1T45 Single-Bit Dual-Supply Bus Transceiver With Configurable Voltage Translation*, SCES882E, revised December 2023, <https://www.ti.com/lit/ds/symlink/sn74axc1t45.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 96, §4.2
