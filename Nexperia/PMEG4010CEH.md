# PMEG4010CEH

- **Manufacturer:** Nexperia
- **Function:** 40 V, 1 A low-VF Schottky barrier rectifier (per the BOM)
- **BOM v1 lines:** 53 (Power), TPS61169 backlight boost rectifier, status Proposed
- **Package:** SOD123F (from the `EH` suffix, **UNVERIFIED**)
- **Datasheet:** PMEG4010CEH data sheet, revision and date **UNVERIFIED**, <https://assets.nexperia.com/documents/data-sheet/PMEG4010CEH.pdf>
- **Status:** Not in the current BOM (replaced in BOM v1.1 by PMEG6010CEH). Datasheet not downloaded: every field UNVERIFIED. The manifest URL returned HTTP 403 (Access Denied) to curl and to WebFetch on 2026-10-22. Every value below comes from the OpenDAP BOM v1 or power tree v0 and is **UNVERIFIED** until the datasheet is read.

## Summary

The rectifier of the TPS61169 backlight boost (BOM line 53): 40 V reverse, 1 A forward per the BOM. Forward voltage, capacitance, reverse leakage and thermal data are **UNVERIFIED**.

## Absolute maximum ratings

VR = 40 V, IF = 1 A (BOM line 53). Peak forward current, junction temperature and the exact VRRM **UNVERIFIED**.

## Recommended operating conditions

Not available: datasheet not downloaded. **UNVERIFIED**

## Power by mode

Average forward current equals the LED current (60 mA maximum); loss = VF × 60 mA, VF **UNVERIFIED**.

## Pinout and package

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended footprint

Not available: datasheet not downloaded. **UNVERIFIED**

## Application circuit and required passives

From the TPS61169 SW node to the LED anode supply (BL_LEDA) and the output capacitor.

## Interfaces and timing

Not applicable.

## Linux driver

None (discrete part).

## Simulation models

None listed in `manifest.toml`. Vendor models **UNVERIFIED** (not checked).

## Design notes for the T1

- **Reverse-voltage margin:** the TPS61169 requires the diode breakdown to exceed its open-LED protection voltage (SNVSA40B p. 12), and VOVP is up to 39 V (p. 5). A 40 V part leaves 1 V of margin; confirm the PMEG4010CEH VR rating over temperature and the ringing at SW before freezing (**UNVERIFIED**).
- Leakage at hot temperature matters only for shutdown current: the LEDs are kept dark by their 14 V forward voltage (TPS61169 sheet).
- BOM second source: onsemi NSR0340HT1G.

## Sources

- Manifest URL above (not downloaded; no sha256).
- OpenDAP board BOM v1 (2026-10-22) line 53; power tree v0 §4.5; TI TPS61169 SNVSA40B (opened, for the requirement only).
