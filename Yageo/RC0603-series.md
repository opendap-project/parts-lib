# RC0603 series (RC0603FR-071RL, RC0603FR-07374RL, RC0603FR-079K31L, RC0603FR-07475KL, RC0603FR-07576KL, RC0603FR-07100KL)

- **Manufacturer:** Yageo
- **Function:** General-purpose thick-film chip resistors, 0603, ±1 % (RC_L series)
- **BOM v1 lines:** all new in BOM v1.3 (ADR 0012, D30), Proposed
  - RC0603FR-071RL (1.0 Ω): line 107, HP-amp ballast resistor, one per OPA1622 half, quantity 12
  - RC0603FR-07374RL (374 Ω): line 109, RILIM of the LT3045, quantity 1
  - RC0603FR-079K31L (9.31 kΩ): line 109, RILIM of the LT3094, quantity 1
  - RC0603FR-07475KL (475 kΩ): line 111, R1 of the TPS65131 positive divider, quantity 1
  - RC0603FR-07576KL (576 kΩ): line 111, R3 of the TPS65131 negative divider, quantity 1
  - RC0603FR-07100KL (100 kΩ): line 111, R2 and R4 of the TPS65131 dividers, quantity 2
- **Package:** 0603 (1608 metric), 1.60 × 0.80 × 0.45 mm
- **Datasheet:** *General Purpose Chip Resistors, RC_L series, ±0.1 %, ±0.5 %, ±1 %, ±5 %, sizes 0075 to 2512*, product specification V.12, August 2, 2022, 11 pages. Cited below as "RC V.12". File sha256 `e7dbabb0611925227ccfc429c14c8833a7b1f2c755684444124446f20b22a229`.
  - Footprint and soldering: Yageo *Chip resistors mounting*, not opened.
- **Status:** Partly UNVERIFIED

## Summary

The RC_L series are Yageo thick-film chip resistors for general-purpose use (RC V.12, p. 1–2). The global part number decodes as RC · 0603 · F (±1 %) · R (paper taping reel) · – (TCR per specification) · 07 (7″ reel, standard power) · value · L (default code) (RC V.12, p. 2). In the T1 they are the 1.0 Ω ballast resistors of the paralleled OPA1622 halves, the current-limit resistors of the LT3045 and LT3094, and the TPS65131 feedback dividers for the ±7.0 V pre-rails (BOM v1 lines 107, 109, 111).

## Absolute maximum ratings

RC V.12, p. 5, Table 2, RC0603 standard power (reel code 07).

| Parameter | Value |
|---|---|
| Rated power at 70 °C | 1/10 W |
| Maximum working voltage | 75 V |
| Maximum overload voltage | 150 V |
| Dielectric withstanding voltage | 150 V |
| Operating temperature range | −55 °C to +155 °C |

- Power derating: 100 % up to 70 °C, linear to 0 % at 155 °C for RC0402 to RC2512 (RC V.12, p. 7, Fig. 10-1).
- Rated continuous voltage: V = √(P × R) or the maximum working voltage, whichever is less (RC V.12, p. 7).
- The "7W" reel code gives 1/5 W in the same size (RC V.12, p. 2, p. 5); the T1 parts use "07".

## Recommended operating conditions

RC V.12, p. 5, Table 2, RC0603 (07).

| Parameter | Value |
|---|---|
| Resistance range, ±1 % (E-24/E-96) | 1 Ω to 10 MΩ |
| TCR, 1 Ω ≤ R ≤ 10 Ω | ±200 ppm/°C |
| TCR, 10 Ω < R ≤ 10 MΩ | ±100 ppm/°C |

All six T1 values are inside the ±1 % range. The 1.0 Ω part falls in the ±200 ppm/°C band; the others in the ±100 ppm/°C band.

Stability for ±1 % (F) parts (RC V.12, pp. 8–9, Table 5): endurance at 70 °C for 1000 h, high-temperature exposure and damp heat ±(1 % + 50 mΩ); moisture resistance, thermal shock and resistance to soldering heat ±(0.5 % + 50 mΩ); short-time overload and board flex (3 mm for 0603) ±(1 % + 50 mΩ).

## Power by mode

Passive part. Dissipation is I² × R or V² / R; see Design notes for the T1.

## Pinout and package

Two terminals, matte tin on a Ni barrier, thick-film resistive element under glass and an epoxy coat on a ceramic substrate (RC V.12, p. 4, Fig. 9).

| Dimension | Value (mm) |
|---|---|
| L | 1.60 ± 0.10 |
| W | 0.80 ± 0.10 |
| H | 0.45 ± 0.10 |
| I1 | 0.25 ± 0.15 |
| I2 | 0.25 ± 0.15 |

(RC V.12, p. 4, Table 1.) Marking on RC0603 at ±1 %: EIA-96 code for E-96 values, three digits otherwise (RC V.12, p. 3). Packaging: 5000 per 7″ paper reel (RC V.12, p. 7, Table 4). MSL 1, halogen-free epoxy, RoHS compliant (RC V.12, p. 2).

## Recommended footprint

Not in this document: RC V.12, p. 6, refers to the Yageo *Chip resistors mounting* data sheet, which was not opened. The 0603 land pattern is **UNVERIFIED** from a Yageo source.

## Application circuit and required passives

None of its own.

## Interfaces and timing

Not applicable.

## Linux driver

None (passive part).

## Simulation models

Not applicable (ideal resistor). No manifest entry beyond the datasheet.

## Design notes for the T1

- **Ballast, 1.0 Ω (line 107):** BOM line 107 estimates ≈ 5 mW at ≈ 100 mA peak per half (16 Ω limit), 5 % of 1/10 W; the rating used there matches RC V.12. Its tolerance (±1 %) and TCR (±200 ppm/°C) set how evenly paralleled halves share current, together with the amplifier offsets; current sharing is **UNVERIFIED** until simulated (BOM line 107).
- **RILIM (line 109):** 374 Ω gives 150 mA·kΩ / 374 Ω ≈ 401 mA on the LT3045; 9.31 kΩ gives 3.75 A·kΩ / 9.31 kΩ ≈ 403 mA on the LT3094 (BOM line 109). The ±1 % resistor tolerance adds ±1 % to the regulators' own programmed-limit spread (LT3045 Rev. D, p. 4: 450–550 mA at 300 Ω; LT3094 Rev. B, p. 5: 450–560 mA at 7.5 kΩ). The LT3045 ILIM pin is rated −0.3 V to 1 V (LT3045 Rev. D, p. 2), far below the resistor rating.
- **TPS65131 dividers (line 111):** VPOS = 1.213 V × (1 + 475 k / 100 k) = 6.97 V; VNEG = −1.213 V × 576 k / 100 k = −6.99 V (SLVS493E Eq. 1–2; BOM line 111). The divider current is about 12 µA, so dissipation is negligible (calculation). With ±1 % resistors the divider adds up to about ±2 % to the 3 % total DC accuracy of the converter (SLVS493E, p. 5; calculation); the LDO headroom estimate in power tree v0 §4.2 (≥ 0.7 V) is the place to check it.
- **Second sources named in the BOM:** Panasonic ERJ-3RQF1R0V for the 1.0 Ω ballast (BOM line 107); not checked here.

## Sources

- Yageo, RC_L series general-purpose chip resistors, product specification V.12 (2022-08-02), from the LCSC datasheet mirror <https://datasheet.lcsc.com/datasheet/pdf/b426be3ce22c6de3e0c3a2248e49159e.pdf> (the yageo.com document path returned HTTP 404 on 2026-10-22), sha256 `e7dbabb0611925227ccfc429c14c8833a7b1f2c755684444124446f20b22a229`.
- OpenDAP board BOM v1 (v1.3), lines 107, 109 and 111; power tree v0 §4.2 (`public/board/docs/specs/`).
