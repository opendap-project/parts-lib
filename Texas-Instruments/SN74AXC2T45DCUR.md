# SN74AXC2T45DCUR

- **Manufacturer:** Texas Instruments
- **Function:** 2-bit dual-supply translating transceiver, 0.65–3.6 V on each port, one direction pin, no output enable
- **BOM v1 lines:** 95 (I2S-A MCLK and DOUT on the DAC clock)
- **Package:** VSSOP-8 (DCU), 2 × 3.1 mm nominal, 0.5 mm pitch
- **Datasheet:** SN74AXC2T45, SCES880D (August 2019, revised January 2024), `sn74axc2t45.pdf`, sha256 `2fbbad36930a9d370e15affdf9378246188b43efc53ba338f79f36ea29564990` (downloaded 2026-10-22 from <https://www.ti.com/lit/ds/symlink/sn74axc2t45.pdf>). The `manifest.toml` entry for this MPN currently points at the SN74AXC8T245 datasheet (sha256 `6cf4003c438c…`)
- **Status:** Partly UNVERIFIED

## Summary

The SN74AXC2T45 is a 2-bit non-inverting translator with independent supplies VCCA and VCCB (each 0.65–3.6 V). A single DIR pin, referenced to VCCA, sets the direction of both bits; the part has no output-enable pin (SCES880D §3, Table 4-1, Table 7-1, pp. 1–2, 20). Both ports go to high impedance when either supply is below 100 mV, and the outputs are glitch-free in any supply order (§1, p. 1). In the T1 it carries the HAT I2S-A MCLK and the DOUT on the DAC clock from the SoC's 1.8 V VCCIO6 bank to the HAT's 3.3 V side (BOM v1 line 95).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, VCCA, VCCB | — | −0.5 | 4.2 | V | SCES880D p. 3, §5.1 |
| Input voltage, VI (A port, B port, control) | — | −0.5 | 4.2 | V | p. 3 |
| Output voltage, high-impedance or power-off state | A or B port | −0.5 | 4.2 | V | p. 3 |
| Output voltage, high or low state | A port / B port | −0.5 | VCCA + 0.2 / VCCB + 0.2 | V | p. 3 |
| Input clamp current, IIK | VI < 0 | −50 | — | mA | p. 3 |
| Output clamp current, IOK | VO < 0 | −50 | — | mA | p. 3 |
| Continuous output current, IO | — | −50 | 50 | mA | p. 3 |
| Continuous current through VCC or GND | — | −100 | 100 | mA | p. 3 |
| Junction temperature | — | — | 150 | °C | p. 3 |
| Storage temperature | — | −65 | 150 | °C | p. 3 |
| ESD, HBM | JS-001 | — | ±8000 | V | p. 3, §5.2 |
| ESD, CDM | JESD22-C101 | — | ±1000 | V | p. 3, §5.2 |

## Recommended operating conditions

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VCCA, VCCB | — | 0.65 | 3.6 | V | p. 4, §5.3 |
| VIH, data inputs | VCCI 1.1–1.95 V | 0.65 × VCCI | — | V | p. 4 |
| VIH, data inputs | VCCI 3–3.6 V | 2 | — | V | p. 4 |
| VIL, data inputs | VCCI 1.1–1.95 V | — | 0.35 × VCCI | V | p. 4 |
| VIL, data inputs | VCCI 3–3.6 V | — | 0.8 | V | p. 4 |
| VIH / VIL, DIR | VCCA 1.1–1.95 V | 0.65 × VCCA | 0.35 × VCCA | V | p. 4 |
| Input voltage, VI | — | 0 | 3.6 | V | p. 4 |
| Output voltage, active / tri-state | — | 0 | VCCO / 3.6 | V | p. 4 |
| Input transition rate, all channels | — | — | 10 | ns/V | p. 4 |
| Input transition rate, one channel while the others are static | — | — | 100 | ns/V | p. 4 |
| Operating free-air temperature | — | −40 | 125 | °C | p. 4 |

Unused inputs must be held at VCC or GND (§5.3 note 2, p. 4); the internal pull-downs do that.

### Electrical characteristics (selected, −40 to 85 °C)

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VOH | IOH = −8 mA, VCC = 1.65 V | 1.2 | — | V | p. 5, §5.5 |
| VOH | IOH = −12 mA, VCC = 3 V | 2.3 | — | V | p. 5 |
| VOL | IOL = 8 mA, VCC = 1.65 V | — | 0.45 | V | p. 5 |
| VOL | IOL = 12 mA, VCC = 3 V | — | 0.7 | V | p. 5 |
| DIR input leakage | VI = VCCA or GND | −0.5 | 0.5 | µA | p. 5 |
| Data input leakage | VI = VCCI or GND | −4 | 4 | µA | p. 5 |
| Ioff, A or B port | Own supply at 0 V | −4 | 4 | µA | p. 5 |
| Ci (DIR) / Cio (data) | VCC = 3.3 V | — | 3.3 / 5.4 typ | pF | p. 5 |

Integrated static pull-down on every data I/O, 71 kΩ typical; an external pull-up must be ≤ 7 kΩ (§7.3.9, p. 19). Thermal (DCU): RθJA 242.9 °C/W (p. 4, §5.4).

## Power by mode

Static supply current, VI = VCCI or GND, IO = 0 (p. 5, §5.5):

| Condition | VCCA | VCCB | Max, −40 to 85 °C | Max, −40 to 125 °C | Unit |
|---|---|---|---|---|---|
| ICCA, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 8 | 14 | µA |
| ICCB, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 8 | 14 | µA |
| ICCA + ICCB | 0.65–3.6 V | 0.65–3.6 V | 16 | 23 | µA |
| ICCB, VCCA off | 0 V | 3.6 V | 4 | 8 | µA |
| ICCA, VCCB off | 3.6 V | 0 V | 4 | 8 | µA |

Dynamic power: power-dissipation capacitance per transceiver at 25 °C in §5.14 (p. 14).

## Pinout and package

DCU pin numbers (Figure 4-2, Table 4-1, p. 2):

| Pin | Name | Description |
|---|---|---|
| 1 | VCCA | A-port supply, 0.65–3.6 V |
| 2 | A1 | A-port I/O, referenced to VCCA |
| 3 | A2 | A-port I/O, referenced to VCCA |
| 4 | GND | Ground |
| 5 | DIR | Direction of both bits, referenced to VCCA |
| 6 | B2 | B-port I/O, referenced to VCCB |
| 7 | B1 | B-port I/O, referenced to VCCB |
| 8 | VCCB | B-port supply, 0.65–3.6 V |

Outline DCU0008A (drawing 4225266/A, p. 33): 0.5 mm pitch, lead span 3.0–3.2 mm, 0.9 mm maximum height; JEDEC MO-187 variation CA. MSL Level-1-260C-UNLIM, Sn finish, −40 to 125 °C, reel 3000 (p. 26).

## Recommended footprint

DCU0008A example board layout (p. 34, drawing 4225266/A): 8 pads 0.85 × 0.3 mm (reference), 0.5 mm pitch, 3.1 mm between pad-row centres (reference), non-solder-mask-defined preferred. Stencil on p. 35.

## Application circuit and required passives

- Bypass on VCCA and VCCB close to the device: 0.1 µF recommended; 1 µF and 0.1 µF in parallel improve transient response (§8.4.1, p. 23).
- DIR strapped or driven to a valid level referenced to VCCA.
- Supplies: ground first; no ramp-order or ramp-rate requirement (§8.3, p. 23).

## Interfaces and timing

Function table (Table 7-1, p. 20): DIR = L → B data to A bus (A outputs, B inputs); DIR = H → A data to B bus. Input circuits of the data I/Os are always active. Up to 380 Mbps from 1.8 V to 3.3 V (§1, p. 1).

Switching, VCCA = 1.8 V ± 0.15 V, VCCB = 3.3 V ± 0.3 V, maximum (§5.11, p. 11):

| Parameter | −40 to 85 °C | −40 to 125 °C | Unit |
|---|---|---|---|
| tpd, A → B | 5 | 5 | ns |
| tpd, B → A | 4 | 5 | ns |
| tdis, DIR → A | 16 | 17 | ns |
| tdis, DIR → B | 12 | 13 | ns |
| ten, DIR → A (calculated) | 171 | 171 | ns |
| ten, DIR → B (calculated) | 20 | 21 | ns |

Minimum tpd is 0.5 ns. Enable times are calculated as tdis of the opposite port plus tpd (§8.1.1 Equations 1–2, p. 21).

## Linux driver

None.

## Simulation models

None listed in `manifest.toml` (and the manifest datasheet entry for this MPN points at the wrong document, see header). Whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **No output enable.** BOM v1 line 95 says "Ioff and OE isolate an absent HAT" for all three translators, but this part has no OE pin (Table 4-1, p. 2). Its only isolation is VCC isolation: if VCCA or VCCB is below 100 mV, both ports go to high impedance (§1, p. 1). For MCLK and DOUT to be quiet towards an absent or unpowered HAT, VCCB must be a rail that is switched off with the HAT, or DIR must be set to B → A so the HAT-side pins become inputs (held low by the 71 kΩ pull-downs). Which rail feeds VCCB is not fixed in BOM v1: **UNVERIFIED**.
- **Direction.** With A = 1.8 V (SoC) and B = 3.3 V (HAT), MCLK and DOUT both go A → B: strap DIR to VCCA. Both bits always share the same direction.
- **Clock quality.** MCLK passes through a CMOS buffer with a 0.5–5 ns propagation window (p. 11); jitter added by the translator is not specified (**UNVERIFIED**). This affects only the HAT branch; the on-board DAC MCLK is not translated (BOM v1 §4.2).
- **Edge rate.** Input transitions must stay within 10 ns/V (100 ns/V for a single switching channel) (p. 4).

## Sources

- TI, *SN74AXC2T45 2-Bit Translating Transceiver with Configurable Level-Shifting*, SCES880D, revised January 2024, <https://www.ti.com/lit/ds/symlink/sn74axc2t45.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 95, §4.2
