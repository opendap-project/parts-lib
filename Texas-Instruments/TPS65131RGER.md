# TPS65131RGER

- **Manufacturer:** Texas Instruments
- **Function:** Dual-output DC-DC converter: boost for the positive output, inverting buck-boost for the negative output
- **BOM v1 lines:** 22 (HP-amp pre-rails ±7.0 V; v1.3: ±6.0 → ±7.0 V, ADR 0012), quantity 1; inductors on line 23, rectifiers on line 24, feedback and output network on line 111
- **Package:** VQFN-24 (RGE), 4 × 4 mm, exposed thermal pad
- **Datasheet:** *TPS6513x Dual, Positive and Negative Output DC-DC Converter*, SLVS493E, March 2004, revised April 2022. Cited below as "SLVS493E". File sha256 `e8360b9509047317416cfd9163a09d8cdf5c8accbd4e702ad6a43292ef48e0ed` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The TPS65131 is a dual-output DC-DC converter: a boost converter for a positive output (VPOS, up to 15 V) and an inverting buck-boost converter for a negative output (VNEG, down to −15 V), from a 2.7 V to 5.5 V input, with 2 A (typ. 1.95 A) switch current limits on the TPS65131 option, separate enables and separate power-save controls per output (SLVS493E, p. 1). In the T1 it makes the AUDIO_P7V0 / AUDIO_N7V0 pre-rails (+7.0 V / −7.0 V) from VSYS, which feed the LT3045 (+6.04 V) and LT3094 (−6.04 V) headphone-amplifier LDOs (BOM v1 line 22, v1.3; power tree v0 §2 and §4.2).

## Absolute maximum ratings

SLVS493E, p. 4, §6.1. All voltages to network ground.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN, INN input voltage | −0.3 | 6 | V |
| VPOS | −0.3 | 17 | V |
| VNEG | −17 | VIN + 0.3 | V |
| ENN, ENP, FBP, FBN, CN, CP, PSP, PSN, BSW | −0.3 | VIN + 0.3 | V |
| INP | −0.3 | 17 | V |
| OUTN to INN differential | −0.3 | 24 | V |
| Operating virtual junction temperature TJ | −40 | 150 | °C |
| Storage temperature | −65 | 150 | °C |

ESD (SLVS493E, p. 4, §6.2): HBM ±1000 V; CDM ±750 V.

## Recommended operating conditions

SLVS493E, p. 4, §6.3.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| Input voltage VIN, VINN | 2.7 | 5.5 | V |
| VPOS (boost output) | VI + 0.5 | 15 | V |
| VNEG (inverting output) | −15 | −2 | V |
| ENN, ENP | 0 | 5.5 | V |
| PSN, PSP | 0 | 5.5 | V |
| Ambient TA | −40 | 85 | °C |
| Junction TJ | −40 | 125 | °C |

Thermal (SLVS493E, p. 5, §6.4): RθJA 34.1 °C/W, RθJB 12.2 °C/W, RθJC(bot) 2.8 °C/W.

## Power by mode

SLVS493E, p. 5, §6.5, VIN = 3.6 V, TJ = 25 °C typical.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown (ENN = ENP = GND) | ISD into VIN | 0.2 | 1.5 | µA |
| Quiescent, no load, into VIN | ENP = ENN = PSP = PSN = VIN, VPOS = 8 V, VNEG = −5 V | 300 | 500 | µA |
| Quiescent, into VPOS | same | 100 | 120 | µA |
| Quiescent, into VNEG | same | 100 | 120 | µA |

- Power-save mode (PSP / PSN high): pulse skipping at light load, per converter (SLVS493E, p. 10, §7.4.1). PSx low forces continuous PWM.
- Between VUVLO and 2.7 V the device keeps operating without guaranteed performance; below VUVLO (2.1 / 2.35 / 2.7 V min/typ/max) both converters are off (SLVS493E, p. 5 and p. 10, §7.4.3–7.4.4).
- Efficiency: up to 89 % (boost) and 81 % (inverter); combined up to 85 % (SLVS493E, p. 1). Efficiency at the T1 operating point (VIN = VSYS 3.4–4.4 V, power tree v0 §3; v1.3: ±7 V, about 13 mA idle to 275 mA per rail, power tree v0 §3, §4.1) is **UNVERIFIED**; power tree v0 §4.11 assumes 0.8 at 275 mA (est.).

## Pinout and package

VQFN-24 (RGE), 4 mm × 4 mm, exposed thermal pad (pad 25) (SLVS493E, p. 3, Figure 5-1 and Table 5-1; p. 36, RGE0024B).

| Pin | Name | Function |
|---|---|---|
| 1, 24 | INP | Boost converter switch input |
| 2, 3 | PGND | Power ground |
| 4 | VIN | Control supply input |
| 5, 6 | INN | Inverting converter switch input |
| 7 | BSW | Gate control for an external P-channel battery switch; goes low when ENP is high |
| 8 | ENP | Enable, positive output |
| 9 | PSP | Power-save enable, boost |
| 10 | ENN | Enable, negative output |
| 11 | PSN | Power-save enable, inverter |
| 12, 20 | NC | Not connected |
| 13, 14 | OUTN | Inverting converter switch output |
| 15 | VNEG | Negative output sense |
| 16 | FBN | Negative feedback |
| 17 | VREF | Reference output; bypass with 220 nF; lower resistor of the negative divider connects here |
| 18 | CN | Compensation, inverter |
| 19 | AGND | Analog ground |
| 21 | CP | Compensation, boost |
| 22 | FBP | Positive feedback |
| 23 | VPOS | Positive output sense |
| 25 | Thermal pad | Solder to PGND plane |

Package body 3.9–4.1 mm square, 1 mm max height, 0.5 mm pitch, exposed pad 2.45 ± 0.1 mm (SLVS493E, p. 36, drawing 4219013/A). MSL Level-2-260C-1 YEAR, NiPdAu finish (SLVS493E, p. 30, package option addendum).

## Recommended footprint

SLVS493E, p. 37 (example board layout) and p. 38 (stencil), drawing 4219013/A 05/2017.

- 24 pads 0.6 mm × 0.25 mm at 0.5 mm pitch; pad row span (3.8 mm) both axes.
- Exposed pad (2.45 mm) square, optional 0.2 mm vias; vias under paste filled, plugged or tented.
- Non-solder-mask-defined pads preferred; 0.07 mm mask clearance.
- Stencil 0.125 mm: four 1.08 mm square apertures on the exposed pad, 78 % paste coverage.

## Application circuit and required passives

Typical application (SLVS493E, p. 11, Figure 8-1; p. 12, Tables 8-1 and 8-2):

| Ref | Function | Datasheet value |
|---|---|---|
| C1, C2 | INP / INN input capacitors | 4.7 µF, 6.3 V, X5R (≥ 4.7 µF recommended, p. 14, §8.2.2.3.1) |
| C3 | VIN bypass | 0.1 µF, 10 V, X5R |
| C4, C5 | VPOS / VNEG output | 4 × 4.7 µF, 25 V, X7R each (22 µF in Figure 8-1) |
| C6 | CP compensation | 10 nF, 16 V, X7R (p. 15, §8.2.2.6.2) |
| C7 | CN compensation | 4.7 nF, 50 V, C0G |
| C8 | VREF bypass | 220 nF, 6.3 V, X5R |
| C9, C10 | Feed-forward across R1 / R3 | 6.8 pF / 7.5 pF for the 10.5 V / −10 V example |
| R1/R2 | Positive divider | VPOS = VREF × (1 + R1/R2); R2 < 200 kΩ (p. 12–13, Eq. 1) |
| R3/R4 | Negative divider, referenced to VREF | VNEG = −VREF × R3/R4; R4 < 200 kΩ (p. 13, Eq. 2) |
| R7 | VIN filter resistor | 100 Ω |
| L1, L2 | Inductors | 4.7 µH typical; the device is optimised for 3.3–6.8 µH (p. 14, §8.2.2.2) |
| D1, D2 | Rectifiers | Schottky, 1 A, 20 V (onsemi MBRM120 in the example) |
| Q1 | Optional input disconnect PMOS on BSW | Vishay Si2323DS in the example; leave BSW floating if unused (p. 15, §8.2.2.5) |

- VREF = 1.213 V typ (1.2–1.225 V), FBP regulation 1.189–1.237 V, FBN 0 ± 0.024 V, total DC accuracy 3 % (SLVS493E, p. 5).
- An RC or LC filter between INN and VIN is recommended (SLVS493E, p. 15, §8.2.3).
- A 10–100 kΩ resistor in series with each feed-forward capacitor limits noise coupled into the loop (SLVS493E, p. 15, §8.2.2.6.1).
- Peak inductor current estimate: IL_P = VPOS × IPOS / (VI × 0.64); IL_N = (VI + |VNEG|) × INEG / (VI × 0.64) (SLVS493E, p. 13, Eq. 3–4).

T1 divider values (v1.3, BOM line 111): R1 475 kΩ / R2 100 kΩ gives VPOS = 1.213 V × (1 + 4.75) = 6.97 V; R3 576 kΩ / R4 100 kΩ gives VNEG = −1.213 V × 5.76 = −6.99 V (Eq. 1–2). Feed-forward C9 = 6.8 µs / R1 = 14.3 pF (15 pF used) and C10 = 7.5 µs / R3 = 13.0 pF (13 pF) (p. 15, Eq. 11–12).

## Interfaces and timing

- ENP, ENN, PSP, PSN: VIH ≥ 1.4 V, VIL ≤ 0.4 V, input current 0.01 µA typ, 0.1 µA max (SLVS493E, p. 5). All four may be driven from 1.8 V logic by these thresholds.
- Switching frequency 1.25 MHz min, 1.38 MHz typ (SLVS493E, p. 6, §6.6). Duty cycle 12.5 % to 87.5 % (p. 6).
- Soft-start: the switch current limit ramps to its nominal value in about 1 ms after enable (SLVS493E, p. 9, §7.3.5).
- Overvoltage protection: a converter shuts down when its feedback exceeds nominal by typically 5 % (SLVS493E, p. 9, §7.3.6).
- Thermal shutdown 150 °C, 5 °C hysteresis (SLVS493E, p. 6).
- Switch current limit, TPS65131: 1.8 / 1.95 / 2.2 A (boost and inverter) (SLVS493E, p. 5).
- Maximum output current is given only as curves vs input voltage (SLVS493E, p. 6–7, Figure 6-2 and Figure 6-4).

## Linux driver

None. The converter has no digital interface; ENP/ENN and PSP/PSN are GPIO-controlled. The rails can be described with the mainline `regulator-fixed` binding gated by a GPIO (`HPA_RAIL_EN`) (BOM v1 line 22: driver path *none*).

## Simulation models

- The datasheet's Device Support section (SLVS493E, p. 28, §10.1) names no model or EVM.
- PSpice, TINA-TI or WEBENCH models on ti.com: **UNVERIFIED**.
- No manifest entry beyond the datasheet.

## Design notes for the T1

- VSYS must stay ≤ 5.5 V at VIN (recommended maximum) and VPOS ≥ VIN + 0.5 V (SLVS493E, p. 4). With VPOS = +7.0 V the input must not exceed 5.5 V; check any VSYS state above that (USB-C input path) before release.
- **Load (v1.3):** 275 mA per rail worst continuous (full-scale sine into balanced 32 Ω, both channels; power tree v0 §4.1). By Eq. 3–4 the inverter peak inductor current is 1.29–1.43 A at VIN 3.5–3.0 V, **72–79 %** of the 1.8 A minimum switch limit; the boost is at 0.86–1.00 A, 48–56 % (BOM line 22; power tree v0 §4.10.1). Figure 6-4 (typical, 25 °C) gives about 340 mA at VIN 3.0 V and about 480 mA at 3.5 V at −7 V (interpolated between the −4 V and −10 V curves). ADR 0012 makes this **conditional on a WEBENCH or SPICE check** at VIN 3.0 V, ±7 V, 275 mA per rail before layout freeze.
- **Output capacitors (v1.3):** for 10 mV ripple at 275 mA and VIN 3.0 V, Eq. 7–8 give at least 12.6 µF (boost) and 15.4 µF (inverter) effective (BOM line 111). The datasheet's 4 × 4.7 µF 25 V X7R per output is kept; its effective value after DC-bias derating at 7 V is **UNVERIFIED**.
- **Compensation and reference (v1.3, line 111):** CP 10 nF, CN 4.7 nF C0G, VREF 220 nF, as in the datasheet example (§8.2.2.6.2).
- ENP and ENN are driven together from `HPA_RAIL_EN`; the LT3045 and LT3094 are enabled afterwards by `HPA_LDO_EN`, so the ±6 V outputs ramp on the LDO soft-starts (power tree v0 §6.2).
- Power-save mode (PSP = PSN = high) can stay enabled during playback per the power tree v0 §4.2 analysis; to be verified by measurement.
- The T1 rectifiers are Nexperia PMEG2010AEH (BOM line 24) instead of the datasheet's MBRM120, and the inductors are Murata DFE252012F-4R7M (BOM line 23). v1.3: the 2.2 A maximum switch limit exceeds the inductors' 2.1 A (ΔL/L −30 %) rating, so an overload runs them at about −30 % inductance (BOM line 23, D31).
- BSW and the input PMOS: not used in the BOM; leave BSW floating unless an input disconnect is added (SLVS493E, p. 15).
- Layout: inputs, outputs, inductors and diodes close to the IC, wide PGND plane, AGND tied to PGND, thermal pad to PGND, dividers close to FBP / VREF (SLVS493E, p. 26, §9.1).

## Sources

- TI, TPS6513x datasheet, SLVS493E (April 2022): <https://www.ti.com/lit/ds/symlink/tps65131.pdf>
- OpenDAP board BOM v1 (v1.3), lines 22–24 and 111, Changes in v1.3 items 3–4; power tree v0 §2, §4.1, §4.2, §4.10.1, §6.2 (`public/board/docs/specs/`).
