# TCA9406DCUR

- **Manufacturer:** Texas Instruments
- **Function:** 2-bit bidirectional I2C and SMBus voltage-level translator, auto-direction, with internal 10 kΩ pull-ups and output enable
- **BOM v1 lines:** 94 (second source for the HAT ID translator PCA9306DCUR)
- **Package:** VSSOP-8 (DCU, "US8"), 2.30 × 2.00 mm body (nominal), 0.5 mm pitch
- **Datasheet:** TCA9406, SCPS221G (October 2010, revised November 2018), `tca9406.pdf`. The `manifest.toml` entry for this MPN currently points at the PCA9306 datasheet (URL `pca9306.pdf`, sha256 `1cd97c734729…`); the correct file is <https://www.ti.com/lit/ds/symlink/tca9406.pdf>, sha256 `fdb80d682fbacd5ef18cbafc57e4d9375a295daa38da33721af6e055f8a7da61` (downloaded 2026-10-22)
- **Status:** Not in the current BOM (removed in BOM v1.1 as second source for PCA9306DCUR: not pin-compatible, §9 item D9). Partly UNVERIFIED

## Summary

The TCA9406 is a 2-bit auto-direction translator for I2C and SMBus: a pass-gate between the A port (1.65–3.6 V, VCCA) and the B port (2.3–5.5 V, VCCB) with one-shot rising-edge accelerators and internal 10 kΩ pull-ups on all four I/Os, rated to 1 MHz Fast-mode Plus (SCPS221G §3, §8.1, pp. 1, 18). OE is referenced to VCCA; OE low puts all I/Os in high impedance and disables the pull-ups (§8.3.4, p. 19). In the T1 it is the listed second source for the HAT ID translator, PCA9306DCUR (BOM v1 line 94). It is not pin-compatible with the PCA9306 (see Pinout).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, VCCA | — | −0.5 | 4.6 | V | SCPS221G p. 6, §6.1 |
| Supply voltage, VCCB | — | −0.5 | 6.5 | V | p. 6 |
| Input voltage, VI | A port / B port | −0.5 | 4.6 / 6.5 | V | p. 6 |
| Output voltage, high-impedance or power-off | A port / B port | −0.5 | 4.6 / 6.5 | V | p. 6 |
| Output voltage, high or low state | A port / B port | −0.5 | VCCA + 0.5 / VCCB + 0.5 | V | p. 6 |
| Input clamp current, IIK | VI < 0 | — | −50 | mA | p. 6 |
| Output clamp current, IOK | VO < 0 | — | −50 | mA | p. 6 |
| Continuous output current, IO | — | — | ±50 | mA | p. 6 |
| Continuous current through VCCA, VCCB or GND | — | — | ±100 | mA | p. 6 |
| Storage temperature | — | −65 | 150 | °C | p. 6 |
| ESD, HBM, A port | JS-001 | — | ±2500 | V | p. 6, §6.2 |
| ESD, HBM, B port | JS-001 | — | ±8000 | V | p. 6, §6.2 |
| ESD, CDM | JESD22-C101 | — | ±1500 | V | p. 6, §6.2 |
| ESD, MM | A115-A | — | ±250 | V | p. 6, §6.2 |

## Recommended operating conditions

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VCCA | — | 1.65 | 3.6 | V | p. 7, §6.3 |
| VCCB | — | 2.3 | 5.5 | V | p. 7 |
| VIH, A-port I/Os | VCCA 1.65–1.95 V | VCCI − 0.2 | VCCI | V | p. 7 |
| VIH, A-port I/Os | VCCA 2.3–3.6 V | VCCI − 0.4 | VCCI | V | p. 7 |
| VIH, B-port I/Os | — | VCCI − 0.4 | VCCI | V | p. 7 |
| VIH, OE | — | 0.65 × VCCA | 5.5 | V | p. 7 |
| VIL, A-port and B-port I/Os | — | 0 | 0.15 | V | p. 7 |
| VIL, OE | — | 0 | 0.35 × VCCA | V | p. 7 |
| Input transition rate, push-pull and control | — | — | 10 | ns/V | p. 7 |
| Operating free-air temperature | — | −40 | 85 | °C | p. 7 |

VCCA must be ≤ VCCB except during power-on transients (§6.3 note 1, p. 7). The VIL maximum of 0.15 V is given so that a valid VOL is kept; VOL is VIL plus the pass-gate drop (§6.3 note 2, p. 7).

### Electrical characteristics (selected, −40 to 85 °C)

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VOHA | IOH = −20 µA, VIB ≥ VCCB − 0.4 V | 0.67 × VCCA | — | V | p. 8, §6.5 |
| VOLA | IOL = 1 mA, VIB ≤ 0.15 V | — | 0.4 | V | p. 8 |
| VOHB | IOH = −20 µA, VIA ≥ VCCA − 0.2 V | 0.67 × VCCB | — | V | p. 8 |
| VOLB | IOL = 1 mA, VIA ≤ 0.15 V | — | 0.4 | V | p. 8 |
| Ioff, A port (VCCA = 0) / B port (VCCB = 0) | — | — | ±2 | µA | p. 8 |
| IOZ, A or B port | OE < VIL | — | ±2 | µA | p. 8 |
| Cio, A port / B port | VCC = 3.3 V | — | 6 / 7.5 | pF | p. 8 |

Thermal (DCU): RθJA 199.1 °C/W (p. 7, §6.4).

## Power by mode

Static supply current, VI = VO = open, IO = 0, −40 to 85 °C (p. 8, §6.5):

| Mode | VCCA | VCCB | ICCA max | ICCB max | Unit |
|---|---|---|---|---|---|
| Both supplies on | 1.65 V to VCCB | 2.3–5.5 V | 2.4 | 12 | µA |
| Both supplies on, total ICCA + ICCB | 1.65 V to VCCB | 2.3–5.5 V | 14.4 (total) | — | µA |
| VCCB off | 3.6 V | 0 V | 2.2 | −1 | µA |
| VCCA off | 0 V | 5.5 V | −1 | 1 | µA |

With an I/O held low, current also flows through the internal 10 kΩ pull-ups (§8.3.5, p. 20); that DC current is set by the bus and is not a datasheet figure. OE low disables the pull-ups and "significantly reduces the quiescent current" (§3, p. 1); no separate figure is given.

## Pinout and package

DCU pin numbers (Pin Functions, p. 5):

| Pin | Name | Type | Description |
|---|---|---|---|
| 1 | SDA_B | I/O | B side, referenced to VCCB |
| 2 | GND | GND | Ground |
| 3 | VCCA | Power | A-port supply, 1.65–3.6 V, VCCA ≤ VCCB |
| 4 | SDA_A | I/O | A side, referenced to VCCA |
| 5 | SCL_A | I/O | A side, referenced to VCCA |
| 6 | OE | Input | Output enable, active high, referenced to VCCA |
| 7 | VCCB | Power | B-port supply, 2.3–5.5 V |
| 8 | SCL_B | I/O | B side, referenced to VCCB |

Outline DCU0008A (drawing 4225266/A, p. 32), the same outline as the PCA9306DCUR: 0.5 mm pitch, lead span 3.0–3.2 mm, 0.9 mm maximum height. MSL Level-1-260C-UNLIM, NiPdAu or Sn, −40 to 85 °C, reel 3000 (p. 25).

## Recommended footprint

DCU0008A example board layout (p. 33, drawing 4225266/A): 8 pads 0.85 × 0.3 mm (reference), 0.5 mm pitch, 3.1 mm between pad-row centres (reference), non-solder-mask-defined preferred. Stencil on p. 34. The land is identical to the PCA9306DCUR's, but the pin assignment is not (see Design notes).

## Application circuit and required passives

From Figure 11 (p. 21), §10 (p. 23) and §11 (p. 23):

- 0.1 µF bypass on VCCA and on VCCB, close to the pins (Figure 11, p. 21; Figure 13, p. 23).
- No external pull-ups needed (internal 10 kΩ on every I/O). External ones may be added in parallel to speed up edges; lower values raise VOL (§8.3.5, p. 20).
- OE can be tied to VCCA for always-on (Figure 11 note). To guarantee high impedance during power-up and power-down, pull OE to GND and enable only after VCCA and VCCB are stable (§10, p. 23).
- Keep traces short: the round-trip delay of any reflection must be below the ≈ 30 ns one-shot duration (§8.3.3, p. 19; §11.1, p. 23).

## Interfaces and timing

Auto-direction pass-gate with one-shot accelerators (≈ 30 ns, driver ≈ 50–70 Ω during acceleration, §8.3.1, p. 18). Open-drain operation up to 2 Mbps; push-pull up to 21–24 Mbps depending on supplies (§6.6–6.8, p. 9).

Selected switching characteristics, VCCA = 1.8 V ± 0.15 V, VCCB = 3.3 V ± 0.3 V (§6.9, p. 10):

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| tPHL, A → B | Open-drain | 2.4 | 9.6 | ns |
| tPLH, A → B | Open-drain | — | 40 | ns |
| tPHL, B → A | Open-drain | 1.1 | 4.4 | ns |
| tPLH, B → A | Open-drain | — | 4.5 | ns |
| ten, OE → A or B | — | — | 200 | ns |
| tdis, OE → A or B | — | — | 200 | ns |
| trA, A-port rise | Open-drain | 30 | 132 | ns |
| trB, B-port rise | Open-drain | 23 | 106 | ns |
| Maximum data rate | Open-drain / push-pull | 2 / 22 | — | Mbps |
| Minimum pulse width, open-drain | — | 500 | — | ns |

## Linux driver

None (transparent translator).

## Simulation models

None listed in `manifest.toml` (and the manifest datasheet entry for this MPN is wrong, see header). Whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **Not a drop-in for the PCA9306DCUR.** Same DCU outline and land, different pinout (PCA9306: 1 GND, 2 VREF1, 3 SCL1, 4 SDA1, 5 SDA2, 6 SCL2, 7 VREF2, 8 EN; TCA9406: 1 SDA_B, 2 GND, 3 VCCA, 4 SDA_A, 5 SCL_A, 6 OE, 7 VCCB, 8 SCL_B). Using it as a second source needs its own footprint or a different schematic. BOM v1 lists it as a second source without noting this.
- **Low-level threshold.** VIL on the I/Os is 0.15 V maximum (p. 7). Any device on the HAT ID bus (EEPROM, or a HAT's own I2C target) must pull below 0.15 V at the TCA9406 pin for the low to pass. Standard I2C targets only guarantee VOL ≤ 0.4 V at 3 mA; whether the HAT EEPROM meets 0.15 V against the 10 kΩ pull-up is **UNVERIFIED**.
- **OE level.** OE is referenced to VCCA (VIH 0.65 × VCCA, p. 7), so a 1.8 V GPIO can drive it directly; the PCA9306 needs a 3.3 V enable.
- **Isolation.** With OE low the internal pull-ups are off, so HAT-side lines float unless the HAT provides pull-ups (§8.3.4, p. 19). With either supply at 0 V, both ports are high-impedance (§1, p. 1), and either supply may ramp first (§10, p. 23).
- **Supplies.** VCCA = 1.8 V (VCCIO4) and VCCB = 3.3 V meet VCCA ≤ VCCB (p. 7).

## Sources

- TI, *TCA9406 2-Bit Bidirectional 1-MHz, I2C Bus and SMBus Voltage-Level Translator With 8-kV HBM ESD*, SCPS221G, revised November 2018, <https://www.ti.com/lit/ds/symlink/tca9406.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 94
