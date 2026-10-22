# Samsung KLMBG2JETD-B041

- **Datasheet not downloaded.** Samsung does not publish a public datasheet for this part (NDA); `manifest.toml` has an empty URL. Every value below comes from OpenDAP's BOM or from the SoC side and is **UNVERIFIED** against a Samsung document.
- **BOM v1 line:** 10 (eMMC, 32 GB), Core

## Summary

eMMC managed NAND, 32 GB, the T1 boot and system storage on the RK3566 eMMC controller (BOM v1 line 10). Second sources named in the BOM: Micron, Kioxia, Longsys FORESEE. Supply risk: one stocked brand (BOM v1 line 10).

## Absolute maximum ratings

**UNVERIFIED** (no datasheet).

## Recommended operating conditions

| Parameter | Value | Source |
|---|---|---|
| VCC (NAND core) | vcc3v3_sys 3.3 V from TLV62569 (BOM v1 line 6) | BOM; part limits **UNVERIFIED** |
| VCCQ (I/O) | 1.8 V, RK3566 bank VCCIO2 with FLASH_VOL_SEL high (BOM v1 §4) | BOM; part limits **UNVERIFIED** |
| eMMC version, speed modes, temperature range | **UNVERIFIED** | — |

## Power by mode

**UNVERIFIED** (no datasheet).

## Pinout and package

**UNVERIFIED** (no datasheet). Package and ball map must come from Samsung or a published reference design.

## Recommended footprint / land pattern

**UNVERIFIED** (no datasheet).

## Application circuit and required passives

**UNVERIFIED** (VCC/VCCQ/VDDi decoupling values, RSTn and DS handling per the part datasheet).

## Interfaces and timing

RK3566 eMMC host: eMMC 4.41/4.51/5.0/5.1, 1/4/8-bit bus, HS200, command queue (RK3568 Datasheet Rev 1.0, p. 8, §1.2.5; the RK3566 brief lists eMMC 5.1, RK3566 Brief Datasheet p. 1). Boot from eMMC is supported by the BootROM (RK3568 Datasheet Rev 1.0, p. 8, §1.2.4).

## Linux driver

None specific (BOM v1 line 10). The RK356x eMMC host uses mainline `sdhci-of-dwcmshc` (**UNVERIFIED** in this session).

## Simulation models available

None public. No `manifest.toml` entry other than the empty datasheet row.

## Design notes for the T1

- VCCQ is fixed at 1.8 V (VCCIO2), which HS200 requires; HS400 support on RK3566 is not stated in the RK3568 datasheet read here (**UNVERIFIED**).
- Verify footprint compatibility before accepting any of the second sources.

## Sources

- OpenDAP board, `docs/specs/bom-v1.md`, lines 6, 10 and §4.
- Rockchip, RK3568 Datasheet Rev 1.0, 2020-12-10; RK3566 Brief Datasheet (2022).
