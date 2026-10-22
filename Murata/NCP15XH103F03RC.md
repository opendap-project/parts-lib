# Murata NCP15XH103F03RC

> **Datasheet not downloaded.** The manifest URL is a product page that redirects to pim.murata.com, which renders by script; no PDF was retrieved on 2026-10-22. Every value below comes from the OpenDAP BOM v1 or power tree v0 and is **UNVERIFIED** until the datasheet is read.

- **Function:** 10 kΩ NTC thermistor, 0402, B = 3380 K (per the BOM)
- **T1 use:** board BOM v1 line 48 (Power, battery NTC on the BQ25895 TS pin) and line 101 (optional MAX17055 TH thermistor), status Proposed
- **Datasheet:** Murata product page <https://www.murata.com/en-us/products/productdetail?partno=NCP15XH103F03RC> (redirects to pim.murata.com); PDF datasheet **UNVERIFIED**
- **Package:** 0402 (1005 metric) chip NTC (`15` size code, **UNVERIFIED**)

## Summary

A 10 kΩ NTC pressed against the battery pocket floor and wired to the BQ25895 TS divider, chosen with B = 3380 K (BOM line 48); a second one is optional on the MAX17055 TH input (line 101). The 1 % resistance tolerance follows from the `F` in the MPN; B-constant tolerance, dissipation constant and thermal time constant are **UNVERIFIED**.

## Absolute maximum ratings

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended operating conditions

R25 = 10 kΩ, B = 3380 K (BOM line 48). B-constant reference temperatures (25/50 °C or 25/85 °C), tolerances and operating temperature range **UNVERIFIED**.

## Power by mode

Self-heating depends on the divider current from REGN; the dissipation constant needed to bound the error is **UNVERIFIED**.

## Pinout and package

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended footprint / land pattern

Not available: datasheet not downloaded. **UNVERIFIED**

## Application circuit and required passives

Lower leg of the BQ25895 TS divider (RT1/RT2 from REGN), sized so the fixed TS thresholds stop charging at or below 40 °C (see the BQ25895 sheet and the Adafruit 328 sheet).

## Interfaces and timing

Thermal time constant **UNVERIFIED**; it sets how quickly a warming pack is detected through the pocket floor.

## Linux driver

None for the part. Temperature reaches Linux through the `bq25890_charger` status (TS fault) and, if fitted on TH, the MAX17055 driver.

## Simulation models available

None listed in `manifest.toml`. Vendor models **UNVERIFIED** (not checked).

## Design notes for the T1

- The TS divider must be computed from the real R–T table of this part; take it from Murata's R–T data, not from the nominal B value alone (**UNVERIFIED**).
- Thermal coupling to the pouch is mechanical (pocket floor contact), see power tree §4.7.

## Sources

- Manifest URL above (not downloaded; no sha256).
- OpenDAP board BOM v1 (2026-10-22) lines 48, 101; power tree v0 §4.7.
