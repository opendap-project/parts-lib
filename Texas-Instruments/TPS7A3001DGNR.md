# TPS7A3001DGNR

- **Manufacturer:** Texas Instruments
- **Function:** −200 mA ultralow-noise negative linear regulator, adjustable output
- **BOM v1 lines:** none in v1.3. Line 26 (−5.0 V headphone-amplifier LDO) up to BOM v1.2
- **Package:** 8-pin HVSSOP PowerPAD (DGN), 3.00 × 3.00 mm body
- **Datasheet:** *TPS7A30 −35-V, −200-mA, Ultralow-Noise, Negative Linear Regulator*, SBVS125D, August 2010, revised June 2015. Cited below as "SBVS125D". File sha256 `b60d6fd8d7220e9f8a4dcfeaa7438a5e5e419ef589e1ea85e9d04781f2203ae5` (matches the BOM v1 Datasheets table).
- **Status:** Not in the current BOM (replaced in BOM v1.3 by LT3045/LT3094, ADR 0012)

## Summary

The TPS7A3001 is the adjustable version of the TPS7A30, a bipolar negative linear regulator for −3 V to −35 V input and up to 200 mA, with 15.1 µVrms output noise (10 Hz to 100 kHz), 72 dB PSRR at 120 Hz and ≥ 55 dB from 10 Hz to 700 kHz (SBVS125D, p. 1). In the T1 it regulates the −6.0 V pre-rail from the TPS65131 to HPA_N5V0 (−5.0 V), the negative supply of the four OPA1622 headphone amplifiers, as the negative counterpart of the TPS7A4901 (BOM v1 line 26; power tree v0 §2 and §4.2).

## Absolute maximum ratings

SBVS125D, p. 5, §6.1.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| IN to GND | −36 | 0.3 | V |
| OUT to GND | −33 | 0.3 | V |
| OUT to IN | −0.3 | 36 | V |
| FB to GND | −2 | 0.3 | V |
| FB to IN | −0.3 | 36 | V |
| EN to IN | −0.3 | 36 | V |
| EN to GND | −36 | 36 | V |
| NR/SS to IN | −0.3 | 36 | V |
| NR/SS to GND | −2 | 0.3 | V |
| Peak output current | internally limited | | |
| Operating junction TJ | −40 | 125 | °C |
| Storage Tstg | −65 | 150 | °C |

ESD (SBVS125D, p. 5, §6.2): HBM ±1500 V; CDM ±500 V.

## Recommended operating conditions

SBVS125D, p. 6, §6.3.

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | −35 | | −3 | V |
| VEN | 0 | | VIN | V |
| VOUT | VREF | | 33 (magnitude) | V |
| IOUT | 0 | | 200 | mA |
| TJ | −40 | | 125 | °C |
| CIN | 2.2 | 10 | | µF |
| COUT | 2.2 | 10 | | µF |
| CNR | 0 | 10 | | nF |
| CFF | 0 | 10 | | nF |
| R2 (lower feedback resistor) | | | 237 | kΩ |

The table prints VEN as "0 to VIN" while the pin description allows a positive enable (|VEN| ≤ |VIN|) and the EC table specifies positive thresholds up to 15 V (SBVS125D, p. 4 and p. 7).

Thermal, DGN package (SBVS125D, p. 6, §6.4): RθJA 63.4 °C/W, RθJB 37.4 °C/W, RθJC(bot) 13.5 °C/W.

## Power by mode

SBVS125D, p. 7, §6.5, typical at TA = 25 °C.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | VEN = 0.4 V or −0.4 V | 1 | 3 | µA |
| Ground current, no load | IOUT = 0 mA | 55 | 100 | µA |
| Ground current, loaded | IOUT = 100 mA | 950 | — | µA |
| Dropout | IOUT = 100 mA | 216 | — | mV |
| Dropout | IOUT = 200 mA | 325 | 600 | mV |

Dissipation: PD = (VIN − VOUT) × IMAX + VIN × IQ (SBVS125D, p. 20, Eq. 3).

## Pinout and package

8-pin HVSSOP PowerPAD (DGN), 3.00 mm × 3.00 mm body (SBVS125D, p. 1, p. 4).

| Pin | Name | Function |
|---|---|---|
| 1 | OUT | Output; ≥ 2.2 µF to ground required |
| 2 | FB | Feedback; sets VOUT |
| 3 | NC | Not internally connected; open or GND |
| 4 | GND | Ground |
| 5 | EN | Dual-polarity enable; may be tied to IN; \|VEN\| ≤ \|VIN\| |
| 6 | NR/SS | Noise-reduction and soft-start capacitor |
| 7 | DNC | Do not connect to any net |
| 8 | IN | Input supply (negative) |
| PowerPAD | — | Leave open or tie to GND; solder to the PCB plane |

(SBVS125D, p. 4, Pin Functions.)

Outline DGN0008D (SBVS125D, p. 39, drawing 4225481/A 11/2019): body 2.9–3.1 mm, 4.75–5.05 mm over leads, 0.65 mm pitch, 1.1 mm max height, exposed pad 1.63–1.89 mm × 1.28–1.57 mm. Addendum (SBVS125D, p. 30): NiPdAu, MSL Level-2-260C-1 YEAR, −40 to 125 °C, marking PSZQ, 2500 per reel.

## Recommended footprint

SBVS125D, p. 40 (DGN0008D example board layout):

- 8 pads 1.4 mm × 0.45 mm, 0.65 mm pitch, pad-row span 4.4 mm.
- Thermal pad 9: metal (2) mm × (3) mm, solder-mask-defined opening 1.57 mm × 1.89 mm; optional 0.2 mm vias, filled, plugged or tented under paste.
- Non-solder-mask-defined signal pads preferred.
- Stencil: SBVS125D, p. 41.

## Application circuit and required passives

Maximum-AC-performance circuit (SBVS125D, p. 20, Figure 32; p. 18, §9.1.2–9.1.3):

| Ref | Value | Note |
|---|---|---|
| CIN | 10 µF (2.2 µF minimum) | Low-ESR X5R/X7R, within 10 mm, same side |
| COUT | 10 µF (2.2 µF minimum) | same |
| CNR/SS | 10 nF | Reference noise 80 → 17 µVrms (§9.1.4); sets soft-start |
| CFF | 10 nF, FB to OUT | PSRR improvement 10 Hz–200 kHz (§9.1.5) |
| R1, R2 | Divider | \|VOUT\| = \|VFB\| × (1 + R1/R2); divider current ≥ 5 µA |

- Standard 1 % values for −5 V: R1 = 32.4 kΩ, R2 = 10 kΩ (SBVS125D, p. 17, Table 2).
- VFB = −1.176 V typ; VREF −1.202 / −1.179 / −1.166 V (SBVS125D, p. 7).
- Accuracy ±1.5 % nominal at 25 °C, ±2.5 % overall (SBVS125D, p. 7). 0.1 % resistors recommended for higher accuracy (p. 17, §9.1.1).
- Do not float EN; do not load NR/SS resistively or inductively (SBVS125D, p. 23, §9.3).

## Interfaces and timing

- EN, dual polarity (SBVS125D, p. 7; p. 15, §8.3.3):

| Threshold | Min | Max | Unit |
|---|---|---|---|
| VEN(+HI), TJ −40 to 125 °C | 2 | 15 | V |
| VEN(+HI), TJ −40 to 85 °C | 1.8 | 15 | V |
| VEN(+LO) | 0 | 0.4 | V |
| VEN(−HI) | VIN | −2 | V |
| VEN(−LO) | −0.4 | 0 | V |

- Soft-start: tSS (ms) = 0.9 × CNR/SS (nF) (SBVS125D, p. 15, Eq. 1).
- Current limit 220 / 330 / 500 mA (SBVS125D, p. 7).
- Thermal shutdown 170 °C, reset 150 °C (SBVS125D, p. 7).
- Noise 17.5 µVrms at VIN = −6.2 V, VOUT = −5 V, COUT = 10 µF, CNR = CFF = 10 nF, 10 Hz–100 kHz; PSRR 72 dB at 120 Hz in the same condition (SBVS125D, p. 7). 14 µVrms 20 Hz–20 kHz (p. 1).

## Linux driver

None. No digital interface; describe as a GPIO-gated `regulator-fixed` supply (BOM v1 line 26: driver path *none*).

## Simulation models

- SPICE model: "available through the product folders under the Tools & Software tab" (SBVS125D, p. 28, §12.1.1.2). File and revision **UNVERIFIED**; no manifest entry yet.
- EVM: TPS7A30-49EVM-567, user's guide SLVU405 (SBVS125D, p. 28, §12.1.1.1).

## Design notes for the T1

- **EN from 1.8 V logic:** VEN(+HI) min is 1.8 V only from −40 to 85 °C and 2 V over the full junction range (SBVS125D, p. 7). A 1.8 V GPIO has no margin. Options from the datasheet: tie EN to IN (the LDO then follows the TPS65131 ENN rail) or drive EN from a ≥ 2 V logic level. To be fixed in the schematic.
- Soft-start laws differ from the TPS7A4901 (0.9 ms/nF here, 1.4 ms/nF there). Matching ramp times on ±5 V, needed for the OPA1622 (power tree v0 §7), requires different CNR/SS values, or EN tied to IN on both and the ramp set by the TPS65131 soft-start. **UNVERIFIED** until simulated or measured.
- Headroom −6.0 V → −5.0 V = 1.0 V; max dropout at 200 mA is 600 mV (SBVS125D, p. 7).
- PSRR at the TPS65131 switching frequency (1.25–1.38 MHz) is outside the specified ≥ 55 dB band (10 Hz–700 kHz); the value there is **UNVERIFIED**.
- Layout as TPS7A4901: separate input and output ground planes star-connected at GND, PowerPAD to ground with vias, all capacitors on the same side (SBVS125D, p. 24, §11.1).

## Sources

- TI, TPS7A30 datasheet, SBVS125D (June 2015): <https://www.ti.com/lit/ds/symlink/tps7a30.pdf>
- OpenDAP board BOM v1, line 26; power tree v0 §2, §4.2, §7 (`public/board/docs/specs/`).
