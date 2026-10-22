# RT0603 series (RT0603BRD071KL, RT0603BRD071K62L, RT0603BRD0760K4L)

- **Manufacturer:** Yageo
- **Function:** Thin-film precision chip resistors, 0603, ±0.1 %, 25 ppm/°C (RT series)
- **BOM v1 lines:** all new in BOM v1.3 (ADR 0012, D30), Proposed
  - RT0603BRD071KL (1.00 kΩ): line 37, R1 = R3 of the 12 HP-amp difference amplifiers, quantity 24
  - RT0603BRD071K62L (1.62 kΩ): line 37, R2 = R4 of the same networks, quantity 24
  - RT0603BRD0760K4L (60.4 kΩ): line 109, RSET of the LT3045 and LT3094 HP-amp LDOs, quantity 2
- **Package:** 0603 (1608 metric), 1.60 × 0.80 × 0.45 mm
- **Datasheet:** *Thin Film Chip Resistors, High precision – high stability, RT series 0.01 % to 1 %, TCR 5 to 50, sizes 0100 to 2512*, product specification V.16, May 6, 2025, 10 pages. Cited below as "RT V.16". File sha256 `0a729d144519a7021c82a0ef242b064e467c70d44afcf9eabd6c7ffdc4b673a3`.
  - Footprint and soldering: Yageo *Chip resistors mounting*, not opened.
- **Status:** Partly UNVERIFIED

## Summary

The RT series are Yageo thin-film chip resistors with tolerances from ±0.01 % to ±1 % and TCR from 5 to 50 ppm/°C (RT V.16, p. 1). The global part number decodes as RT · 0603 · B (±0.1 %) · R (paper/PE taping reel) · D (25 ppm/°C) · 07 (7″ reel) · value · L (default code) (RT V.16, p. 2). The three values are in the E-96 series. In the T1 they set the gain of the OPA1622 difference amplifiers (1.00 kΩ / 1.62 kΩ, gain 1.62) and the ±6.04 V outputs of the LT3045 and LT3094 (VOUT = 100 µA × 60.4 kΩ) (BOM v1 lines 37 and 109).

## Absolute maximum ratings

RT V.16, p. 5, Table 2 (RT0603).

| Parameter | Value |
|---|---|
| Rated power at 70 °C | 1/10 W |
| Maximum working voltage | 75 V |
| Maximum overload voltage | 150 V |
| Operating temperature range | −55 °C to +155 °C |

- Power derating: 100 % up to 70 °C, linear to 0 % at 155 °C for RT0402 to RT1206 (RT V.16, p. 6, Fig. 6).
- Rated continuous voltage: V = √(P × R) or the maximum working voltage, whichever is less (RT V.16, p. 6).

## Recommended operating conditions

RT V.16, p. 5, Table 2, RT0603 at ±25 ppm/°C.

| Tolerance | Resistance range (E-24/E-96) |
|---|---|
| ±0.1 % | 1 Ω to 1 MΩ |
| ±0.25 %, ±0.5 %, ±1 % | 1 Ω to 1 MΩ |
| ±0.05 % | 4.7 Ω to 100 kΩ |

All three T1 values (1.00 kΩ, 1.62 kΩ, 60.4 kΩ) are inside the ±0.1 %, 25 ppm/°C range.

Stability (RT V.16, pp. 7–8, Table 4): endurance at 70 °C for 1000 h, high-temperature exposure, moisture resistance, thermal shock (−55/+125 °C, 300 cycles), damp heat, short-time overload and resistance to soldering heat each ±(0.5 % + 0.05 Ω); board flex (3 mm for 0603) ±(0.25 % + 0.05 Ω). TCR is measured at +25/−55 °C and +25/+125 °C (MIL-STD-202 Method 304).

## Power by mode

Passive part. Dissipation is V² / R; see Design notes for the T1.

## Pinout and package

Two terminals, Ni / matte tin over inner electrodes, thin-film resistive layer on a ceramic substrate under a protective coat (RT V.16, p. 4, Fig. 5).

| Dimension | Value (mm) |
|---|---|
| L | 1.60 ± 0.10 |
| W | 0.80 ± 0.10 |
| H | 0.45 ± 0.10 |
| I1 (top termination) | 0.25 ± 0.15 |
| I2 (bottom termination) | 0.25 ± 0.15 |

(RT V.16, p. 4, Table 1.) Marking on RT0603: three characters for E-96 values (RT V.16, p. 4, Fig. 3). Packaging: 5000 per 7″ paper/PE reel (RT V.16, p. 6, Table 3). Unit weight 2.128 mg (p. 5). MSL 1, halogen-free epoxy, RoHS compliant (RT V.16, p. 2).

## Recommended footprint

Not in this document: RT V.16, p. 6, refers to the Yageo *Chip resistors mounting* data sheet, which was not opened. The 0603 land pattern is **UNVERIFIED** from a Yageo source.

## Application circuit and required passives

None of its own.

## Interfaces and timing

Not applicable.

## Linux driver

None (passive part).

## Simulation models

Not applicable (ideal resistor). No manifest entry beyond the datasheet.

## Design notes for the T1

- **Difference-amplifier match (line 37):** each network has R1 = R3 = 1.00 kΩ and R2 = R4 = 1.62 kΩ. With ±0.1 % parts the worst-case ratio error is ±0.2 % per ratio (calculation); the common-mode rejection that results is not computed in the BOM (**UNVERIFIED**). TCR 25 ppm/°C applies to each part; tracking between parts is not specified in RT V.16.
- **Dissipation (line 37):** even with the ±5.2 V maximum no-load output swing (BOM line 36) across 1.62 kΩ, the peak dissipation is 5.2² / 1620 ≈ 17 mW, 17 % of 1/10 W (calculation, an upper bound).
- **RSET (line 109):** 60.4 kΩ × 100 µA = 6.04 V across the part, 0.6 mW (calculation). The ±0.1 % tolerance is small against the ±2 % SET current spread of the LDOs (BOM line 109). Leakage into the SET node matters more than the resistor: LT3045 Rev. D, p. 16, asks for a guard ring around SET (BOM line 109).
- **Second sources named in the BOM:** Panasonic ERA-3AEB102V (1.00 kΩ), ERA-3AEB1621V (1.62 kΩ), ERA-3AEB6042V (60.4 kΩ), Susumu RG1608 (BOM lines 37, 109); not checked here.

## Sources

- Yageo, RT series thin-film chip resistors, product specification V.16 (2025-05-06), from the LCSC datasheet mirror <https://datasheet.lcsc.com/datasheet/pdf/46d7760c582640714d605308a25a220a.pdf> (the yageo.com document path returned HTTP 404 on 2026-10-22), sha256 `0a729d144519a7021c82a0ef242b064e467c70d44afcf9eabd6c7ffdc4b673a3`.
- OpenDAP board BOM v1 (v1.3), lines 37 and 109; power tree v0 §4.1, §4.2 (`public/board/docs/specs/`).
