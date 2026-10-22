# TPS7A4901DGNR

- **Manufacturer:** Texas Instruments
- **Function:** 150 mA ultralow-noise positive linear regulator, adjustable output
- **BOM v1 lines:** 25 (+5.0 V headphone-amplifier LDO)
- **Package:** 8-pin HVSSOP PowerPAD (DGN), 3.00 × 3.00 mm body
- **Datasheet:** *TPS7A49 36-V, 150-mA, Ultralow-Noise, Positive Linear Regulator*, SBVS121E, August 2010, revised May 2015. Cited below as "SBVS121E". File sha256 `f69e957b22bcc2db72149f57c96501aedeb4ed214f016c98f562d71411474182` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The TPS7A4901 is the adjustable version of the TPS7A49, a bipolar positive linear regulator for 3 V to 36 V input, 150 mA output, with 15.4 µVrms output noise (10 Hz to 100 kHz) and 72 dB PSRR at 120 Hz (SBVS121E, p. 1). The DGNR suffix is the 8-pin HVSSOP PowerPAD on a 2500-piece reel (SBVS121E, p. 22, Table 2; package addendum). In the T1 it regulates the +6.0 V pre-rail from the TPS65131 down to HPA_P5V0 (+5.0 V), the positive supply of the four OPA1622 headphone amplifiers (BOM v1 line 25; power tree v0 §2 and §4.2).

## Absolute maximum ratings

SBVS121E, p. 5, §6.1.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| IN to GND | −0.3 | 36 | V |
| OUT to GND | −0.3 | 33 | V |
| OUT to IN | −36 | 0.3 | V |
| FB to GND | −0.3 | 2 | V |
| FB to IN | −36 | 0.3 | V |
| EN to IN | −36 | 0.3 | V |
| EN to GND | −0.3 | 36 | V |
| NR/SS to IN | −36 | 0.3 | V |
| NR/SS to GND | −0.3 | 2 | V |
| Peak output current | internally limited | | |
| Operating junction TJ | −40 | 125 | °C |
| Storage Tstg | −65 | 150 | °C |

ESD (SBVS121E, p. 5, §6.2): HBM ±1500 V; CDM ±500 V.

## Recommended operating conditions

SBVS121E, p. 5, §6.3.

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | 3 | | 35 | V |
| VEN | 0 | | VIN | V |
| VOUT | VFB | | 33 | V |
| IOUT | 0 | | 150 | mA |
| TJ | −40 | | 125 | °C |
| CIN | 2.2 | 10 | | µF |
| COUT | 2.2 | 10 | | µF |
| CNR (noise reduction) | 0 | 10 | | nF |
| CFF (feed-forward) | 0 | 10 | | nF |
| R2 (lower feedback resistor) | | | 237 | kΩ |

Thermal, DGN package (SBVS121E, p. 6, §6.4): RθJA 63.4 °C/W, RθJB 37.4 °C/W, RθJC(bot) 13.5 °C/W, ψJB 37.1 °C/W.

## Power by mode

SBVS121E, p. 6, §6.5, typical at TA = 25 °C.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | VEN = 0.4 V | 0.8 | 3 | µA |
| Ground current, no load | IOUT = 0 mA | 49 | 100 | µA |
| Ground current, loaded | IOUT = 100 mA | 800 | — | µA |
| Dropout | IOUT = 100 mA | 260 | — | mV |
| Dropout | IOUT = 150 mA | 333 | 600 | mV |

Dissipation: PD = (VIN − VOUT) × IOUT + VIN × IQ (SBVS121E, p. 17, Eq. 3).

## Pinout and package

8-pin HVSSOP PowerPAD (DGN), 3.00 mm × 3.00 mm body (SBVS121E, p. 1 and p. 4).

| Pin | Name | Function |
|---|---|---|
| 1 | OUT | Regulator output; ≥ 2.2 µF to ground required for stability |
| 2 | FB | Error-amplifier input; sets VOUT |
| 3 | NC | Not internally connected; leave open or tie to GND |
| 4 | GND | Ground |
| 5 | EN | Enable; may be tied to IN if unused; VEN ≤ VIN |
| 6 | NR/SS | Noise-reduction and soft-start capacitor |
| 7 | DNC | Do not connect; not even to GND or IN |
| 8 | IN | Input supply |
| PowerPAD | — | Leave open or tie to ground; solder to the PCB plane for thermal performance |

(SBVS121E, p. 4, Pin Functions.)

The datasheet carries two DGN outlines: DGN0008D (exposed pad 1.63–1.89 mm × 1.28–1.57 mm, drawing 4225481/A, p. 33) and DGN0008G (exposed pad 1.95–2.15 mm × 1.646–1.846 mm, drawing 4225480/C, p. 36). Body 2.9–3.1 mm, 4.75–5.05 mm over leads, 0.65 mm pitch, 1.1 mm max height. Which outline applies to a given TPS7A4901DGNR lot is not stated in the datasheet: **UNVERIFIED**; the land patterns of both are identical (below). MSL Level-2-260C-1 YEAR; lead finish "Call TI | NiPdAuAg | NiPdAu" (SBVS121E, p. 24, addendum).

## Recommended footprint

SBVS121E, p. 34 (DGN0008D) and p. 37 (DGN0008G), identical dimensions:

- 8 pads 1.4 mm × 0.45 mm, 0.65 mm pitch, pad-row span 4.4 mm.
- Thermal pad 9: metal (2) mm × (3) mm, solder-mask-defined opening 1.57 mm × 1.89 mm; optional 0.2 mm vias; vias under paste filled, plugged or tented.
- Non-solder-mask-defined signal pads preferred; 0.05 mm mask clearance.
- Stencil: see p. 35 / p. 38.

## Application circuit and required passives

Maximum-AC-performance circuit (SBVS121E, p. 16, Figure 29; p. 14, §9.1.3–9.1.5):

| Ref | Value | Note |
|---|---|---|
| CIN | 10 µF (2.2 µF minimum) | X5R/X7R, ESR < 200 mΩ, same side as the IC, no vias to the pin |
| COUT | 10 µF (2.2 µF minimum) | same |
| CNR/SS | 10 nF | Filters reference noise (69 → 17 µVrms per §9.1.6); sets soft-start |
| CFF | 10 nF, FB to OUT | Improves PSRR 10 Hz–200 kHz (§9.1.8) |
| R1, R2 | Feedback divider | VOUT = VFB × (1 + R1/R2); divider current ≥ 5 µA; R2 ≤ 237 kΩ |

- VFB = 1.185 V typ; VREF 1.176 / 1.188 / 1.212 V (SBVS121E, p. 6).
- Accuracy ±1.5 % nominal at 25 °C, ±2.5 % overall (SBVS121E, p. 6). The datasheet recommends 0.1 % divider resistors for higher accuracy (p. 14, §9.1.1).
- Dropout headroom (VIN − VOUT − VDO(max)) of at least 1 V for optimal performance (SBVS121E, p. 16, §9.2.2).
- Do not float EN; do not load NR/SS resistively or inductively; capacitors within 10 mm (SBVS121E, p. 19, §9.3).

## Interfaces and timing

- EN: VEN(high) ≥ 2.1 V, VEN(low) ≤ 0.4 V, IEN 0.02 µA typ (SBVS121E, p. 6).
- Soft-start: tSS (ms) = 1.4 × CNR/SS (nF); 10 nF gives 14 ms (SBVS121E, p. 12, Eq. 1).
- Current limit 220 / 309 / 500 mA (SBVS121E, p. 6).
- Thermal shutdown 170 °C, reset 150 °C (SBVS121E, p. 6).
- Noise: 12.7 µVrms 20 Hz–20 kHz (p. 1); 21.15 µVrms at VOUT = 5 V, VIN = 6.2 V, COUT = 10 µF, CNR = CFF = 10 nF, 10 Hz–100 kHz (p. 6).
- PSRR 72 dB at 120 Hz in the same 5 V condition (p. 6); ≥ 52 dB from 10 Hz to 400 kHz with the Figure 29 circuit (p. 14, §9.1.5).

## Linux driver

None. No digital interface. Can be described as a `regulator-fixed` supply gated by a GPIO (BOM v1 line 25: driver path *none*).

## Simulation models

- SPICE model: "available through the product folder under Tools & Software" (SBVS121E, p. 22, §12.1.1.2). Exact file, format and revision **UNVERIFIED**; no manifest entry yet.
- EVM: TPS7A30-49EVM-567, user's guide SLVU405 (SBVS121E, p. 22, §12.1.1.1).

## Design notes for the T1

- **EN threshold:** VEN(high) min is 2.1 V (SBVS121E, p. 6). A 1.8 V SoC GPIO (`HPA_RAIL_EN`, power tree v0 §7) does not meet it. Options consistent with the datasheet: tie EN to IN (allowed, p. 4) so the LDO follows the TPS65131 ENP rail, or drive EN through a level shifter. The choice belongs to the schematic and is open.
- VIN = +6.0 V, VOUT = +5.0 V gives 1.0 V headroom; at 150 mA the max dropout is 600 mV, so the margin beyond VDO(max) is 0.4 V, below the 1 V the datasheet calls optimal (p. 16). At playback currents (10–40 mA, power tree v0 §2) the dropout is lower than the 100 mA figure; the PSRR at the actual headroom is read from the datasheet curves (Figure 18, not transcribed).
- PSRR at the TPS65131 switching frequency (1.25–1.38 MHz) is not specified; the power tree's ≥ 40 dB assumption is **UNVERIFIED**.
- 0.1 % divider resistors are consistent with the ERA-3AEB precision series already in the BOM (line 37).
- Layout: separate input and output ground planes star-connected at GND, PowerPAD to ground with multiple vias, all capacitors on the same side (SBVS121E, p. 19, §11.1–11.1.1).
- Ramp symmetry with the TPS7A3001 (OPA1622 requirement) depends on matching CNR/SS soft-start on both LDOs; the TPS7A3001 soft-start law is on its own sheet.

## Sources

- TI, TPS7A49 datasheet, SBVS121E (May 2015): <https://www.ti.com/lit/ds/symlink/tps7a49.pdf>
- OpenDAP board BOM v1, line 25; power tree v0 §2, §4.2, §7 (`public/board/docs/specs/`).
