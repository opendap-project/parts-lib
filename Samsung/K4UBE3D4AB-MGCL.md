# K4UBE3D4AB-MGCL

- **Manufacturer:** Samsung
- **Function:** LPDDR4X SDRAM, 32 Gb (4 GB) dual-die package
- **BOM v1 lines:** 8 (LPDDR4X, 4 GB), Core
- **Package:** 200FBGA, 10.00 × 15.00 mm (DS p. 9)
- **Datasheet:** Samsung *K4UBE3D4AB-MGCL LPDDR4X SDRAM* datasheet, Rev. 1.0, Aug. 2021, 108 pages, cited as "DS". Distributor copy (LCSC C5827966) listed in `manifest.toml`; not redistributable.
- **Availability (2026-10-24):** Samsung's product page lists the part as **discontinued**. Supply risk as in BOM v1 line 8 and §8.
- **Status:** Package, ball map, organisation and supply ranges from DS. Power by mode, the AC timing values and the IBIS model are not transcribed here.

## Summary

32 Gb LPDDR4X in a dual-die package: two dies, each with two 8 Gb x16 channels, so each channel A and B has two ranks selected by CS0 and CS1 (DS p. 7; p. 12, Functional Block Diagram). Up to 4266 Mb/s (tCK 0.468 ns), backward compatible with lower rates; LVSTLE_06 interface (DS p. 8). It is the T1 system memory on the RK3566 32-bit controller (BOM v1 line 8). Second source in the BOM: SK hynix H9HCNNNCPMMLXR-NEE.

## Absolute maximum ratings

DS p. 6 (LPDDR4X column of the LPDDR3/LPDDR4/LPDDR4X comparison): VDD1 −0.4 to 2.1 V; VDD2 −0.4 to 1.4 V; VDDQ −0.4 to 1.4 V; VIN/VOUT −0.4 to 1.4 V; storage −55 to 125 °C. The full table is DS §7.0, p. 44 (not transcribed).

## Recommended operating conditions

DS p. 5 (LPDDR4X column) and p. 7:

| Parameter | Value |
|---|---|
| VDD1 | 1.70–1.95 V (1.8 V nominal) |
| VDD2 | 1.06–1.17 V (1.1 V nominal) |
| VDDQ | 0.57–0.65 V (0.6 V nominal) |
| Case temperature | −25 to 85 °C (DS p. 8) |
| Refresh | 8K / 32 ms (DS p. 8), 3.9 µs (DS p. 7) |

## Power by mode

IDD values: DS §11, pp. 65–85, not transcribed (**UNVERIFIED** here).

## Pinout and package

- **Package** 200FBGA, body 10.00 ± 0.10 × 15.00 ± 0.10 mm, height 0.90 ± 0.10 mm, stand-off 0.22 ± 0.05 mm, ball Ø 0.31 ± 0.05 mm after reflow (solder ball Ø 0.30 mm), ball position tolerance Ø 0.15 mm to A-B (DS p. 9).
- **Ball grid**: 12 columns at 0.80 mm (0.80 × 11 = 8.80 mm) and 22 rows A–AB at 0.65 mm (0.65 × 21 = 13.65 mm), centred; columns 6–7 and rows L–M carry no ball (DS pp. 9–10).
- **Ball map**: DS p. 10, §4.2 (top view). Channel A in rows A–K, channel B mirrored in rows N–AB; ZQ0 A5, ZQ1 A8, RESET_n T11, ODT_CA_a G2, ODT_CA_b T2; DNU at A1, A2, A11, A12, B1, B12, G11, K5, K8, N5, N8, AA1, AA12, AB1, AB2, AB11, AB12.
- The same ball map, with JEDEC names, is in the Radxa ZERO 3W v1.12 schematic, sheet 14; it matches DS ball for ball (kicad-lib `generator/bga/Samsung/`).

## Recommended footprint

Samsung gives no land pattern. kicad-lib footprint `Samsung:Samsung_FBGA-200_10.0x15.0mm_Layout12x22_P0.8x0.65mm_Ball0.3mm_Pad0.25mm_NSMD`: NSMD 0.25 mm copper, 0.35 mm mask opening (kicad-lib `generator/bga/Samsung/K4UBE3D4AB-MGCL.toml` gives the reasoning).

## Application circuit and required passives

- VDDQ 0.6 V from TPS7A1006PDSER (VIN = vcc_ddr 1.1 V, BIAS = vcc_1v8), BOM v1 line 9; see [`Texas-Instruments/TPS7A1006PDSER.md`](../Texas-Instruments/TPS7A1006PDSER.md).
- vcc_ddr decoupling as on the Radxa ZERO 3W v1.12 reference: 2 × 22 µF + 1 µF + 10 × 100 nF (BOM v1 §5).
- ODT_CA: "ODT pin should connect to VDD2 or VSS"; the ODT_CA balls are wired to the rank 0 die (DS p. 10, notes 1 and 2).
- ZQ resistor value, per-ball decoupling: not transcribed (**UNVERIFIED**).

## Interfaces and timing

- RK3566 controller: LPDDR4X, 32-bit data width (RK3566 DS Rev 1.1; RK3566 Brief Datasheet p. 1).
- Training and timing are set by the Rockchip DDR init blob (rkbin ≥ v1.26, BOM v1 line 8). Whether this exact part is on Rockchip's supported-memory list is **UNVERIFIED**.

## Linux driver

None (BOM v1 line 8: "none (rkbin DDR blob ≥ v1.26)"). The memory is initialised by the boot loader; Linux sees it as system RAM.

## Simulation models

None available publicly; IBIS models for LPDDR4X are normally released under NDA (**UNVERIFIED**).

## Design notes for the T1

- Two ranks per channel (DS p. 12): connect CS1 and CKE1 of both channels (board pinout v1 ball A3 note).
- Routing (length matching, impedance) must follow the RK3566 hardware design guide and DS.
- Keep the SK hynix second source footprint-compatible only if both packages match; not verified.

## Sources

- Samsung, K4UBE3D4AB-MGCL datasheet Rev. 1.0, Aug. 2021 (`manifest.toml`).
- Samsung semiconductor product page, K4UBE3D4AB-MGCL (discontinued notice), read 2026-10-24.
- Radxa ZERO 3W v1.12 schematic, sheet 14 (`manifest.toml`, Radxa).
- OpenDAP board, `docs/specs/bom-v1.md`, lines 8, 9, §5, §8.
