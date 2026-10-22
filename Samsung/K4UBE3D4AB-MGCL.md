# Samsung K4UBE3D4AB-MGCL

- **Datasheet not downloaded.** Samsung does not publish a public datasheet for this part (NDA); `manifest.toml` has an empty URL. Every value below comes from OpenDAP's BOM or from the SoC side and is **UNVERIFIED** against a Samsung document.
- **BOM v1 line:** 8 (LPDDR4X, 4 GB), Core

## Summary

LPDDR4X SDRAM, 4 GB, the T1 system memory on the RK3566 32-bit DDR controller (BOM v1 line 8). Second source in the BOM: SK hynix H9HCNNNCPMMLXR-NEE. Supply risk: broker prices and low stock (BOM v1 line 8 and §8).

## Absolute maximum ratings

**UNVERIFIED** (no datasheet).

## Recommended operating conditions

| Parameter | Value | Source |
|---|---|---|
| VDDQ (LPDDR4X) | 0.6 V nominal; the RK3566 PHY accepts 0.54–0.66 V | RK3568 Datasheet Rev 1.0, p. 55, Table 3-2 (SoC side) |
| VDD1, VDD2 | **UNVERIFIED** (LPDDR4X convention 1.8 V and 1.1 V; not confirmed for this part) | — |
| Speed grade, density organisation, temperature range | **UNVERIFIED** | — |

## Power by mode

**UNVERIFIED** (no datasheet). The VDDQ LDO current budget is also **UNVERIFIED** (BOM v1 line 9).

## Pinout and package

**UNVERIFIED** (no datasheet). Package type and ball map must come from Samsung under NDA or from a published reference design.

## Recommended footprint / land pattern

**UNVERIFIED** (no datasheet).

## Application circuit and required passives

- VDDQ 0.6 V from TPS7A1006PDSER (VIN = vcc_ddr 1.1 V, BIAS = vcc_1v8), BOM v1 line 9; see [`Texas-Instruments/TPS7A1006PDSER.md`](../Texas-Instruments/TPS7A1006PDSER.md).
- vcc_ddr decoupling as on the Radxa ZERO 3W v1.12 reference: 2 × 22 µF + 1 µF + 10 × 100 nF (BOM v1 §5).
- Other passives (ZQ resistor, VREF, per-ball decoupling): **UNVERIFIED**.

## Interfaces and timing

- RK3566 controller: LPDDR4X up to 3200, 32-bit data width, up to 8 GB addressing for LPDDR4/4X (RK3568 Datasheet Rev 1.0, p. 8, §1.2.5; the RK3566 brief lists 32-bit DDR4/3/3L/LPDDR4/4X/3, RK3566 Brief Datasheet p. 1).
- Training and timing are set by the Rockchip DDR init blob (rkbin ≥ v1.26, BOM v1 line 8). Whether this exact part is on Rockchip's supported-memory list is **UNVERIFIED**.

## Linux driver

None (BOM v1 line 8: "none (rkbin DDR blob ≥ v1.26)"). The memory is initialised by the boot loader; Linux sees it as system RAM.

## Simulation models available

None available publicly; IBIS models for LPDDR4X are normally released under NDA (**UNVERIFIED**). No `manifest.toml` entry other than the empty datasheet row.

## Design notes for the T1

- Routing (length matching, impedance, VREF) must follow the RK3566 hardware design guide and the memory datasheet, neither retrieved (**UNVERIFIED**).
- Keep the SK hynix second source footprint-compatible only if both packages match; not verified.

## Sources

- OpenDAP board, `docs/specs/bom-v1.md`, lines 8, 9, §5, §8.
- Rockchip, RK3568 Datasheet Rev 1.0, 2020-12-10; RK3566 Brief Datasheet (2022).
