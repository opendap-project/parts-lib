# Texas Instruments TPS61088RHLR

> **Datasheet not downloaded.** On 2026-10-22 TI returned **HTTP 404** for both the datasheet URL and the product page `ti.com/product/TPS61088` (the TPS61089 URLs still answer 200). The part's status at TI is therefore unknown and must be checked before it stays in the BOM. Every value below comes from the OpenDAP BOM v1 or power tree v0 and is **UNVERIFIED** until the datasheet is read.

- **Function:** synchronous boost converter, used at 5.1 V output from VSYS (per the BOM)
- **T1 use:** board BOM v1 line 91 (Power), HAT_5V and USB-C VBUS source boost ahead of eFuses #A and #C; inductor line 92; status Proposed (new)
- **Datasheet:** TPS61088 datasheet, revision and date **UNVERIFIED**, <https://www.ti.com/lit/ds/symlink/tps61088.pdf>
- **Package:** VQFN (RHL) from the MPN suffix; pin count and size **UNVERIFIED**

## Summary

In the T1 the TPS61088 boosts VSYS to 5.1 V for HAT_5V (eFuse #A) and the USB-C VBUS source (eFuse #C), replacing the BQ25895 OTG boost that cannot run while charging (BOM line 91, power tree finding 9). It is enabled by `HAT5V_EN` OR `USB_SRC_ON`, and it is not a load-disconnect boost, so the eFuses stay off when idle (BOM line 91). Every electrical figure is **UNVERIFIED**.

## Absolute maximum ratings

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended operating conditions

VIN = VSYS 3.5–4.4 V, VOUT = 5.1 V (BOM line 91, power tree §3). Input range, switch current limit, switching frequency and output current capability **UNVERIFIED**.

## Power by mode

Shutdown and quiescent currents **UNVERIFIED**. Load case from the T1: up to 1.5 A + 1.5 A at 5.1 V (eFuse ceilings), about 0.7 A on battery by software budget (power tree §4.6); input current calculations are in the XAL4020-152MEC sheet.

## Pinout and package

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended footprint / land pattern

Not available: datasheet not downloaded. **UNVERIFIED**

## Application circuit and required passives

- Inductor 1.5 µH, Isat ≥ 6 A: Coilcraft XAL4020-152MEC (BOM line 92; value from the datasheet example, **UNVERIFIED**).
- Feedback divider for 5.1 V, input and output capacitors, compensation and ILIM resistor (if any): **UNVERIFIED**.

## Interfaces and timing

EN from a hardware OR of `HAT5V_EN` and `USB_SRC_ON` (BOM line 91). EN thresholds, soft-start time and light-load mode selection **UNVERIFIED**.

## Linux driver

None (no register interface). In the device tree the 5.1 V rail is a `regulator-fixed` supply of the eFuse-switched outputs; modelling is OpenDAP's design.

## Simulation models available

None listed in `manifest.toml`. Vendor models **UNVERIFIED** (not checked).

## Design notes for the T1

- **Availability:** the 404 on TI's datasheet and product pages (2026-10-22) is the first thing to resolve: confirm whether the part is still active, renamed or discontinued, and re-check the BOM second source (TI TPS61022, rejected on stock).
- **No load disconnect:** with EN low the output is still connected to VSYS through the inductor and the high-side path in a conventional boost (**UNVERIFIED** for this part); the eFuses #A and #C are what isolate HAT_5V and VBUS (BOM line 91).
- **Self-feed interlock:** the same nets that enable the boost force TPS2121 OV1/OV2 (power tree §4.6, finding 10).

## Sources

- Manifest URL above (HTTP 404 on 2026-10-22; no sha256).
- OpenDAP board BOM v1 (2026-10-22) lines 91–92; power tree v0 §2–4.6.
