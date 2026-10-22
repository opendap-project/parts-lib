# DF40C-100DS-DP-0.4V

- **Manufacturer:** Hirose Electric
- **Function:** 100-contact board-to-FPC connector pair, 0.4 mm pitch, 1.5 mm stacking height: DF40C-100DP-0.4V(51) header (board) and DF40C-100DS-0.4V(51) receptacle (FPC)
- **BOM v1 lines:** 66 (signals; 2 + 2 per end, Proposed, picked in ADR 0009)
- **Package:** SMT, double row. Header 21.52 × 2.97 mm, 1.14 mm high; receptacle 22.6 × 3.38 mm, 1.45 mm high
- **Datasheet:** DF40 Series catalog, edition May 1, 2020 (catalog 2020.2); DF40C-*DP-0.4V(51) header drawing EDC3-311351-00 (revision 7, 2018-11-19) and specification sheet ELC4-311351-01 (2008-06-27). Copies obtained from the LCSC datasheet mirror.
- **Status:** Partly UNVERIFIED

## Summary

The DF40 is a 0.4 mm-pitch board-to-board and board-to-FPC connector family with stacking heights from 1.5 to 4.0 mm, a 0.45 mm effective mating length at 1.5 mm stacking and a locking system on the 10- to 50-position parts (DF40 catalog 2020, p. 1). In the T1 the 100-contact pair carries the HAT flat cable's signals (BOM v1 line 66, BRD-013, ADR 0002): the DF40C-100DP header sits on the board and on the device-side piece, the DF40C-100DS receptacle on each end of the flat cable. The DS + DP combination without a stacking-height code is the 1.5 mm stack (p. 3, product number structure).

## Absolute maximum ratings

| Parameter | Value | Condition | Reference |
|---|---|---|---|
| Rated current | 0.3 A per contact | — | Catalog p. 2, Ratings; spec sheet ELC4-311351-01 |
| Rated voltage | 30 V AC, DC | — | Catalog p. 2 (spec sheet: 30 V AC) |
| Insulation resistance | 50 MΩ min | 100 V DC | Catalog p. 2, item 1 |
| Withstanding voltage | No flashover or breakdown | 100 V AC, 1 minute | Catalog p. 2, item 2 |
| Contact resistance | 90 mΩ max | 20 mV AC, 1 kHz, 1 mA | Catalog p. 2, item 3 |
| Durability | Contact resistance ≤ 90 mΩ | 30 mating cycles | Catalog p. 2, item 7; spec sheet |
| Storage temperature | −10 to +60 °C, 40–70 % RH (Note 2) | — | Catalog p. 2 |
| Soldering heat | Reflow per profile; iron 350 °C, ≤ 3 s | — | Catalog p. 2, item 8 |

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Operating temperature | −35 to +85 °C, including temperature rise from current (Note 1) | Catalog p. 2; spec sheet |
| Operating humidity | 20 to 80 % | Catalog p. 2 |

Materials (catalog p. 2): LCP insulator (black, UL94V-0); phosphor-bronze contacts, gold plated. Header drawing: contact area gold 0.05 µm minimum over 1 µm minimum nickel (EDC3-311351-00, material table).

## Power by mode

Not applicable (passive connector).

## Pinout and package

Two rows of 50 contacts at 0.4 mm pitch. **The four corner contacts of the header are metal hold-downs and must not be used as signal or power contacts** (catalog p. 10, note 3; drawing EDC3-311351-00, note 2): 96 contacts are usable. The connector is not polarized (catalog p. 4, note 4; p. 10, note 5). The 60- to 120-position parts have no locking concave on the contacts (drawing EDC3-311351-00, note 3; catalog p. 10, note 2), so the 100-position pair has no tactile lock.

| Item | Header DF40C-100DP-0.4V(51) | Receptacle DF40C-100DS-0.4V(51) | Reference |
|---|---|---|---|
| HRS No. | 684-4032-1 51 | 684-4033-4 51 | Catalog pp. 10, 4 |
| Length A | 21.52 ± 0.2 mm | 22.6 ± 0.2 mm | Catalog pp. 10, 4 |
| Contact span B | 19.6 ± 0.08 mm | 19.6 ± 0.08 mm | Catalog pp. 10, 4 |
| Vacuum pick-up area C | 3.2 ± 0.2 mm | 3.2 ± 0.2 mm | Catalog pp. 10, 4 |
| Width | 2.97 ± 0.2 mm (body 1.85 ± 0.2) | 3.38 ± 0.2 mm (body 2.88 ± 0.2) | Catalog pp. 10, 4 |
| Height | 1.14 ± 0.15 mm | D = 1.45 ± 0.15 mm | Catalog pp. 10, 4 |
| Lead width | 0.15 ± 0.02 mm | 0.12 ± 0.02 mm | Catalog pp. 10, 4 |
| Packaging | (51): embossed tape, full reels | (51): embossed tape, 5,000 per reel | Catalog pp. 3, 4 |

Lead coplanarity 0.1 mm maximum (drawing EDC3-311351-00, note 1).

## Recommended footprint

Header DF40C-100DP (catalog p. 10; drawing EDC3-311351-00, recommended pattern):

- Lands 0.23 ± 0.02 mm wide at P = 0.4 ± 0.02 mm; outer row edge to edge 3.37 (+0.05/0) mm, inner 2.05 (0/−0.05) mm, so each land is about 0.66 mm long; contact span B = 19.6 ± 0.02 mm.
- The corner (hold-down) lands are 0.35 ± 0.02 mm wide; drawing dimensions 0.475 ± 0.02 mm and catalog 0.3 ± 0.02 / 0.65 ± 0.02 mm locate them from the last signal land (the two documents dimension them differently: check against the drawing).
- Metal mask 120 µm thick, 80 % opening ratio for the lead pads (drawing).

Receptacle DF40C-100DS, 1.5 mm stacking, DF40C (without reinforcing metal fitting) (catalog p. 4):

- Lands 0.2 ± 0.02 mm wide at P = 0.4 ± 0.02 mm; outer row edge to edge 3.78 (+0.05/0) mm, inner 2.38 (0/−0.05) mm (land length about 0.7 mm); span B = 19.6 ± 0.02 mm; 1.5 mm max resist-coating area between rows (note 3).

## Application circuit and required passives

Not applicable. HAT ESD sits at the pogo field on the device-side piece (lines 68, 69); HAT rail TVS TVS0500 at the board flat-cable connector (line 65); USB 3 and PCIe TX AC-coupling capacitors on line 70.

## Interfaces and timing

The catalog states that the shielded DF40 type supports high-speed signal transmission (p. 1, feature 9); the T1 uses the standard, non-shielded type. No impedance, insertion-loss or data-rate figure for the standard type is in the catalog. The 5 Gb/s capability assumed in BOM line 66 is **UNVERIFIED**: a test coupon is required before freeze (BOM line 66).

## Linux driver

None (passive part).

## Simulation models

None listed in `manifest.toml`. Hirose S-parameter models for DF40: **UNVERIFIED**.

## Design notes for the T1

- The 100-pin connector plan in BOM line 66 (12 pairs in GSSG = 37 contacts, 46 low-speed, 6 analog, grounds) must fit in 96 usable contacts, not 100: the four corner contacts are hold-downs (catalog p. 10, note 3).
- The 100-position pair has no contact locking concave (drawing note 3): mating retention relies on contact friction only; the case or a clamp must hold the flat cable.
- 0.3 A per contact (catalog p. 2) applies to the signal grounds as well.
- Rated for 30 mating cycles (catalog p. 2): the flat cable is an assembly part, not a user-pluggable cable.
- Not polarized (catalog p. 4 note 4, p. 10 note 5): the flat-cable ends must be keyed mechanically or by the case to prevent a 180° mating.
- Self-alignment range 0.33 mm (catalog p. 1, feature 4).
- The receptacle is placed on the FPC, which is a fabricated flex board (BOM line 102); the FPC must have a stiffener under the receptacle (stiffener specification **UNVERIFIED**, not in the catalog).

## Sources

- Hirose Electric, *0.4 mm Pitch, 1.5 to 4.0 mm Height, Board-to-Board and Board-to-FPC Connectors, DF40 Series*, catalog May 1, 2020; copy from the LCSC datasheet mirror (LCSC part C597931), sha256 `d49c00f06336c89fbf2eda5d8db7c452d3376bbd53dd1732d125b480159dd370`; the DF40C-30DS-DP cache folder holds the Aug. 1, 2019 edition (LCSC part C424642), sha256 `b806e4a9a488507525fbc3174b2ad9273a08efcd24d151c45a3ccb3db540e19f`, not used here. Manifest URL <https://www.hirose.com/en/product/document?clcode=&productname=&series=DF40&documenttype=Catalog&lang=en&documentid=en_DF40_CAT>
- Hirose Electric, DF40C-*DP-0.4V(51) drawing EDC3-311351-00 (LCSC part C531031), sha256 `9aba1fa11097eaa2cc85b774a5001aa3dbde399b071c3e2df4584c9d7d47debb`
- Hirose Electric, DF40C-*DP-0.4V(51) specification sheet ELC4-311351-01 (LCSC part C429942), sha256 `f77d162f091a9cd5657cec41abb8ba9fbd5ba3e34050e5690c8f44be4913e5a8`
- OpenDAP board, `docs/specs/bom-v1.md`, lines 65, 66, 68–70, 102
