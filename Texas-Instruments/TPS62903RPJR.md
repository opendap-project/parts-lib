# TPS62903RPJR

- **Manufacturer:** Texas Instruments
- **Function:** 3 A synchronous step-down converter, 3–17 V input, 0.4–5.5 V output (external divider or 16 resistor-selected fixed voltages), DCS-Control, 2.5 or 1.0 MHz, 4 µA quiescent current, 100 % mode, power good
- **BOM v1 lines:** 38 (Power, HAT_3V3 3.3 V buck from VSYS, qty 1) and 91 (Power, HAT_5V / USB-C source 5.1 V buck from VSYS, qty 1); both new in BOM v1.5 (board ADR 0014), replacing the [TLV62569DBVR](TLV62569DBVR.md) and the [TPS61089RNRR](TPS61089RNRR.md). Inductors on lines 7 and 92 ([XGL4020-102MEC](../Coilcraft/XGL4020-102MEC.md)); passives on line 115
- **Package:** VQFN-HR-9 (RPJ0009A), 1.5 × 2.0 mm, 0.5 mm pitch, 1 mm maximum height
- **Datasheet:** *TPS62903, 3-V to 17-V, High Efficiency and Low IQ Buck Converter in 1.5-mm × 2-mm QFN Package*, SLVSES3A, February 2021, revised March 2021, 51 pages with the addendum. Cited below as "SLVSES3A". File sha256 `323bfe650fdef2fa2c361f1264391a4e0d75c30772a49ee46f6741370250dcee`.
- **Status:** Partly UNVERIFIED

## Summary

The TPS62903 is a DCS-Control synchronous buck converter: 3–17 V input, up to 3 A continuous output, 62 mΩ / 22 mΩ switches, 4 µA quiescent current, selectable 2.5 or 1.0 MHz, ±0.9 % feedback accuracy over −40 to 150 °C, 100 % mode, power good, selectable output discharge, adjustable soft start and tracking, and a MODE/S-CONF pin that selects divider or VSET operation, frequency, discharge and PFM/PWM by one resistor (SLVSES3A, p. 1). In the T1 one part number makes two rails from the 2S VSYS (6.0–8.8 V): 5.1 V for HAT_5V and the USB-C source (VSET 95.3 kΩ) and 3.3 V for HAT_3V3 (VSET open) (board BOM v1.5 lines 38 and 91).

## Absolute maximum ratings

SLVSES3A, p. 4, §6.1. Voltages to ground.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN, EN, PG, MODE/S-CONF | −0.3 | 18 | V |
| SW (DC) | −0.3 | VIN + 0.3 | V |
| SW (AC, < 10 ns, while switching) | −3.0 | 23 | V |
| FB/VSET, SS/TR, VOS | −0.3 | 6 | V |
| TJ | −40 | 150 | °C |
| Tstg | −65 | 150 | °C |

ESD (SLVSES3A, p. 4, §6.2): HBM ±2000 V; CDM ±500 V.

## Recommended operating conditions

SLVSES3A, p. 4, §6.3.

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | 3.0 | | 17 | V |
| VOUT | 0.4 | | 5.5 | V |
| Effective input capacitance | 3 | 10 | | µF |
| Effective output capacitance, 2.5 MHz | 10 | 22 | 100 | µF |
| Effective output capacitance, 1.0 MHz | 6 | 22 | 50 | µF |
| IOUT | 0 | | 3 | A |
| PG sink current | | | 1 | mA |
| TJ (lifetime derated above 125 °C) | −40 | | 150 | °C |

Thermal (SLVSES3A, p. 5, §6.4): RθJA 97.2 °C/W (JEDEC), 73.5 °C/W (TPS6290xEVM-069); RθJC(top) 74.4 °C/W; RθJB 25 °C/W; ΨJT 2.7 / 4.3 °C/W; ΨJB 24.7 / 28 °C/W.

## Power by mode

SLVSES3A, p. 5, §6.5 (typical at VIN 12 V, 25 °C).

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Quiescent, power-save mode | IOUT 0, not switching | 4 | | µA |
| Quiescent, PWM | VIN 12 V, VOUT 1.2 V, IOUT 0, switching | 8 | | mA |
| Shutdown | EN = 0 V | 0.27 | 3.5 | µA |

## Pinout and package

SLVSES3A, p. 3, Figure 5-1 and Table 5-1.

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | PG | O | Open-drain power good; needs a pull-up |
| 2 | SW | — | Switch node |
| 3 | VOS | I | Output voltage sense, to the output capacitor |
| 4 | GND | — | Ground |
| 5 | EN | I | Enable; never floating |
| 6 | VIN | I | Supply input |
| 7 | MODE/S-CONF | I | Mode and SmartConfig (Table 7-1); never floating |
| 8 | SS/TR | I | Soft-start capacitor or tracking; may float for the fastest start |
| 9 | FB/VSET | I | Divider feedback, or VSET resistor to GND (Table 7-2) |

Ordering (SLVSES3A, package option addendum, p. 46): TPS62903RPJR, 3000 per reel, Sn, MSL 2 at 260 °C (1 year), −40 to 150 °C, marking FN8.

## Recommended footprint

TI outline, example land pattern and stencil for RPJ0009A: SLVSES3A, pp. 43–45. Not transcribed here: **UNVERIFIED** until the footprint is drawn against those pages. Layout guidance: SLVSES3A, p. 40 (§10.1), example p. 40–41 (§10.2).

## Application circuit and required passives

SLVSES3A, p. 17, Figure 8-1 and Table 8-1; pp. 18–20:

| Ref | Value | Note |
|---|---|---|
| L | 1 µH (Coilcraft XGL4020-102 in Table 8-1) | Designed for a nominal 1 µH (§8.2.2.4) |
| CIN | 10 µF, 25 V, 0805 | 10 µF nominal recommended (§8.2.2.5.2) |
| COUT | 22 µF, 10–16 V, 0805 | 22 µF recommended; observe DC-bias derating at high VOUT (§8.2.2.5.1) |
| CSS | per soft-start time | ISS 2.5 µA (p. 6) |
| R1, R2 | external divider, or none in VSET mode | R1 = R2 × (VOUT / 0.6 V − 1), R2 ≤ 400 kΩ (Eq. 10, p. 18) |
| R3 | MODE/S-CONF setting | Table 7-1 |

- **LC combinations** (SLVSES3A, p. 18, Table 8-3): 1 µH with 22 µF is the 2.5 MHz standard; 2.2 µH with 22 µF the 1.0 MHz standard; 1–2.2 µH with 10–100 µF allowed (≥ 10 mΩ ESR above 100 µF).
- **Inductor** (SLVSES3A, p. 19, Eq. 11–12, Table 8-4): IL(max) = IOUT(max) + ΔIL(max) / 2 with ΔIL(max) = VOUT × (1 − VOUT / VIN(max)) / (L(min) × fSW); about 20 % margin over IL(max). Listed: Coilcraft XGL4020-102ME (8.8 A), Murata DFE252012F-1R0M (4.7 A), Samsung CIGT252010TM1R0MLE (5.3 A), TDK TFM252010ALM-1R0MTAA (4.7 A), Coilcraft XEL5030-222ME (9.7 A), XGL4020-222ME (6.2 A); currents are Isat at 30 % drop.
- **VSET settings used in the T1** (SLVSES3A, p. 11, Table 7-2): 95.3 kΩ → 5.1 V; 249 kΩ or open → 3.3 V. MODE/S-CONF 26.1 kΩ (p. 10, Table 7-1): VSET operation, 2.5 MHz, output discharge on, auto PFM/PWM with AEE. E96 resistors, 1 %, ≤ ±200 ppm/°C; at most 30 pF on the S-CONF/VSET pins.

## Interfaces and timing

- EN (precise enable): VIH 0.97 / 1.0 / 1.03 V, VIL 0.87 / 0.9 / 0.93 V, 0.5 MΩ internal pull-down when low (SLVSES3A, p. 5). MODE/S-CONF VIH 1.0 V.
- UVLO 2.85 / 2.925 / 3.0 V rising, 2.7 / 2.775 / 2.85 V falling (p. 5).
- Power good 93.5 / 96 / 99 % rising, 88.5 / 93 / 96 % falling of VFB nominal; VOL 0.4 V at 1 mA; 32 µs delay (p. 5).
- Current limit: high side 4.0 / 4.6 / 5.5 A, low side 4.0 / 4.4 / 5.0 A, low-side sink 1.3 / 1.7 / 2.5 A (p. 5). Dynamic peak = ILIMH + (VIN − VOUT) / L × 50 ns (p. 13, Eq. 1–2).
- RDS(on) 62 / 111 mΩ high side, 22 / 40 mΩ low side at VIN > 4 V (p. 5).
- Start-up delay 600 / 1400 µs (divider) or 650 / 1850 µs (VSET); soft start 150 / 200 µs with SS/TR open (p. 6).
- VSET output accuracy ±0.9 % at 25 °C, ±1.25 % over −40 to 150 °C (p. 6). Active discharge 7.5 / 20 Ω (p. 6).
- Thermal shutdown 170 °C, 20 °C hysteresis (p. 5).

## Linux driver

None. `regulator-fixed` with an enable GPIO (HAT_3V3: `HAT3V3_EN`; 5.1 V: `HAT5V_EN` OR `USB_SRC_ON`, board BOM line 91).

## Simulation models

The datasheet names TI WEBENCH (p. 17); PSpice or TINA models on ti.com were not checked: **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **Why a buck (board ADR 0014):** with a 2S VSYS (6.0–8.8 V) the 5.1 V output sits below the input, so the TPS61089 boost cannot work and the TLV62569 (5.5 V maximum input) cannot sit on VSYS. One TPS62903 part number covers both rails (55 % and 33 % of 3 A in the ADR's wording; 53 % and 33 % at the 1.6 A and 1.0 A design loads).
- **5.1 V margins (BRD-049):** 1.6 A design = 53 %; both eFuses at their 1.66 A ceilings (3.3 A, a software fault) are bounded by the 4.0 A minimum high-side limit. 100 % mode holds 5.1 V at 1.6 A down to VIN ≈ 5.1 + 1.6 × (0.111 + 0.009) = 5.29 V, below the 6.0 V VSYS minimum.
- **Inductor (lines 7, 92):** XGL4020-102MEC (8.8 A Isat at 30 % drop); peak 2.14 A at 1.6 A out and 1.67 A at the 1.15 A HAT_3V3 ceiling; the ≈ 5.7 A worst dynamic limit stays below 8.8 A, so a short does not saturate it.
- **Thermal:** ≈ 0.6 W loss at 8.16 W out (η 0.93, est.) → ≈ +44 °C at the EVM's 73.5 °C/W. Check in the board thermal model (board BOM §7 item 24).
- **Output capacitance at 5.1 V (board BOM v1.6 line 121):** one 22 µF with ≥ 12 µF effective at 5.1 V ([boost and MaskROM simulation](https://github.com/opendap-project/board/blob/main/docs/research/2026-10-boost-and-maskrom-simulation.md) §3.4): Murata GRM32ER71E226KE15L (25 V X7R 1210), effective value on Murata's DC-bias curve **UNVERIFIED**. A 22 µF 0805 sits near the 10 µF minimum of p. 4 at 5.1 V (est.). Phase margin at VSYS 6.0 V ≈ 38–40° (generic model corrected against TI's TPS62136 model, est.): a bench Bode plot is required (board BOM §7 item 27).
- **Shutdown:** the output does not follow VIN when disabled (unlike the TPS61089 boost); the eFuses still isolate the HAT and USB-C outputs.

## Sources

- TI, TPS62903 datasheet, SLVSES3A (March 2021): <https://www.ti.com/lit/ds/symlink/tps62903.pdf>
- OpenDAP board ADR 0014 and BOM v1.5, lines 7, 38, 91–92, 115; power tree v0 §2, §4.6, §4.10; board 2S battery study §4.2, §4.4 (`public/board/docs/`).
