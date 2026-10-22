# PMEG6010CEH

- **Manufacturer:** Nexperia (data sheet issued by NXP Semiconductors)
- **Function:** 60 V, 1 A very low VF MEGA Schottky barrier rectifier
- **BOM v1 lines:** 53 (TPS61169 backlight boost rectifier, qty 1; BOM v1.1, replaces the PMEG4010CEH); ordered as PMEG6010CEH,115
- **Package:** SOD123F, 2-lead flat-lead plastic SMD, body 2.5–2.7 × 1.5–1.7 mm, 1.0–1.2 mm height
- **Datasheet:** *PMEG6010CEH; PMEG6010CEJ 1 A very low VF MEGA Schottky barrier rectifiers*, product data sheet Rev. 02, 27 March 2007 (document PMEG6010CEH_PMEG6010CEJ_2), with a Nexperia cover notice. Cited below as "Rev. 02"; pages are the document's own page numbers. File sha256 `00cb4092481811245afeadff66d4bf266ff5486c7ca28fb47e822868f8689bee` (matches the BOM v1.1 Datasheets table). The copy came from the LCSC mirror; the Nexperia URL (assets.nexperia.com) returned HTTP 403 in this session.
- **Status:** Partly UNVERIFIED

## Summary

Planar MEGA Schottky barrier rectifier with an integrated guard ring for stress protection, in the flat-lead SOD123F package; the PMEG6010CEJ is the same die in SOD323F (SC-90) (Rev. 02, p. 1, §1.1, Table 1). IF ≤ 1 A, VR ≤ 60 V, VF 570 mV typ / 660 mV max at 1 A (p. 1, Table 2). In the T1 it is the rectifier of the TPS61169 backlight boost (BOM v1 line 53). It replaces the 40 V PMEG4010CEH, which left 1 V of margin above the TPS61169 39 V maximum OVP threshold (BOM v1 §9 D25; [TPS61169DCKR](../Texas-Instruments/TPS61169DCKR.md)). The ",115" suffix is the packing code for 3000 pieces on 8 mm tape (p. 6, Table 9).

## Absolute maximum ratings

Rev. 02, p. 3, Table 6 (IEC 60134).

| Parameter | Symbol | Condition | Max | Unit |
|---|---|---|---|---|
| Reverse voltage | VR | — | 60 | V |
| Forward current | IF | Tsp ≤ 55 °C | 1 | A |
| Repetitive peak forward current | IFRM | tp ≤ 1 ms, δ ≤ 0.25 | 7 | A |
| Non-repetitive peak forward current | IFSM | square wave, tp = 8 ms | 9 | A |
| Total power dissipation | Ptot | Tamb ≤ 25 °C, standard footprint | 375 | mW |
| Total power dissipation | Ptot | Tamb ≤ 25 °C, 1 cm² cathode pad | 830 | mW |
| Junction temperature | Tj | — | 150 | °C |
| Ambient temperature | Tamb | — | −65 to +150 | °C |
| Storage temperature | Tstg | — | −65 to +150 | °C |

Ptot conditions: FR4, single-sided copper, tin-plated (p. 3, notes 1–2). ESD rating: not given in the data sheet (**UNVERIFIED**).

## Recommended operating conditions

The data sheet has no recommended-operating-conditions table; operation is bounded by the limiting values above. Thermal characteristics (p. 3, Table 7):

| Parameter | Condition | Max | Unit |
|---|---|---|---|
| Rth(j-a) | standard footprint | 330 | K/W |
| Rth(j-a) | 1 cm² cathode pad | 150 | K/W |
| Rth(j-sp) | to the cathode tab solder point | 60 | K/W |

Thermal runaway must be considered for Schottky diodes when reverse losses are a significant part of the total (p. 3, note 1).

## Power by mode

Characteristics at Tamb = 25 °C (p. 4, Table 8; VF pulse-tested, tp ≤ 300 µs, δ ≤ 0.02):

| Parameter | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| VF | IF = 1 mA | 210 | 250 | mV |
| VF | IF = 10 mA | 270 | 310 | mV |
| VF | IF = 100 mA | 350 | 400 | mV |
| VF | IF = 500 mA | 460 | 530 | mV |
| VF | IF = 700 mA | 510 | 580 | mV |
| VF | IF = 1 A | 570 | 660 | mV |
| IR | VR = 5 V | 0.8 | — | µA |
| IR | VR = 10 V | 1.1 | — | µA |
| IR | VR = 60 V | 11 | 50 | µA |
| Cd | VR = 1 V, f = 1 MHz | 60 | 68 | pF |

Temperature dependence of IF(VF) and IR(VR) is given as typical curves only (p. 5, Fig 1–2; −40 to 150 °C and −40 to 125 °C). Capacitance versus VR: p. 5, Fig 3.

T1 estimate (calculation): the average diode current equals the LED current, 60 mA at full brightness; with VF ≤ 400 mV at 100 mA (25 °C) the conduction loss is below about 24 mW. Peak switch current 0.45 A (power tree v0 §4.5) gives VF ≤ 530 mV at 500 mA.

## Pinout and package

Pinning (p. 2, Table 3):

| Pin | Function |
|---|---|
| 1 | Cathode (marked by the bar) |
| 2 | Anode |

Package outline SOD123F (p. 6, Fig 5, 04-11-29): overall length 3.4–3.6 mm, body 2.5–2.7 × 1.5–1.7 mm, height 1.0–1.2 mm, lead width 0.55–0.70 mm, lead length 0.35–0.55 mm, lead thickness 0.10–0.25 mm. Marking code CA (p. 2, Table 5). Packing: 4 mm pitch, 8 mm tape and reel; -115 = 3000, -135 = 10000 (p. 6, Table 9). The "-115" in the table corresponds to the ",115" ordering suffix (last three digits of the 12NC). Lead finish and MSL are not given in this data sheet (**UNVERIFIED**).

## Recommended footprint

Reflow soldering footprint SOD123F (p. 7, Fig 7): two lands 1.1 mm wide (2×); horizontal dimensions 1.6, 2.9, 4.0 and 4.4 mm; vertical dimensions 2.1 and 1.6 mm on the left, 1.1 and 1.2 mm on the right. The drawing distinguishes solder lands, solder resist, solder paste and occupied area; the assignment of each dimension to one of them is read from the drawing only (**UNVERIFIED** until checked against the PDF when drawing the KiCad footprint). Reflow soldering is the only recommended method (p. 7). Same SOD123F land as the PMEG4010CEH it replaces (BOM v1 line 53).

## Application circuit and required passives

Not applicable: the data sheet gives no application circuit. In the T1 the anode is on the TPS61169 SW node and the cathode on the LED string output with the 1 µF 50 V output capacitor (BOM v1 §5; TPS61169 sheet).

## Interfaces and timing

Not applicable. Reverse-recovery data is not given (Schottky); the 60–68 pF junction capacitance at 1 V (p. 4) is charged on every switching cycle.

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. Nexperia SPICE model availability is **UNVERIFIED**.

## Design notes for the T1

- **Voltage margin:** VR 60 V against the TPS61169 VOVP of 39 V maximum (SNVSA40B p. 5, on the TPS61169 sheet) leaves 21 V; the normal string voltage is 14–16.5 V (power tree v0 §4.5).
- **Leakage at temperature:** IR is 11 µA typ / 50 µA max at 60 V and 25 °C (p. 4); at higher temperature only typical curves exist (p. 5, Fig 2). Reverse loss at ≈ 16.5 V is small at room temperature; the hot-case figure is **UNVERIFIED** until read from the curve.
- **Data sheet age:** Rev. 02 is a 2007 NXP document under a Nexperia cover notice. Whether a newer Nexperia revision exists is **UNVERIFIED** (the Nexperia URL returned HTTP 403).
- **Sourcing:** pin genuine Nexperia LCSC codes; clones are listed under the same name (BOM v1 line 53). The SOD323F PMEG6010CEJ,115 is the BOM second source; it needs its own footprint (p. 7, Fig 8).

## Sources

- Nexperia (NXP Semiconductors), *PMEG6010CEH; PMEG6010CEJ* product data sheet, Rev. 02, 27 March 2007: <https://assets.nexperia.com/documents/data-sheet/PMEG6010CEH_PMEG6010CEJ.pdf> (copy obtained from the LCSC mirror)
- OpenDAP board BOM v1.1, line 53, §5, §9 D25; power tree v0 §4.5 (`public/board/docs/specs/`).
- File name: the ",115" packing suffix is omitted, as for [BAT54](BAT54.md).
