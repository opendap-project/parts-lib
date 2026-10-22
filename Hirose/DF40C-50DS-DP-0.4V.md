# DF40C-50DS-DP-0.4V

- **Manufacturer:** Hirose Electric
- **Function:** 50-contact board-to-FPC connector pair, 0.4 mm pitch, 1.5 mm stacking height: DF40C-50DP-0.4V(51) header (board) and DF40C-50DS-0.4V(51) receptacle (FPC)
- **BOM v1 lines:** 66 (HAT power connector: HAT_5V ×12, HAT_3V3 ×6, GND ×22, HAT_DET# ×1, reserved ×5; 2 + 2 per end, Proposed, picked in ADR 0009; v1.2 replaces the 30-contact pair)
- **Package:** SMT, double row. Header 11.52 × 2.97 mm, 1.14 mm high; receptacle 12.6 × 3.38 mm, 1.45 mm high
- **Datasheet:** DF40 Series catalog, edition Aug. 1, 2019, copy from the LCSC datasheet mirror (origin URL not recorded), sha256 `b806e4a9a488507525fbc3174b2ad9273a08efcd24d151c45a3ccb3db540e19f`. Cited below as "catalog 2019". Pages are those of this edition.
- **Status:** Partly UNVERIFIED

## Summary

The DF40 is a 0.4 mm-pitch board-to-board and board-to-FPC connector family with stacking heights from 1.5 to 4.0 mm, a 0.45 mm effective mating length at 1.5 mm stacking and a locking system on the 10- to 50-position parts (catalog 2019, p. 1, features 2 and 3). The 50-position part is offered at every stacking height, 1.5 to 4.0 mm (p. 1, stacking height variations). In the T1 the 50-contact pair carries the HAT flat cable's power (BOM v1 line 66, BRD-013, ADR 0002, v1.2 change 2): the DF40C-50DP header sits on the board and on the device-side piece, the DF40C-50DS receptacle on each end of the flat cable. The contact allocation comes from the hat-standard HAT interface v0 (Draft). It replaces the [DF40C-30DS-DP-0.4V](DF40C-30DS-DP-0.4V.md) pair, which could not carry HAT_5V and HAT_3V3 with their returns at ≤ 70 % per contact.

## Absolute maximum ratings

Catalog 2019, p. 2, Product Specifications.

| Parameter | Value | Condition |
|---|---|---|
| Rated current | 0.3 A | — |
| Rated voltage | 30 V AC, DC | — |
| Insulation resistance | 50 MΩ min | 100 V DC |
| Withstanding voltage | No flashover or breakdown | 100 V AC, 1 minute |
| Contact resistance | 90 mΩ max | 20 mV AC, 1 kHz, 1 mA |
| Vibration | No discontinuity ≥ 1 µs | 10–55 Hz, half amplitude 0.75 mm, 3 directions, 2 h |
| Durability | Contact resistance ≤ 90 mΩ | 30 mating cycles |
| Storage temperature | −10 to +60 °C, 40–70 % RH (Note 2) | — |
| Soldering heat | Reflow per recommended profile; iron 350 °C, ≤ 3 s | — |

The catalog states the rated current without "per contact" and without an all-contacts-loaded derating; reading it as per contact (as the 30-pin sheet and BOM v1 line 66 do) is the usual convention but is **UNVERIFIED** against a Hirose statement.

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Operating temperature | −35 to +85 °C, including temperature rise from current (Note 1) | Catalog 2019, p. 2 |
| Operating humidity | 20 to 80 % | Catalog 2019, p. 2 |

Materials, standard non-shielded type (catalog 2019, p. 2): LCP insulator (black, UL94V-0); phosphor-bronze contacts, gold plated. Plating thickness for the 50-position parts: **UNVERIFIED** (the 30-pin sheet's figure comes from the header drawing EDC3-311351-00; the cached copy of that drawing does not extract as text and was not checked for the 50-position row).

## Power by mode

Not applicable (passive connector).

## Pinout and package

Two rows of 25 contacts at 0.4 mm pitch. **The four corner contacts of the header are metal fittings and must not be used as signal or power contacts** (catalog 2019, p. 10, note 3): 46 contacts are usable. The connector is not polarized (p. 4, note 4; p. 10, note 5). The header has concave locking parts on its contacts up to 50 positions; from 60 positions there are none (p. 10, note 2; p. 1, feature 3).

| Item | Header DF40C-50DP-0.4V(51) | Receptacle DF40C-50DS-0.4V(51) | Reference |
|---|---|---|---|
| HRS No. | 684-4014-0 51 | 684-4009-0 51 | Catalog 2019, pp. 10, 4 |
| Length A | 11.52 ± 0.2 mm | 12.6 ± 0.2 mm | pp. 10, 4 |
| Contact span B | 9.6 ± 0.08 mm | 9.6 ± 0.08 mm | pp. 10, 4 |
| Vacuum pick-up area C | 3.2 ± 0.2 mm | 3.2 ± 0.2 mm | pp. 10, 4 |
| Width | 2.97 ± 0.2 mm (body 1.85 ± 0.2) | 3.38 ± 0.2 mm (body 2.88 ± 0.2) | pp. 10, 4 |
| Height | 1.14 ± 0.15 mm | D = 1.45 ± 0.15 mm | pp. 10, 4 |
| Lead width | 0.15 ± 0.02 mm | 0.12 ± 0.02 mm | pp. 10, 4 |
| Packaging | (51): embossed tape, full reels; 24 mm carrier tape | (51): embossed tape, 5,000 per reel | pp. 10, 15; p. 4 |

## Recommended footprint

Header DF40C-50DP (catalog 2019, p. 10):

- Lands 0.23 ± 0.02 mm wide at P = 0.4 ± 0.02 mm; outer row edge to edge 3.37 (+0.05/0) mm, inner 2.05 (0/−0.05) mm; contact span B = 9.6 ± 0.02 mm.
- Corner (metal fitting) lands 0.35 ± 0.02 mm wide, dimensioned 0.3 ± 0.02 mm and 0.65 ± 0.02 mm from the last contact land.
- Metal mask thickness and opening ratio: **UNVERIFIED** for this part (the 30-pin sheet takes 120 µm, 80 % from drawing EDC3-311351-00).

Receptacle DF40C-50DS, 1.5 mm stacking, DF40C (without reinforcing metal fitting) (catalog 2019, p. 4):

- Lands 0.2 ± 0.02 mm wide at P = 0.4 ± 0.02 mm; outer row edge to edge 3.78 (+0.05/0) mm, inner 2.38 (0/−0.05) mm; span B = 9.6 ± 0.02 mm; 1.5 mm max resist-coating area between rows (note 3).

## Application circuit and required passives

Not applicable. HAT rail TVS at the board flat-cable connector (BOM v1 line 65); HAT outputs limited by the TPS259470 eFuses (line 44) and the TPS2121 input limit (line 45).

## Interfaces and timing

Power only in the T1. HAT_DET# on this connector also proves the power connector is mated (BOM v1 line 66). No impedance or data-rate figure for the standard type is in the catalog.

## Linux driver

None (passive part).

## Simulation models

None listed in `manifest.toml`. Hirose S-parameter models for DF40: **UNVERIFIED**.

## Design notes for the T1

- **Contact current (BOM v1 line 66, power tree v0 §4.10).** At 0.3 A per contact: HAT_5V 2.0 A on 12 contacts = 0.17 A (56 %), 3.0 A input ceiling = 0.25 A (83 %, within the 100 % ceiling rule); HAT_3V3 1.0 A on 6 = 0.17 A (56 %), 1.15 A eFuse ceiling = 0.19 A (64 %); GND 3.0 A on 22 = 0.14 A (45 %), 4.15 A = 0.19 A (63 %). Recomputed here from the catalog rating; they match the BOM. The catalog gives no derating for all contacts loaded, so the 70 % rule is the project's own margin.
- **Voltage drop** (computed from the 90 mΩ maximum contact resistance, catalog p. 2; the catalog figure is measured at 1 mA): HAT_5V at 2.0 A over 12 contacts ≈ 15 mV, GND at 3.0 A over 22 ≈ 12 mV, per mated pair. A flat cable with a pair at each end doubles this; FPC conductor resistance comes on top.
- Rated voltage 30 V AC/DC (catalog p. 2) covers HAT_5V and HAT_3V3.
- Rated for 30 mating cycles (catalog p. 2): the flat cable is an assembly part, not a user-pluggable cable.
- Not polarized (catalog p. 4 note 4, p. 10 note 5): the flat-cable ends must be keyed mechanically or by the case to prevent a 180° mating, which on a power connector would put HAT_5V on other contacts.
- Self-alignment range 0.33 mm (catalog p. 1, feature 4).
- The receptacle sits on the FPC, a fabricated flex board (BOM v1 line 102); stiffener specification **UNVERIFIED** (not in the catalog).
- The header is 4.0 mm longer than the 30-pin part (11.52 vs 7.52 mm) and the receptacle 4.0 mm longer (12.6 vs 8.6 mm) (catalog pp. 10, 4): the board and FPC outlines must follow.

## Sources

- Hirose Electric, *0.4 mm Pitch, 1.5 to 4.0 mm Height, Board-to-Board and Board-to-FPC Connectors, DF40 Series*, catalog Aug. 1, 2019, copy from the LCSC datasheet mirror, sha256 `b806e4a9a488507525fbc3174b2ad9273a08efcd24d151c45a3ccb3db540e19f`. Manifest URL <https://www.hirose.com/en/product/document?clcode=&productname=&series=DF40&documenttype=Catalog&lang=en&documentid=en_DF40_CAT> (that URL returned an HTML page, not a PDF, on 2026-10-22).
- OpenDAP board BOM v1, line 66 and Changes in v1.2 item 2; power tree v0 §4.10 (`public/board/docs/specs/`); hat-standard HAT interface v0 (Draft).
