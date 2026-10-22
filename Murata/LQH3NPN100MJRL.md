# LQH3NPN100MJRL

- **Manufacturer:** Murata
- **Function:** 10 µH wire-wound power inductor, LQH3NP series (3 × 3 mm class, **UNVERIFIED**)
- **BOM v1 lines:** 52 (Power), TPS61169 backlight boost inductor, status Proposed
- **Package:** SMD wire-wound, dimensions **UNVERIFIED**
- **Datasheet:** Murata product page <https://www.murata.com/en-us/products/productdetail?partno=LQH3NPN100MJRL> (redirects to pim.murata.com); PDF datasheet **UNVERIFIED**
- **Status:** Datasheet not downloaded: every field UNVERIFIED. The manifest URL is a product page that redirects to pim.murata.com, which renders by script; no PDF was retrieved on 2026-10-22. Every value below comes from the OpenDAP BOM v1 or power tree v0 and is **UNVERIFIED** until the datasheet is read.

## Summary

The 10 µH inductor of the TPS61169 backlight boost (BOM line 52). The TPS61169 datasheet (SNVSA40B p. 4) accepts 4.7–10 µH. Saturation current, DCR and tolerance are **UNVERIFIED**; `M` in the MPN conventionally denotes ±20 % (**UNVERIFIED**).

## Absolute maximum ratings

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended operating conditions

L = 10 µH (BOM). Isat, Itemp, DCR, SRF **UNVERIFIED**. Requirement from the T1 calculation: peak current 0.45 A at full brightness and VIN = 3.5 V (power tree §4.5, re-derived in the TPS61169 sheet); power tree §4.5 asks for ≥ 0.6 A saturation.

## Power by mode

Loss = DCR × I²rms; input current at full brightness about 0.34 A DC (TPS61169 sheet). DCR **UNVERIFIED**.

## Pinout and package

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended footprint

Not available: datasheet not downloaded. **UNVERIFIED**

## Application circuit and required passives

Between VSYS and the TPS61169 SW pin.

## Interfaces and timing

Not applicable.

## Linux driver

None (passive part).

## Simulation models

None listed in `manifest.toml`. Vendor models **UNVERIFIED** (not checked).

## Design notes for the T1

- Confirm Isat ≥ 0.6 A and DCR before layout; the second source LQH3NPN100MMEL is listed in the BOM (**UNVERIFIED** ratings).
- Keep the SW loop short (TPS61169 SNVSA40B §7.5.1).

## Sources

- Manifest URL above (not downloaded; no sha256).
- OpenDAP board BOM v1 (2026-10-22) line 52; power tree v0 §4.5; TI TPS61169 SNVSA40B (opened, for the requirement only).
