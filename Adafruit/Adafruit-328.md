# Adafruit 328

- **Manufacturer:** Adafruit
- **Function:** Single-cell lithium-ion polymer pack, 2500 mAh, with protection circuit module (PCM) and 2-pin JST PH lead; Adafruit lists it as a lithium-ion polymer battery, 3.7 V 2500 mAh
- **BOM v1 lines:** 46 (Power), the T1 battery, status Decided (board ADR 0007); connector line 47, board NTC line 48, gauge line 42
- **BOM v1.5:** removed from line 46 by board ADR 0014: the Adafruit 328 is no longer a T1 pack (the T1 runs on a quoted 2S pack). Kept for traceability.
- **Package:** Pouch cell 785060 with PCM and wire leads; pack 7.9 × 50.5 × 60.5 mm maximum with PCM
- **Datasheet:** Polymer Lithium-ion Battery Product Specification, model 785060 2500mAh, Q/WAPL785060-1011, edition 1.0, Hunan Sounddon New Energy Co., Ltd (cell maker's sheet published by Adafruit), <https://cdn-shop.adafruit.com/datasheets/785060-2500mAh_specification_sheet.pdf>
- **Status:** Partly UNVERIFIED

## Summary

Adafruit product 328 is a 1S lithium-ion polymer pack built on the Sounddon 785060 cell: 2500 mAh nominal at 0.2C, 3.75 V nominal, 4.2 V CC/CV charge, 2.75 V discharge cut-off, with a PCM based on the S-8261AAJMD protection IC and a JST PHR-2 connector on 26 AWG leads (Q/WAPL785060-1011 pp. 2, 10). It is the only adopted T1 battery (BOM line 46, ADR 0007). Nominal energy 2.5 Ah × 3.75 V = 9.4 Wh (calculation).

## Absolute maximum ratings

The sheet has no absolute-maximum table; these are its "must" and "max" limits.

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| Charge current | — | 1C5A (2.5 A) | A | Q/WAPL785060-1011 p. 2, §3; p. 6, §8.3.1 |
| Charge voltage ("must be lower than") | — | 4.25 | V | p. 7, §8.3.1 |
| Discharge current | — | 2C5A (5 A) | A | p. 7, §8.3.2 |
| Discharge voltage | 2.75 | — | V | p. 7, §8.3.2 |
| Tab soldering iron temperature / time | — | 350 °C / 3 s, ≤ 5 times | — | p. 8, §9.3 |
| Cell body heating | — | approx. 100 | °C | p. 8, §9.3 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Nominal capacity (0.2C5A, 25 °C) | — | 2500 | — | mAh | p. 2, §3 |
| Nominal voltage (average at 0.2C5A) | — | 3.75 | — | V | p. 2, §3 |
| Charge cut-off voltage (CC/CV) | — | 4.2 | — | V | p. 2, §3 |
| Standard charge current | — | 0.2C5A (0.5 A) | — | A | p. 2, §3 |
| Standard discharge current | — | 0.5C5A (1.25 A) | — | A | p. 2, §3 |
| Charge temperature | 0 | — | 40 | °C | p. 2, §3; p. 7, §8.3.1 |
| Discharge temperature | 0 | — | 60 | °C | p. 7, §8.3.2 |
| Impedance (AC 1 kHz, 50 % charge, 25 °C) | — | — | 35 | mΩ | p. 2, §3 |
| Cell voltage as shipped | 3.7 | — | 3.9 | V | p. 2, §3 |
| Storage ≤ 1 month / ≤ 3 months / ≤ 6 months | −10…45 / 0…30 / 20 ± 5 | — | — | °C | p. 2, §3 |
| Long-term storage | 40–60 % charged, 20 ± 5 °C, 45–85 % RH | — | — | — | p. 7, §8.4 |

Standard charge: 0.2C5A to 4.2 V, then 4.2 V until the current falls to 0.05C5A (p. 2, §4).

## Power by mode

| Mode | Conditions | Value | Source |
|---|---|---|---|
| 0.2C capacity | discharge 0.2C5A to 2.75 V | ≥ 300 min | p. 3, §4.1 |
| 1C capacity | discharge 1C5A to 2.75 V | ≥ 54 min | p. 3, §4.2 |
| Cycle life | 0.5C charge / 0.5C discharge until 1C… discharge time < 36 min | ≥ 400 cycles | p. 3, §4.3 |
| Charge retention | 28 days at 20 ± 5 °C, then 0.2C discharge | ≥ 240 min | p. 3, §4.4 |
| High temperature | 4 h at 60 °C, 0.2C discharge | ≥ 270 min | p. 3, §5.1 |
| Low temperature | 4 h at −10 °C, 0.2C discharge | ≥ 210 min | p. 3, §5.2 |

PCM quiescent current is not stated (**UNVERIFIED**).

## Pinout and package

| Pin | Name | Type | Function |
|---|---|---|---|
| red wire | BAT+ | power | Pack positive, UL 26 AWG (p. 10) |
| black wire | BAT− | power | Pack negative, UL 26 AWG (p. 10) |

Connector JST PHR-2 (p. 10, bill of materials item 5). Which contact of the PHR-2 carries red and which black is not given in the sheet (**UNVERIFIED**; BOM line 47 says to check the polarity on every lot).

Dimensions: cell 7.8 × 50 × 60 mm maximum, pack 7.9 × 50.5 × 60.5 mm maximum with PCM (p. 2, §2.3); the drawing table on p. 10 gives length 60.2, width 50.5, thickness 7.9 mm maximum and tab width 3 mm. Weight approx. 46 g (p. 2, §3). Lead length is not given (**UNVERIFIED**).

## Recommended footprint

Not applicable to the pack. The board side is the JST S2B-PH-SM4-TB header (BOM line 47).

## Application circuit and required passives

- Charger: CC/CV, ≤ 1C, 0–40 °C, < 4.25 V (p. 6–7, §8.3.1). In the T1 this is the BQ25895 (line 39) with VREG 4.20 V and 1.2 A charge (BOM line 39).
- PCM: S-8261AAJMD protection IC with an 8814 MOSFET (p. 10). The sheet's PCM design rules state an overcharge threshold "should not be exceeding 3.95V", an over-discharge threshold not below 2.3 V and a built-in short protection (p. 8, §9.2). The 3.95 V figure is below the 4.2 V charge cut-off on the same sheet, so it cannot be the threshold of the fitted PCM as written; the actual S-8261AAJMD thresholds are **UNVERIFIED** (its datasheet was not opened).
- No thermistor lead: the pack has two wires only, so the T1 senses temperature with the board NTC (line 48) pressed against the pocket floor.

## Interfaces and timing

None (two-wire pack, no data line).

## Linux driver

None for the pack itself. Its parameters reach the charger and gauge drivers through the device tree, typically a `simple-battery` node (`charge-full-design-microamp-hours`, `voltage-max-design-microvolt`, `constant-charge-voltage-max-microvolt`, `constant-charge-current-max-microamp`) referenced by `monitored-battery`; which properties the `bq25890_charger` and MAX17055 drivers actually read is **UNVERIFIED** (see their sheets). Values from this sheet: 2 500 000 µAh, 4 200 000 µV charge voltage, 2 750 000 µV minimum.

## Simulation models

None listed in `manifest.toml`. A cell model for the MAX17055 (ModelGauge m5 EZ or custom) has not been characterised (**UNVERIFIED**).

## Design notes for the T1

- **Charge window:** charge only at 0–40 °C (pp. 2, 7). The BQ25895 TS thresholds must be set by the TS divider for the board NTC so charging stops at or below 40 °C (power tree §4.7; see the BQ25895 sheet).
- **Charge current:** 1.2 A is 0.48C, inside the 1C maximum (p. 6). The standard rate is 0.2C (0.5 A).
- **Charge voltage:** 4.20 V CC/CV (p. 2) with a hard limit below 4.25 V (p. 7). The BQ25895 VREG setting must stay at 4.20 V or lower for this pack; LiHV settings (ADR 0008) are for other packs only.
- **Discharge current:** the cell allows 2C = 5 A (p. 7), but its 26 AWG leads and the JST PH contact (2 A per contact, BOM line 47) cap the T1 battery path: JST rates the PH contact 2 A with AWG #24 only, so BOM v1.1 derates the path to 1.6 A continuous (est.) for the 26 AWG leads (power tree §4.7, finding 8; BOM v1.1 lines 46–47).
- **Low-voltage cut-off:** the sheet's discharge floor is 2.75 V (p. 7); the system cut-off (gauge empty voltage, set in OpenDAP OS) must sit above it. The BQ25895 VSYSMIN of 3.5 V is not a cut-off: on battery VSYS follows VBAT below it (power tree v0 §3 designs VSYS for 3.4–4.4 V).
- **Long storage and shipping:** 40–60 % charge for storage, 10–50 % for transport (p. 7, §8.4–8.5). Ship mode (BATFET off) in the BQ25895 limits self-discharge during storage.
- **Mechanical:** the pouch must be fixed over its large face, protected from sharp edges, and its sealed and folded edges must not be bent or touch conductors (pp. 5–8). This applies to the T1 battery pocket.
- **Dimensional inconsistency:** pack length is 60.5 mm in §2.3 and 60.2 mm in the p. 10 table. Use 60.5 mm for the pocket until measured.

## Sources

- Hunan Sounddon New Energy, Polymer Lithium-ion Battery Product Specification, model 785060 2500mAh, Q/WAPL785060-1011, edition 1.0 (page 6 header reads Q/WAPL785060-0811), <https://cdn-shop.adafruit.com/datasheets/785060-2500mAh_specification_sheet.pdf>, sha256 `826149daa4aa9ba3ab7b635993a022d6521572a44d1d0588171468507b58ecd3` (manifest). Page numbers are the sheet's own page numbers (n/10).
- OpenDAP board BOM v1 lines 46–48, power tree v0 §4.7 and finding 8, board ADR 0007 (T1 context).
