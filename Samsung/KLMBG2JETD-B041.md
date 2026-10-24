# KLMBG2JETD-B041

- **Manufacturer:** Samsung
- **Function:** eMMC 5.1 managed NAND, 32 GB
- **BOM v1 lines:** 10 (eMMC, 32 GB), Core
- **Package:** 153FBGA, 11.50 × 13.00 × 0.8 mm class (DS p. 4, Table 1; p. 6, Figure 3)
- **Datasheet:** Samsung *KLMxGxJETD-B041 eMMC 5.1* datasheet, Rev. 1.0, Nov. 2016, 26 pages, cited as "DS"; it covers KLMAG1JETD-B041 (16 GB), KLMBG2JETD-B041 (32 GB) and KLMCG4JETD-B041 (64 GB). Distributor copy (LCSC C2803245) listed in `manifest.toml`; not redistributable.
- **Status:** Package, ball map, supplies and features from DS. Power by mode and timing are not transcribed here.

## Summary

eMMC 5.1 with 2 × 128 Gb NAND, HS200 and HS400, command queuing, 1/4/8-bit bus, 0–200 MHz interface clock, 0–52 MHz in boot (DS p. 4). It is the T1 boot and system storage on the RK3566 eMMC controller (BOM v1 line 10).

## Absolute maximum ratings

Not transcribed (**UNVERIFIED** here).

## Recommended operating conditions

DS p. 4 (Table 1 and key features):

| Parameter | Value |
|---|---|
| VDD (VCCQ), interface | 1.70–1.95 V or 2.7–3.6 V |
| VDDF (VCC), memory | 2.7–3.6 V |
| Operating temperature | −25 to 85 °C |
| Storage temperature, not operating | −40 to 85 °C |

## Power by mode

Not transcribed (**UNVERIFIED** here).

## Pinout and package

- **Package** body 11.50 ± 0.10 × 13.00 ± 0.10 mm, height 0.72 ± 0.08 mm, stand-off 0.21 ± 0.05 mm, 153 balls Ø 0.30 ± 0.05 mm, ball position tolerance Ø 0.15 mm to A-B, coplanarity 0.08 mm (DS p. 6, Figure 3).
- **Ball grid**: 14 × 14 at 0.50 mm (0.50 × 13 = 6.50 mm, 3.25 mm from the centre lines), partly depopulated (DS p. 5, Figure 1; p. 6).
- **Ball map** (DS p. 5, Table 2 and Figure 1): DAT0–DAT2 A3–A5, DAT3–DAT7 B2–B6, CMD M5, CLK M6, Data Strobe H5, RSTN K5; VDD (VCCQ) C6, M4, N4, P3, P5; VDDF (VCC) E6, F5, J10, K9; VDDI C2; VSS A6, C4, E7, G5, H10, J5, K8, N2, N5, P4, P6. RFU ("do not use for any usage") A7, E5, E8, E9, E10, F10, G3, G10, K6, K7, K10, P7, P10; every other ball NC.

## Recommended footprint

Samsung gives no land pattern. kicad-lib footprint `Samsung:Samsung_FBGA-153_11.5x13.0mm_Layout14x14_P0.5mm_Ball0.3mm_Pad0.25mm_NSMD` (shared by KLMAG1JETD-B041 and KLMBG2JETD-B041): NSMD 0.25 mm copper, 0.35 mm mask opening (reasoning in kicad-lib `generator/bga/Samsung/KLMBG2JETD-B041.toml`).

## Application circuit and required passives

- VDDi is the internal regulator node for the controller core; it takes a capacitor CReg (DS p. 7, Figure 5). The value is not stated in DS (**UNVERIFIED**); the RK3566 hardware design guide asks for 2.2 µF or more (see [`Rockchip/RK3566.md`](../Rockchip/RK3566.md)).
- VCC/VCCQ decoupling values: **UNVERIFIED** (not in DS).

## Interfaces and timing

RK3566 eMMC host: eMMC 4.41–5.1, 1/4/8-bit, HS200, command queue (RK3566 HDG 1.1, p. 26). DS supports HS200 and HS400 (p. 4); HS400 on the RK3566 is not stated (**UNVERIFIED**).

## Linux driver

None specific (BOM v1 line 10). The RK356x eMMC host uses mainline `sdhci-of-dwcmshc` (**UNVERIFIED** in this session).

## Simulation models

None public.

## Design notes for the T1

- VCCQ at 1.8 V (VCCIO2 with FLASH_VOL_SEL high) is inside DS's 1.70–1.95 V range.
- Verify footprint compatibility before accepting any second source.

## Sources

- Samsung, KLMxGxJETD-B041 eMMC 5.1 datasheet Rev. 1.0, Nov. 2016 (`manifest.toml`).
- OpenDAP board, `docs/specs/bom-v1.md`, line 10.
