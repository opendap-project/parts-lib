# TPS61089RNRR

- **Manufacturer:** Texas Instruments
- **Function:** 12.6 V, 7 A fully integrated synchronous boost converter, adjustable switching frequency and peak current limit, PFM at light load
- **BOM v1 lines:** 91 (HAT_5V / USB-C source 5.1 V boost from VSYS, qty 1; v1.1 replacement for the TPS61088RHLR); feeds eFuses #A and #C of line 44; inductor on line 92
- **BOM v1.5:** removed from line 91 by board ADR 0014 (a boost cannot run from a 2S VSYS); replaced by the [TPS62903RPJR](TPS62903RPJR.md) buck. Kept for traceability.
- **Package:** VQFN-HR 11 pins (RNR0011A), 2.0 × 2.5 mm nominal, 1 mm max height, 0.5 mm pitch
- **Datasheet:** *TPS61089x 12.6-V, 7-A Fully-Integrated Synchronous Boost Converters in 2.0-mm x 2.5-mm VQFN Package*, SLVSD38C, November 2015, revised August 2021. Cited below as "SLVSD38C"; "p. n" is the printed page, "PDF p. n" the addendum and drawing pages. File sha256 `863eda98cbb0853553e7cfd4f199027fcca5b80a5e0fb57448aeccabce061e0d` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The TPS61089 is a synchronous boost converter with a 19 mΩ main switch and a 27 mΩ rectifier switch, 2.7–12 V input, 4.5–12.6 V output, resistor-programmable peak current limit up to 10 A, switching frequency adjustable from 200 kHz to 2.2 MHz, 4 ms built-in soft start and 13.2 V output overvoltage protection (SLVSD38C, p. 1). It uses adaptive constant off-time peak current control with external loop compensation; the TPS61089 works in PFM at light load, the TPS610891 in forced PWM (SLVSD38C, p. 3, p. 9). TPS61089RNRR is the 3000-piece reel, active, marking ZGOI (SLVSD38C, PDF p. 26). In the T1 it boosts VSYS to 5.1 V for HAT_5V (eFuse #A) and the USB-C VBUS source (eFuse #C), because the BQ25895 OTG boost cannot run while charging; design output 1.6 A; EN from `HAT5V_EN` OR `USB_SRC_ON` (BOM v1.1 lines 44, 91; power tree v0 §2, §4.6).

## Absolute maximum ratings

SLVSD38C, p. 5, §7.1. Voltages to the network ground.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| BOOT | −0.3 | SW + 7 | V |
| VIN, SW, FSW, VOUT | −0.3 | 14.5 | V |
| EN, VCC, COMP | −0.3 | 7 | V |
| ILIM, FB | −0.3 | 3.6 | V |
| Operating junction TJ | −40 | 150 | °C |
| Storage Tstg | −65 | 150 | °C |

ESD (SLVSD38C, p. 5, §7.2): HBM ±2000 V; CDM ±500 V.

## Recommended operating conditions

SLVSD38C, p. 5, §7.3.

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | 2.7 | | 12 | V |
| VOUT | 4.5 | | 12.6 | V |
| L, effective | 0.47 | 2.2 | 10 | µH |
| CIN, effective | 10 | | | µF |
| CO, effective | 10 | 47 | 1000 | µF |
| TJ | −40 | | 125 | °C |

Thermal, RNR (SLVSD38C, p. 5, §7.4): RθJA 53.4 °C/W, RθJC(top) 59.2 °C/W, RθJB 9.6 °C/W, ψJT 0.5 °C/W, ψJB 9.5 °C/W, RθJC(bot) 0.7 °C/W; RθJA on the TI EVM (4-layer, 76 × 52 mm, 2 oz outer copper) 39.2 °C/W (pp. 5–6). Keep TJ ≤ 125 °C in normal operation; PD(max) = (125 − TA) / RθJA (SLVSD38C, p. 22, Eq. 20).

## Power by mode

SLVSD38C, p. 6, §7.5: VIN = 2.7–5.5 V, VOUT = 9 V, TJ −40 to 125 °C, typical at 25 °C.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown, into VIN | EN low, VIN 2.7–5.5 V, TJ ≤ 85 °C | 1 | 3 | µA |
| Quiescent, into VIN | enabled, no load, VFB = 1.3 V, VOUT = 12 V, TJ ≤ 85 °C | 1 | 3 | µA |
| Quiescent, into VOUT | same | 100 | 180 | µA |

- In PFM the TPS61089 keeps efficiency above 70 % down to 1 mA load, regulating VOUT 1 % above the nominal setting (SLVSD38C, p. 11, §8.4.1.2; p. 12, Figure 8-1).
- Efficiency curves (VOUT = 5 V among them, VIN = 3.6 V): SLVSD38C, p. 7, Figure 7-2. The T1 operating point (VIN 3.0–4.4 V, 5.1 V, 0.4–1.6 A) is read from curves only (**UNVERIFIED**; the power tree uses η = 0.88).
- In shutdown the input reaches VOUT through the body diode of the high-side rectifier FET (SLVSD38C, p. 10, §8.3.2): the boost does not disconnect the load.

## Pinout and package

RNR0011A, 11-pin VQFN-HR with large power pads, body 2.4–2.6 × 1.9–2.1 mm, 1 mm max height, 0.5 mm pitch (SLVSD38C, p. 1; PDF p. 29, drawing 4222143/A 08/2015).

| Pin | Name | I/O | Function |
|---|---|---|---|
| 1 | FSW | I | Switching frequency: resistor between FSW and SW; do not leave open |
| 2 | VCC | O | Internal regulator output; ceramic capacitor > 1.0 µF to ground |
| 3 | FB | I | Output voltage feedback |
| 4 | COMP | O | Error amplifier output; compensation network to GND |
| 5 | GND | PWR | Ground |
| 6 | VOUT | PWR | Boost output |
| 7 | EN | I | Enable, high = on; low = shutdown; 800 kΩ pulldown |
| 8 | ILIM | O | Peak current limit: resistor to GND |
| 9 | VIN | I | IC supply input |
| 10 | BOOT | O | High-side gate driver supply: capacitor to SW |
| 11 | SW | PWR | Switching node (low-side drain, high-side source) |

(SLVSD38C, p. 4, Figure 6-1 and Table 6-1; p. 6 for the EN pulldown.) Addendum: RoHS, Sn finish, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking ZGOI (PDF p. 26). Reel 180 mm, 8 mm tape, pin 1 in Q2 (PDF p. 27).

## Recommended footprint

RNR0011A example board layout (SLVSD38C, PDF p. 30) and stencil (PDF p. 31):

- Pins 1–4 and 7–10: 8 pads (0.55) × (0.25) mm, 0.5 mm pitch, two columns (2.35) mm apart centre to centre; non-solder-mask-defined, 0.05 mm max mask clearance.
- Pins 5 (GND) and 6 (VOUT): two long pads (0.35) mm wide, (0.7) mm apart; pin 11 (SW): (1) mm wide pad with a (0.2) mm via; pads 5, 6 and 11 are solder-mask-defined, 0.05 mm min mask overlap.
- Stencil 0.1 mm thick: 90 % printed coverage on pads 5 and 6, 79 % on pad 11 (split into openings).
- Note 3 (PDF p. 30): the package is designed to be soldered to a thermal pad on the board (TI SLUA271).

## Application circuit and required passives

Typical application, 3.0–4.35 V to 9 V / 2 A at 500 kHz (SLVSD38C, p. 13, Figure 9-1; Table 9-1):

| Ref | Example value | T1 note |
|---|---|---|
| L1 | 1.8 µH | XAL4020-152MEC, 1.5 µH (line 92) |
| C1 (CIN) | 22 µF | ≥ 10 µF effective (p. 5); plus 0.1 µF ceramic close to VIN (p. 16, §9.2.2.6) |
| C2 (CO) | 3 × 22 µF | 10–1000 µF effective, 47 µF nominal (p. 5); derate for DC bias (p. 16) |
| C3 (VCC) | 2.2 µF | > 1.0 µF required (p. 4, p. 16) |
| C4 (BOOT–SW) | 0.1 µF | same |
| R3 (RFREQ, FSW–SW) | 301 kΩ (500 kHz) | ≈ 147 kΩ for 1 MHz (calculation below) |
| R4 (RILIM) | 127 kΩ (8 A) | 200 kΩ (5.15 A typ, BOM line 91) |
| R1 / R2 (FB divider) | 681 kΩ / 107 kΩ (9 V) | 5.1 V: R1 ≈ 321 kΩ with R2 = 100 kΩ (calculation) |
| R5, C5, C6 (COMP) | 17.4 kΩ, 4.7 nF, C6 per Eq. 19 | to be calculated for the T1 L and CO (**UNVERIFIED**) |

Design equations (SLVSD38C, pp. 10, 14–18):

- Switching frequency (Eq. 1 / Eq. 3): RFREQ = 4 × (1/fSW − tDELAY × VOUT/VIN) / CFREQ, CFREQ = 24 pF, tDELAY = 86 ns. For 1 MHz and 5.1 V: 142 kΩ at VIN = 3.0 V, 147 kΩ at 3.7 V, 150 kΩ at 4.4 V (calculation). With a fixed resistor the frequency shifts slightly with VIN (quasi-constant frequency, p. 9). EC table: 500 kHz at 301 kΩ, 2000 kHz at 46.4 kΩ (p. 6).
- Peak current limit (Eq. 2 / Eq. 4): ILIM = 1,030,000 / RILIM; 8 A at 127 kΩ. At worst case the minimum limit can be 0.8 A below the calculated value (p. 14, §9.2.2.3). EC table at 127 kΩ: 7.3 / 8.1 / 8.9 A; at 100 kΩ: 9.0 / 10 / 11 A (p. 6). Figure 7-3 plots the limit for 100–400 kΩ (p. 7).
- Output voltage (Eq. 5): R1 = (VOUT − VREF) × R2 / VREF, R2 < 120 kΩ, ≥ 10 µA through the divider; VREF 1.188 / 1.212 / 1.236 V in PWM, 1.224 V typ in PFM (pp. 6, 15).
- Inductor (Eq. 6–8): IDC = VOUT × IOUT / (VIN × η); IPP = VIN × (VOUT − VIN) / (L × fSW × VOUT); ILpeak = IDC + IPP/2. TI recommends the minimum VIN, the minimum fSW, L − 30 % and a low η for the worst case, and an inductor whose saturation current is above the set current limit (pp. 15–16).
- Output ripple (Eq. 9–10), loop compensation (Eq. 11–19; equivalent sense resistance 0.08 Ω, GEA 190 µS; crossover below the lower of fSW/10 and fRHPZ/5; phase margin > 45°, gain margin > 10 dB) (pp. 17–19).
- Layout: short SW loop, input capacitor close to VIN and GND, output capacitor close to both VOUT and GND, ground plane under the device; solder SW, VOUT and GND pads to large copper with vias (pp. 22–23, Figure 11-1).

## Interfaces and timing

- EN: VEN_H 1.2 V max, VEN_L 0.4 V min; 800 kΩ internal pulldown (SLVSD38C, p. 6). Driven by 1.8 V or 3.3 V logic.
- Soft start 2 / 4 / 6 ms (COUT effective 47 µF, IOUT = 0), from EN high (SLVSD38C, p. 6; p. 10, §8.3.3).
- VIN UVLO: rising 2.7 V max, falling 2.4 / 2.5 V, hysteresis 200 mV (SLVSD38C, p. 6; p. 10, §8.3.1).
- VCC: 5.8 V typ at VIN = 8 V, ICC = 2 mA; VCC UVLO 2.1 V falling (SLVSD38C, p. 6).
- Output OVP: 12.7 / 13.2 / 13.6 V rising, 0.25 V hysteresis; switching stops until VOUT falls (SLVSD38C, pp. 6, 10–11).
- RDS(on) at VCC = 6 V: high side 27 / 44 mΩ, low side 19 / 31 mΩ (typ / max); minimum on time 90 / 180 ns (SLVSD38C, p. 6).
- Thermal shutdown 150 °C, 20 °C hysteresis (SLVSD38C, p. 6; p. 11 gives restart at about 130 °C).
- No I2C, no power-good output.

## Linux driver

None. The enable is the hardware OR of `HAT5V_EN` and `USB_SRC_ON` (BOM v1.1 line 91; BOM driver path *none*).

## Simulation models

- The Device and Documentation Support section (SLVSD38C, p. 24) points to WEBENCH Power Designer only; it names no SPICE model or EVM.
- PSpice/TINA models on ti.com: **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **BOM v1.1 claims checked against SLVSD38C.** VIN 2.7–12 V, VOUT 4.5–12.6 V, PFM at light load, 4 ms soft start (pp. 1, 5–6): agree. ILIM = 1,030,000 / RILIM, so 200 kΩ → 5.15 A typ (Eq. 2, p. 10): agrees. Shutdown current is 1 µA typ, 3 µA max at TJ ≤ 85 °C (p. 6): the BOM's "1 µA" is the typical figure. Not a load-disconnect boost (p. 10, §8.3.2): agrees. CIN ≥ 10 µF and CO ≥ 10 µF effective, 47 µF nominal (p. 5): agrees. 0.1 µF BOOT capacitor (p. 13, Figure 9-1): agrees. fSW set by RFREQ per Eq. 1: agrees; about 147 kΩ for 1 MHz at VIN = 3.7 V.
- **Disagreement, current-limit minimum.** The BOM and power tree derive 4.6–5.7 A from the ±10 % spread at 127 kΩ (7.3–8.9 A, p. 6). The datasheet states instead that the minimum limit can be 0.8 A below the calculated value (p. 14, §9.2.2.3), which gives 5.15 − 0.8 = 4.35 A at 200 kΩ. The 3.6 A design peak (BOM line 92) still sits below 4.35 A. No maximum is given at 200 kΩ; the BOM's 5.7 A upper figure is **UNVERIFIED** (the XAL4020-152 Isat of 7.1 A leaves margin above it either way).
- **Peak at the design point.** IDC = 5.1 × 1.6 / (3.0 × 0.88) = 3.1 A (Eq. 6). With 1.5 µH at 1 MHz the power tree computes 0.96 A ripple and a 3.6 A peak; Eq. 7 with L − 30 % (1.05 µH), as TI recommends, gives 1.18 A ripple and a 3.7 A peak (calculation). Both below 4.35 A.
- **Low battery.** VSYS follows VBAT on battery and can sit below 3.5 V; the boost runs down to its UVLO (2.4–2.5 V falling, p. 6). The 3.0 V worst case used in the BOM sizing is above it.
- **Load path in shutdown.** VOUT ≈ VIN − body diode while EN is low (p. 10). eFuses #A and #C must therefore stay off when the boost is idle, as the BOM states; the eFuse inputs see about VSYS during that time.
- **PFM and audio.** PFM bursts at light load lower the switching frequency (p. 11). The boost runs only while HAT_5V or the USB-C source is on; its effect on the audio rails is a layout and measurement item (**UNVERIFIED**). The forced-PWM TPS610891 is Product Preview only (p. 3).
- **Output setting.** The PFM regulation point is 1 % above nominal (p. 11): 5.1 V nominal becomes about 5.15 V at light load.
- **Thermal.** RθJA 53.4 °C/W (JEDEC) or 39.2 °C/W (TI EVM); conduction loss at the 3.1 A input is small with 19/27 mΩ switches, but the switching loss at 1 MHz is not tabulated: check with WEBENCH or measurement (**UNVERIFIED**).

## Sources

- TI, TPS61089x datasheet, SLVSD38C (August 2021; package addendum 31 October 2025): <https://www.ti.com/lit/ds/symlink/tps61089.pdf>
- OpenDAP board BOM v1.1, lines 44, 91, 92, §9 D18; power tree v0 §2, §4.6 (`public/board/docs/specs/`).
- [XAL4020-152MEC](../Coilcraft/XAL4020-152MEC.md) (inductor); [TPS61088RHLR](TPS61088RHLR.md) (replaced part).
