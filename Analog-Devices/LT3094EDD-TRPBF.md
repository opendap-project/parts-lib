# LT3094EDD#TRPBF

- **Manufacturer:** Analog Devices (Linear Technology)
- **Function:** −20 V, 500 mA ultralow-noise, ultrahigh-PSRR negative linear regulator, output set by one resistor on a 100 µA SET current
- **BOM v1 lines:** 26 (Audio, −6.0 V HP-amp LDO, HPA_N6V0), quantity 1, Proposed (v1.3: replaces the TPS7A3001DGNR, ADR 0012, D30; LT3094EDD#PBF, the same part in tube, is the listed alternative), paired with the [LT3045EDD#TRPBF](LT3045EDD-TRPBF.md) on line 25. Its RSET, RILIM and capacitors are on lines 109–110
- **Package:** 12-lead DFN (DD), 3 mm × 3 mm, 0.45 mm pitch, 0.75 mm height, exposed pad = IN
- **Datasheet:** *LT3094 −20V, 500mA, Ultralow Noise, Ultrahigh PSRR Negative Linear Regulator*, Rev. B, 01/20. Cited below as "LT3094 Rev. B". Obtained from the LCSC datasheet mirror; analog.com did not answer from this host.
- **Status:** Partly UNVERIFIED

## Summary

The LT3094 is the negative counterpart of the LT3045: a precision 100 µA SET current and a unity-gain error amplifier, so VOUT = ISET × RSET (negative) and noise, PSRR and bandwidth are independent of the output voltage (LT3094 Rev. B, p. 1; p. 15). Headline figures: 0.8 µVrms (10 Hz–100 kHz), 2.2 nV/√Hz at 10 kHz, 74 dB PSRR at 1 MHz, 500 mA, 235 mV typical dropout, 2.35 mA quiescent current, 3 µA in shutdown, −1.8 V to −20 V input, 0 V to −19.5 V output, bipolar enable, VIOC pin to track an upstream converter, minimum 10 µF ceramic output capacitor (p. 1). LT3094EDD#TRPBF is the E-grade DFN-12 on tape and reel, marking LHCC, −40 °C to 125 °C (p. 4). BOM v1.3 uses it for HPA_N6V0 (−6.04 V from the TPS65131 −7.0 V pre-rail), so both HP-amp LDOs share the same SET-pin soft-start law (BOM v1 lines 25–26, Changes in v1.3 item 3).

## Absolute maximum ratings

LT3094 Rev. B, p. 3 (Note 1).

| Parameter | With respect to GND | With respect to IN |
|---|---|---|
| IN pin voltage | −22 V, 0.3 V | — |
| EN/UV pin voltage | ±22 V | −0.3 V, 30 V |
| PG pin voltage | −0.3 V, 22 V | −0.3 V, 30 V |
| PGFB pin voltage | ±22 V | −0.3 V, 30 V |
| ILIM pin voltage | — | −0.3 V, 22 V |
| VIOC pin voltage | −2 V, 0.3 V | −0.3 V, 22 V |
| SET pin voltage | ±22 V | −0.3 V, 22 V |
| OUTS pin voltage | ±22 V | −0.3 V, 22 V |
| OUT pin voltage | ±22 V | −0.3 V, 22 V |

- SET and OUTS pin current ±10 mA; SET-to-OUTS and OUT-to-OUTS differential ±22 V; output short-circuit duration indefinite (p. 3).
- Operating junction: E- and I-grade −40 °C to 125 °C; storage −65 °C to 150 °C (p. 3).
- Parasitic diodes exist from every other pin to IN: do not drive them more than 0.3 V below IN (p. 6, Note 2).
- ESD ratings are not given in the document: **UNVERIFIED**.

## Recommended operating conditions

LT3094 Rev. B, p. 4–6, Electrical Characteristics.

| Parameter | Min | Typ | Max | Unit |
|---|---|---|---|---|
| Input voltage range, 500 mA | −20 | | −2.3 | V |
| Minimum IN voltage (UVLO rising), 500 mA | | −1.8 | −2.3 | V |
| Output voltage range | −19.5 | | 0 | V |
| SET pin current, full range (Note 7) | 98 | 100 | 102 | µA |
| SET pin current, 25 °C | 99 | 100 | 101 | µA |
| Output offset VOUT − VSET, full range | −2 | | 2 | mV |
| Minimum load, VOUT > −1.5 V | | | 10 | µA |

- Output capacitor: ≥ 10 µF, ESR < 30 mΩ, ESL < 1.5 nH (p. 15; p. 18).
- Input capacitor: ≥ 10 µF low-ESR ceramic (p. 15; p. 20).
- Thermal (DD): θJA 34 °C/W, θJC 5.5 °C/W, TJMAX 150 °C (p. 3).
- Internal current limit folds back for |VOUT − VIN| > 7 V (p. 6, Notes 7, 13, 14).

## Power by mode

LT3094 Rev. B, p. 4–5.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | VEN/UV = 0 V, VIN = −6 V, PG open, 25 °C | 3 | 8 | µA |
| Shutdown | full range | | 10 | µA |
| GND pin current | ILOAD = 10 µA | 2.35 | | mA |
| GND pin current, VIN = VOUT(NOM) (dropout, worst case) | ILOAD = 1 mA | 2.4 | 4 | mA |
| | ILOAD = 50 mA | 3.1 | 5.5 | mA |
| | ILOAD = 100 mA | 3.8 | 6.5 | mA |
| | ILOAD = 500 mA | 12 | 23 | mA |

GND pin current excludes the SET and ILIM currents, which the quiescent current includes (p. 6, Note 11).

## Pinout and package

DD package, 12-lead DFN 3 × 3 mm; same pin numbering as the MSE package (LT3094 Rev. B, p. 3; pin functions p. 15).

| Pin | Name | Function |
|---|---|---|
| 1, 2 | IN | Negative input; ≥ 10 µF bypass |
| 3 | EN/UV | Bipolar enable / UVLO: on above +1.26 V (200 mV hysteresis) or below −1.26 V (215 mV hysteresis); do not float |
| 4 | PG | Open-collector power good; low while PGFB is between 0 V and −300 mV; valid (low) in shutdown |
| 5 | PGFB | Power-good feedback, −300 mV threshold; also enables fast start-up; tie to IN if unused |
| 6 | ILIM | Current-limit programming resistor to GND (3.75 A·kΩ); do not float |
| 7 | VIOC | Tracking output to control an upstream converter; float if unused |
| 8 | SET | Error-amplifier inverting input; sinks 100 µA through RSET; CSET to GND lowers noise |
| 9 | GND | Ground |
| 10 | OUTS | Output sense; Kelvin to COUT and the load |
| 11, 12 | OUT | Output; ≥ 10 µF, ESR < 30 mΩ, ESL < 1.5 nH |
| 13 (EP) | IN | Exposed pad is IN, must be soldered to the PCB (p. 3) |

Package drawing (p. 31, LTC DWG 05-08-1725 Rev A): body 3.00 ± 0.10 mm, height 0.75 ± 0.05 mm, pitch 0.45 mm, lead width 0.23 ± 0.05 mm, exposed pad 1.65 × 2.38 mm.

## Recommended footprint

LT3094 Rev. B, p. 31, recommended solder pad pitch and dimensions: 0.45 mm pitch, pad width 0.25 ± 0.05 mm, pad length 0.70 ± 0.05 mm, outer extent 3.50 ± 0.05 mm, centre pad 1.65 ± 0.05 × 2.38 ± 0.05 mm; solder mask on areas not soldered. The centre pad is the IN net, not ground. Recommended layout: **UNVERIFIED** (not transcribed in this pass).

## Application circuit and required passives

Typical application (LT3094 Rev. B, p. 1):

| Ref | Value | Note |
|---|---|---|
| RSET | 49.9 kΩ for −5.0 V | Electrical Characteristics start-up condition uses 49.9 kΩ for VOUT(NOM) = −5 V (p. 6); VSET = ISET × RSET (p. 15) |
| CSET | 0.47–4.7 µF typical | Low leakage; larger lowers 1/f noise (p. 21–22) |
| COUT | ≥ 10 µF ceramic | ESR < 30 mΩ, ESL < 1.5 nH (p. 15) |
| CIN | ≥ 10 µF ceramic | Low ESR (p. 20) |
| RILIM | 3.75 A·kΩ / ILIM | 7.5 kΩ → 500 mA, 37.5 kΩ → 105 mA (p. 5) |
| RPG1, RPG2 | VPG = −0.3 V × (1 + RPG1/RPG2) − IPGFB × RPG1 | Optional (p. 15) |

- Soft-start: tSS ≈ 2.3 × RSET × CSET, fast start-up disabled (p. 22), the same law as the LT3045.
- Fast start-up: 1.8 mA typ SET current while PGFB is above −300 mV (p. 4).
- VIOC: outputs VIN − VOUT (or VIN + 1.5 V for VOUT between 0 and −1.5 V) to drive the feedback of an upstream switcher and keep the LDO headroom constant (p. 5, Note 15; p. 22–24).

## Interfaces and timing

LT3094 Rev. B, p. 4–6 unless noted.

- Dropout (1 % out of regulation): 1 mA / 50 mA: 185 typ, 225 max (25 °C), 275 mV max (full range); 100 mA: 185 typ, 230 max, 280 mV max (full range); 500 mA: 235 typ, 310 max, 410 mV max (full range). Typical dropout curve (p. 8, G14): about 180 mV at 25 °C from 0 to about 300 mA (read from the curve).
- Output RMS noise, 10 Hz–100 kHz, 500 mA, COUT 10 µF: 0.8 µVrms with CSET 4.7 µF (−19.5 V ≤ VOUT ≤ −1.5 V); 3 µVrms with CSET 0.47 µF at −3.3 V.
- Noise density, 500 mA: 2.2 nV/√Hz at 10 kHz (CSET 0.47 µF); 70 nV/√Hz at 10 Hz (CSET 4.7 µF).
- Ripple rejection, −18 V ≤ VOUT ≤ −1.5 V, VIN − VOUT = 2 V, 500 mA, COUT 10 µF: 108 dB at 120 Hz (CSET 4.7 µF); 94 dB at 10 kHz, 75 dB at 100 kHz, 74 dB at 1 MHz, 28 dB at 10 MHz (CSET 0.47 µF) (p. 5). No table value at 1 kHz; the curve (p. 11, G43, VIN −5 V, −500 mA, CSET 4.7 µF) reads about 107 dB at 1 kHz.
- PSRR versus headroom (p. 12, G47, −500 mA, CSET 0.47 µF): at 1 V headroom about 65 dB at 1 MHz and about 70 dB at 100 kHz and 2 MHz; about 70–76 dB at 2 V (read from the curve).
- Internal current limit: 550 mA min, 750 mA typ at VIN = −2.3 V; 425 mA typ at −12 V; 40 / 85 / 160 mA at −20 V (foldback). Programmable: 450 / 500 / 560 mA at 7.5 kΩ; 90 / 105 / 120 mA at 37.5 kΩ (p. 5).
- EN/UV: positive 1.20 / 1.26 / 1.35 V rising, 200 mV hysteresis; negative −1.33 / −1.26 / −1.20 V, 215 mV hysteresis. EN/UV current 8 µA typ at +1.5 V (p. 5).
- PGFB: 288 / 300 / 312 mV (magnitude), 7 mV hysteresis; PG low 17 / 50 mV at 100 µA (p. 5).
- Start-up, RSET 49.9 kΩ, VOUT = −5 V, 500 mA, VIN = −6 V: 55 ms (CSET 0.47 µF), 550 ms (CSET 4.7 µF), 10 ms with fast start-up to 90 % (p. 6).
- Thermal shutdown 167 °C, 8 °C hysteresis (p. 6).

## Linux driver

None. A fixed regulator enabled by the HP-amp rail logic, described as a `regulator-fixed` supply (BOM v1 line 26: driver path *none*).

## Simulation models

- LTspice model: **UNVERIFIED** (not named in the datasheet text read here).
- No manifest entry beyond the datasheet.

## Design notes for the T1

- **Replaces the TPS7A3001DGNR (v1.3).** The TPS7A3001 is an 8-pin MSOP with a divider and CNR/SS; the LT3094 is a DFN-12 programmed by RSET and CSET. Footprint, pinout and passives changed with it (BOM lines 26, 109–110).
- **Exposed pad is IN (−7.0 V), not GND.** The thermal copper under the part belongs to the AUDIO_N7V0 net; it cannot join the ground plane (BOM line 26).
- **Operating point:** −7.0 V in (TPS65131 AUDIO_N7V0), −6.04 V out, so about 0.96 V of headroom against the 280 mV (100 mA) and 410 mV (500 mA) full-range maximum dropout (power tree v0 §4.2). The worst continuous load of 275 mA (power tree v0 §4.1) is 55 % of the 500 mA rating (BOM line 26).
- **RSET = 60.4 kΩ, 0.1 %** (Yageo RT0603BRD0760K4L, BOM line 109): VOUT = −100 µA × 60.4 kΩ = −6.04 V (p. 15).
- **Current limit:** RILIM = 9.31 kΩ (Yageo RC0603FR-079K31L, line 109): 3.75 A·kΩ / 9.31 kΩ ≈ 403 mA (p. 5). ILIM must not float (p. 15). The spread is tabulated only at 7.5 kΩ (450 / 500 / 560 mA, −10 % / +12 %) and 37.5 kΩ (p. 5); BOM lines 26 and 109 assume ±10 % at 9.31 kΩ (≈ 360 mA minimum, est., **UNVERIFIED**); the +12 % upper spread at 7.5 kΩ would put the maximum near 450 mA (est.). 275 mA is 68 % of the programmed limit.
- **CSET = 0.47 µF** (line 110): 3 µVrms at −3.3 V with CSET 0.47 µF; 0.8 µVrms with 4.7 µF (p. 5).
- **Soft-start match with the LT3045:** tSS ≈ 2.3 × RSET × CSET ≈ 65 ms with equal RSET and CSET on both rails (p. 22; BOM line 110). Fast start-up is disabled (PGFB tied to IN) because the SET currents differ (1.8 mA vs 2 mA typ). See the LT3045 sheet.
- **Enable from 3.3 V logic:** the positive EN/UV threshold (1.26 V) lets the shared 3.3 V `HPA_LDO_EN` net drive it directly; EN/UV to IN is then 10.3 V, inside the −0.3 V to 30 V rating (p. 3).
- **PSRR at the T1 headroom:** the 74 dB at 1 MHz is at VIN − VOUT = 2 V. At about 1 V, curve G47 reads about 65 dB at 1 MHz, close to the 1.25 MHz TPS65131 switching frequency.
- **Capacitors:** COUT 10 µF X7R (ESR < 30 mΩ, ESL < 1.5 nH), CIN 10 µF X7R (p. 15, p. 18, p. 20; BOM line 110).
- **Thermal:** about 0.33 W at 275 mA (power tree v0 §4.2); GND current 2.35 mA typ at no load.
- **VIOC** is not needed with the TPS65131 pre-rail; float it (p. 15). Using it to trim the TPS65131 negative output is a design option for the maintainers, **UNVERIFIED** against the TPS65131 feedback network.

## Sources

- Analog Devices, LT3094 datasheet, Rev. B (01/20), via the LCSC mirror: <https://datasheet.lcsc.com/datasheet/pdf/1a8bfd511d8ae1f9056ba9136e868838.pdf>. Manufacturer URL (not reachable from this host): <https://www.analog.com/media/en/technical-documentation/data-sheets/lt3094.pdf>
- OpenDAP board BOM v1 (v1.3), lines 25–26 and 109–110, Changes in v1.3 item 3; power tree v0 §4.1, §4.2, §4.10.1, §6.2 (`public/board/docs/specs/`).
