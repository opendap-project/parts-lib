# LT3045EDD#TRPBF

- **Manufacturer:** Analog Devices (Linear Technology)
- **Function:** 20 V, 500 mA ultralow-noise, ultrahigh-PSRR positive linear regulator, output set by one resistor on a 100 µA SET current
- **BOM v1 lines:** none placed. Proposed in BOM v1.2 (change 8, line 25, §7 item 13) as the replacement for the +5.0 V HP-amp LDO (TPS7A4901DGNR), paired with the [LT3094EDD#TRPBF](LT3094EDD-TRPBF.md) on line 26; listed as the line 25 second source
- **Package:** 10-lead DFN (DD), 3 mm × 3 mm, 0.5 mm pitch, 0.75 mm height, exposed pad = GND
- **Datasheet:** *LT3045 20V, 500mA, Ultralow Noise, Ultrahigh PSRR Linear Regulator*, Rev. D, 11/22. Cited below as "LT3045 Rev. D". Obtained from the LCSC datasheet mirror; analog.com did not answer from this host.
- **Status:** Partly UNVERIFIED. Not in the current BOM (proposed alternative, BOM v1.2 change 8, pending the maintainers' confirmation).

## Summary

The LT3045 is a precision 100 µA current reference followed by a unity-gain rail-to-rail buffer: VOUT = ISET × RSET, so noise, PSRR and bandwidth do not change with the programmed output voltage (LT3045 Rev. D, p. 1; p. 15). Headline figures: 0.8 µVrms (10 Hz–100 kHz) with CSET = 4.7 µF, 2 nV/√Hz at 10 kHz, 76 dB PSRR at 1 MHz, 500 mA, 260 mV typical dropout at 500 mA, 2.2 mA quiescent current, < 1 µA in shutdown, 1.8 V to 20 V input, 0 V to 15 V output, minimum 10 µF ceramic output capacitor, programmable current limit and power good (p. 1). LT3045EDD#TRPBF is the E-grade DFN-10 on tape and reel, marking LGYP, −40 °C to 125 °C (p. 2, Order Information). BOM v1.2 proposes it for HPA_P5V0 (+5.0 V from the TPS65131 +6.0 V pre-rail) because the worst continuous sine load of 122 mA is 81 % of the TPS7A4901's 150 mA (BOM v1 line 25; power tree v0 §4.1, §4.10).

## Absolute maximum ratings

LT3045 Rev. D, p. 2 (Note 1).

| Parameter | Rating |
|---|---|
| IN pin voltage | ±22 V |
| EN/UV pin voltage | ±22 V |
| IN-to-EN/UV, IN-to-OUT, IN-to-OUTS differential | ±22 V |
| PG, PGFB pin voltage | −0.3 V, 22 V |
| ILIM pin voltage | −0.3 V, 1 V |
| SET, OUTS, OUT pin voltage | −0.3 V, 16 V |
| SET, OUTS pin current | ±20 mA |
| OUT-to-OUTS differential | ±1.2 V |
| Output short-circuit duration | Indefinite |
| Operating junction, E- and I-grade | −40 °C to 125 °C |
| Storage | −65 °C to 150 °C |

- Parasitic diodes exist from ILIM, PG, PGFB, SET, OUTS and OUT to GND: do not drive them more than 0.3 V below GND (p. 5, Note 10).
- ESD ratings are not given in the document: **UNVERIFIED**.

## Recommended operating conditions

LT3045 Rev. D, p. 3, Electrical Characteristics, full temperature range unless noted.

| Parameter | Min | Typ | Max | Unit |
|---|---|---|---|---|
| Input voltage range | 2 | | 20 | V |
| Minimum IN voltage (UVLO rising), 500 mA | | 1.78 | 2 | V |
| Output voltage range (VIN > VOUT) | 0 | | 15 | V |
| SET pin current, full range (Note 3) | 98 | 100 | 102 | µA |
| SET pin current, 25 °C | 99 | 100 | 101 | µA |
| Output offset VOUT − VSET, full range | −2 | | 2 | mV |
| Minimum load, VOUT < 1 V | | | 10 | µA |

- Output capacitor: ≥ 10 µF, ESR < 20 mΩ, ESL < 2 nH (p. 13; p. 16).
- Input capacitor: ≥ 4.7 µF low-ESR ceramic (p. 18).
- Thermal (DD): θJA 34 °C/W, θJC 5.5 °C/W, TJMAX 150 °C (p. 2); measured 34–36 °C/W on a 4-layer board depending on top copper area (p. 22, Table 3).
- Internal current limit folds back for VIN − VOUT > 12 V (p. 4, Notes 3, 12).

## Power by mode

LT3045 Rev. D, p. 3–4.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | VEN/UV = 0 V, VIN = 6 V, 25 °C | 0.3 | 1 | µA |
| Shutdown | TJ ≤ 125 °C (E/I) | | 10 | µA |
| GND pin current | ILOAD = 10 µA | 2.2 | | mA |
| GND pin current, VIN = VOUT(NOM) (dropout, worst case) | ILOAD = 1 mA | 2.4 | 4 | mA |
| | ILOAD = 50 mA | 3.5 | 5.5 | mA |
| | ILOAD = 100 mA | 4.3 | 7 | mA |
| | ILOAD = 500 mA | 15 | 25 | mA |

GND pin current is tested in dropout and decreases at higher input voltage; it excludes the SET and ILIM currents, which the quiescent current includes (p. 4, Note 6). Dissipation: IOUT × (VIN − VOUT) + IGND × VIN (p. 22).

## Pinout and package

DD package, 10-lead DFN 3 × 3 mm (LT3045 Rev. D, p. 2; pin functions p. 12–13).

| Pin | Name | Function |
|---|---|---|
| 1, 2 | IN | Input; bypass capacitor required; withstands reverse input (acts as a series diode) |
| 3 | EN/UV | Enable / UVLO, 1.24 V rising threshold, 130 mV hysteresis; may be driven above VIN; do not float |
| 4 | PG | Open-collector power good; low while PGFB < 300 mV; float if unused |
| 5 | ILIM | Current-limit programming resistor to GND (150 mA·kΩ); sources 1:500 of IOUT (current monitor, 0–300 mV); tie to GND if unused |
| 6 | PGFB | Power-good feedback, 300 mV threshold; also enables fast start-up; tie to IN if unused |
| 7 | SET | Error-amplifier inverting input; sources 100 µA into RSET; CSET to GND lowers noise |
| 8 | GND | Ground |
| 9 | OUTS | Output sense; Kelvin to COUT and the load |
| 10 | OUT | Output; ≥ 10 µF, ESR < 20 mΩ, ESL < 2 nH |
| 11 (EP) | GND | Exposed pad, must be soldered to the PCB ground |

Package drawing (p. 29, LTC DWG 05-08-1699 Rev C): body 3.00 ± 0.10 mm, height 0.75 ± 0.05 mm, pitch 0.50 mm, lead width 0.25 ± 0.05 mm, exposed pad 1.65 × 2.38 mm.

## Recommended footprint

LT3045 Rev. D, p. 29, recommended solder pad pitch and dimensions: 0.50 mm pitch, pad width 0.25 ± 0.05 mm, pad length 0.70 ± 0.05 mm, outer extent 3.55 ± 0.05 mm, centre pad 1.65 ± 0.05 × 2.38 ± 0.05 mm. Recommended DFN layout: p. 21, Figure 8 (DC2491A demo board); guard ring around SET: p. 16, Figure 2. Thermal vias under the pad: not specified (**UNVERIFIED**).

## Application circuit and required passives

Basic adjustable regulator (LT3045 Rev. D, p. 15, Figure 1):

| Ref | Value | Note |
|---|---|---|
| RSET | 49.9 kΩ for 5.0 V | Table 1, p. 15; precision resistor; leakage of 100 nA at SET is a 0.1 % error (p. 16) |
| CSET | 0.47–4.7 µF typical, ≤ 22 µF | Low-leakage, non-piezoelectric preferred (p. 18–19); 10 nF minimum to avoid coupling into SET (p. 16); max 22 µF (p. 23) |
| COUT | ≥ 10 µF ceramic, X5R/X7R | ESR < 20 mΩ, ESL < 2 nH; larger values add little (p. 16–17) |
| CIN | ≥ 4.7 µF ceramic | Low ESR; more for long leads (p. 18) |
| RILIM | 150 mA·kΩ / ILIM | Optional; tie ILIM to GND if unused (p. 20) |
| RPG1, RPG2 | VPG = 0.3 V × (1 + RPG2/RPG1) − IPGFB × RPG2 | Optional (p. 20) |

- Soft-start: tSS ≈ 2.3 × RSET × CSET from 0 to 90 % of VOUT, fast start-up disabled (p. 19).
- Fast start-up: about 2 mA into SET while PGFB < 300 mV (p. 19; p. 3: 2 mA typ). Tie PGFB to IN or OUT to disable it, which also disables power good (p. 20).
- UVLO divider: VIN(UVLO) = 1.24 V × (1 + REN2/REN1) + IEN × REN2 (p. 20).
- PSRR depends on layout: switching current in the input capacitor can degrade PSRR by over 30 dB at 1 MHz; follow the demo-board layout (p. 18–19). A ferrite bead or short trace before IN filters spikes beyond the regulator bandwidth (p. 19).

## Interfaces and timing

LT3045 Rev. D, p. 3–4 unless noted.

- Dropout (1 % out of regulation): 1 mA / 50 mA: 220 typ, 275 max (25 °C), 330 mV max (full range); 300 mA: 220 typ, 280 max, 350 mV max (full range); 500 mA: 260 typ, 350 max, 450 mV max (full range). Typical dropout curve (p. 6, G14): about 215 mV at 25 °C, flat from 0 to about 350 mA (read from the curve).
- Output RMS noise, 10 Hz–100 kHz, 500 mA, COUT 10 µF: 0.8 µVrms with CSET 4.7 µF (1.3 V ≤ VOUT ≤ 15 V); 2.5 µVrms with CSET 0.47 µF at 3.3 V.
- Noise density, 500 mA: 2 nV/√Hz at 10 kHz (CSET 0.47 µF); 70 nV/√Hz at 10 Hz (CSET 4.7 µF).
- Ripple rejection, 1.3 V ≤ VOUT ≤ 15 V, VIN − VOUT = 2 V, 500 mA, COUT 10 µF: 117 dB at 120 Hz (CSET 4.7 µF); 90 dB at 10 kHz, 77 dB at 100 kHz, 76 dB at 1 MHz, 53 dB at 10 MHz (CSET 0.47 µF). No table value at 1 kHz; the curve (p. 9, G41, VIN 5 V, IL 500 mA) reads about 110 dB at 1 kHz.
- PSRR versus headroom (p. 10, G45, IL 500 mA, CSET 0.47 µF): about 65–75 dB from 100 kHz to 2 MHz at 1 V headroom, rising to about 80 dB at 2 V and above (read from the curve).
- Internal current limit: 570 / 710 / 850 mA at VIN = 2 V; 330 mA typ at VIN = 20 V (foldback). Programmable: 450 / 500 / 550 mA at RILIM = 300 Ω; 90 / 100 / 110 mA at 1.5 kΩ (p. 4).
- EN/UV: 1.18 / 1.24 / 1.32 V rising, 130 mV hysteresis.
- PGFB: 291 / 300 / 309 mV rising, 7 mV hysteresis; PG low 30 / 100 mV at 100 µA.
- Start-up, VOUT = 5 V, 500 mA, VIN = 6 V: 55 ms (CSET 0.47 µF), 550 ms (CSET 4.7 µF), 10 ms with fast start-up to 90 % (CSET 4.7 µF, RPG1 50 kΩ, RPG2 700 kΩ) (p. 4).
- Thermal shutdown 165 °C, 8 °C hysteresis (p. 4).
- Output overshoot recovery sink about 4 mA, disabled below VIN 2.5 V or VOUT 1.5 V (p. 20).

## Linux driver

None. A fixed regulator enabled by the HP-amp rail logic; in the device tree it would be a `regulator-fixed` supply like the TPS7A4901 it would replace (BOM v1 line 25: driver path *none*).

## Simulation models

- LTspice model: **UNVERIFIED** (not named in the datasheet text read here). Demo board DC2491A is named (p. 21).
- No manifest entry beyond the datasheet.

## Design notes for the T1

- **Not a drop-in.** The TPS7A4901DGNR on line 25 is an 8-pin MSOP with a feedback divider and a CNR/SS capacitor; the LT3045 is a DFN-10 programmed by RSET with CSET. Footprint, pinout and passives change.
- **Electrically it fits the +6 V → +5 V rail.** VIN 6 V is inside 2–20 V; 1 V headroom exceeds the 350 mV full-range maximum dropout at 300 mA, so it covers the 122 mA worst continuous sine (power tree v0 §4.1). 122 mA is 24 % of the 500 mA rating (BOM v1.2 change 8 states the same).
- **RSET = 49.9 kΩ** gives 5.0 V (Table 1). Accuracy is set by ISET ±2 % (full range) plus the RSET tolerance.
- **PSRR at the T1 headroom:** the 76 dB at 1 MHz is specified at VIN − VOUT = 2 V. At 1 V the curve G45 reads about 65–75 dB near the 1.25 MHz TPS65131 frequency; the power tree's PSRR budget (§4.2) should use the 1 V curve, or the pre-rail moves up. Layout governs it (p. 18–19).
- **Quiescent current:** 2.2 mA typ at no load, 4.3 mA typ at 100 mA (dropout, worst case), against about 0.8 mA at 100 mA for the TPS7A4901 (power tree v0 §4.2). BOM v1.2 estimates about 4 mA more for the LT3045/LT3094 pair; the datasheet typicals (2.2 + 2.35 mA at no load) agree in magnitude.
- **Soft-start match with the LT3094:** both use tSS ≈ 2.3 × RSET × CSET (LT3045 p. 19; LT3094 p. 22). Equal RSET (49.9 kΩ) and equal CSET give equal RC ramps. The ramp is RC-shaped, not linear like the TPS7A49/TPS7A30 pair; with CSET 4.7 µF it takes about 0.5 s (p. 4: 550 ms). Fast start-up currents differ (2 mA vs 1.8 mA typ), so fast start-up does not keep the ramps matched (**UNVERIFIED** in practice). The OPA1622 symmetric-ramp requirement (BOM v1 D3) must be re-checked with the chosen CSET.
- **EN/UV** at 1.24 V is driven by the 3.3 V `HPA_LDO_EN` net directly (power tree v0 §7).
- **Current limit:** RILIM can cap the output below the TPS65131's 200–500 mA capability (power tree v0 §4.2), e.g. 1 kΩ for 150 mA (p. 20). Value is a design choice for the maintainers.
- **Thermal:** 0.122 A × 1 V + about 4 mA × 6 V ≈ 0.15 W; × 35 °C/W ≈ 5 °C rise (calculation from p. 22 method).

## Sources

- Analog Devices, LT3045 datasheet, Rev. D (11/22), via the LCSC mirror: <https://datasheet.lcsc.com/datasheet/pdf/6b4c027fb90357baec1b8d318e11eacb.pdf>. Manufacturer URL (not reachable from this host): <https://www.analog.com/media/en/technical-documentation/data-sheets/lt3045.pdf>
- OpenDAP board BOM v1, v1.2 change 8, lines 25–26, §7 item 13; power tree v0 §4.1, §4.2, §4.10 (`public/board/docs/specs/`).
