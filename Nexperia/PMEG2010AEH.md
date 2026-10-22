# Nexperia PMEG2010AEH

- **BOM v1 line:** 24 (Audio, TPS65131 rectifiers), quantity 2
- **Datasheet:** NXP/Nexperia "PMEG2010AEH; PMEG2010AET 1 A very low VF MEGA Schottky barrier rectifiers", Rev. 03, 2007-03-28, product data sheet, 11 pages plus a Nexperia cover notice (cited as "Rev. 03"). Obtained from the LCSC-hosted copy of the manufacturer document (<https://datasheet.lcsc.com/datasheet/pdf/0048ef3cc1cc47f2a46f601985c58027.pdf?productCode=C110921>); the manifest URL returned HTTP 403 from this host.
- **Package:** SOD123F, 2 leads, flat

## Summary

A 20 V, 1 A planar Schottky barrier rectifier with integrated guard ring and very low forward voltage (Rev. 03 p. 1). In the T1 two parts are the rectifiers of the TPS65131 ±6 V pre-regulator for the headphone amplifiers (BOM v1 line 24). onsemi MBRM120LT1G (the TPS65131 datasheet example part) is the listed second source.

## Absolute maximum ratings

Rev. 03 Table 6, p. 3 (IEC 60134).

| Parameter | Symbol | Max | Unit | Condition |
|---|---|---|---|---|
| Reverse voltage | VR | 20 | V | — |
| Forward current | IF | 1 | A | Tsp ≤ 55 °C |
| Repetitive peak forward current | IFRM | 7 | A | tp ≤ 1 ms, δ ≤ 0.25 |
| Non-repetitive peak forward current | IFSM | 9 | A | Square wave, tp = 8 ms |
| Total power dissipation | Ptot | 375 | mW | Tamb ≤ 25 °C, standard footprint |
| Total power dissipation | Ptot | 830 | mW | Cathode pad 1 cm² |
| Junction temperature | Tj | 150 | °C | — |
| Ambient temperature | Tamb | −65 to +150 | °C | — |
| Storage temperature | Tstg | −65 to +150 | °C | — |

Thermal (Rev. 03 Table 7, p. 3): Rth(j-a) 330 K/W (standard footprint), 150 K/W (1 cm² cathode pad); Rth(j-sp) 60 K/W.

## Recommended operating conditions

No separate table. Characteristics at Tamb = 25 °C (Rev. 03 Table 8, p. 4):

| Parameter | Typ | Max | Unit | Condition |
|---|---|---|---|---|
| VF | 200 | 220 | mV | IF = 10 mA |
| VF | 265 | 290 | mV | IF = 100 mA |
| VF | 380 | 430 | mV | IF = 1 A |
| IR | 15 | 50 | µA | VR = 5 V |
| IR | 20 | 80 | µA | VR = 10 V |
| IR | 50 | 200 | µA | VR = 20 V |
| Cd | 55 | 70 | pF | VR = 5 V, 1 MHz |

VF is a pulse test, tp ≤ 300 µs, δ ≤ 0.02. IR rises steeply with temperature (Fig. 2, p. 5, curves for 25/85/125 °C not transcribed). The datasheet warns that thermal runaway must be considered because reverse losses can be significant (Table 7 note 1, p. 3).

## Power by mode

Not applicable (discrete). In the boost converter the losses are VF × IF while conducting plus VR × IR while blocking.

## Pinout and package

| Pin | Function |
|---|---|
| 1 | Cathode (marking bar side) |
| 2 | Anode |

Rev. 03 Table 3, p. 2. Marking code "AF" (Table 5, p. 2). SOD123F outline (Fig. 5, p. 6): body 2.5–2.7 × 1.5–1.7 mm, overall length with leads 3.4–3.6 mm, height 1.0–1.2 mm, lead width 0.55–0.70 mm. Packing: 3000 pcs (-115) or 10000 pcs (-135) on 8 mm tape (Table 9, p. 6).

## Recommended footprint / land pattern

Rev. 03 Fig. 7, p. 7, reflow footprint SOD123F: occupied area 4.4 × 2.1 mm; dimensions 4.0, 2.9, 1.6 mm (horizontal) and 1.6, 1.1, 1.2 mm (vertical); land width 1.1 mm (2×). Transcribe the full geometry from Fig. 7 when the footprint is drawn. Reflow soldering is the only recommended method.

## Application circuit and required passives

In the TPS65131 circuit (see its sheet) one diode is the positive-boost rectifier and one is in the inverting stage. Rating check: VR 20 V covers the ±6 V pre-rail configuration; peak current through each diode must be checked against IF 1 A and IFRM 7 A at the TPS65131 switch-current limit (**UNVERIFIED**, calculation not done here).

## Interfaces and timing

Not applicable. Reverse-recovery time is not specified (Schottky). Junction capacitance 55 pF typ at 5 V adds to switch-node capacitance.

## Linux driver

None (discrete).

## Simulation models available

None listed in `manifest.toml`. Nexperia SPICE model: **UNVERIFIED** (not searched).

## Design notes for the T1

- Reverse leakage up to 200 µA at 20 V and 25 °C, higher when hot (Rev. 03 p. 4–5); it is a standing loss on the ±6 V rails while the converter runs. The TPS65131 is shut down when the headphone path is idle (BOM line 22), which removes it.
- Use the 1 cm² cathode copper option if thermal margin is tight (Ptot 830 mW vs 375 mW, Table 6).

## Sources

- Nexperia PMEG2010AEH; PMEG2010AET product data sheet, Rev. 03, 2007-03-28, pp. 1–7 (LCSC-hosted copy, URL above).
- Board BOM v1, line 24.
