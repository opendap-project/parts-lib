# Nippon DICS Pentaconn 4.4 mm jack

**Datasheet not downloaded.** Nippon DICS publishes no public drawing for the Pentaconn 4.4 mm jack; the manifest URL (<https://www.ndics.com/brands/pentaconn/>) is a brand page. The exact order number is not fixed in BOM v1. Every value below comes from BOM v1 and is **UNVERIFIED**.

- **BOM:** board BOM v1, line 31 (Audio), quoted upgrade to the primary G-Switch GT-3321667P-01

## Summary

Genuine Pentaconn 4.4 mm balanced headphone jack (Nippon DICS), available by quote only. In the T1 it is an optional upgrade on a land shared with the stocked G-Switch GT-3321667P-01, if the two drawings match (BOM v1 line 31, T1-029). All characteristics: **UNVERIFIED**.

## Absolute maximum ratings

**UNVERIFIED** (no public datasheet).

## Recommended operating conditions

**UNVERIFIED** (no public datasheet).

## Power by mode

Not applicable (passive connector).

## Pinout and package

Order number, pinout, detect switch and dimensions: **UNVERIFIED**. The BOM requires the 5-pole JEITA RC-8141C layout to be confirmed before layout (BOM v1 line 31).

## Recommended footprint / land pattern

**UNVERIFIED**. A shared land with the G-Switch part is possible only if the Pentaconn drawing matches drawing C-GT03321667P-01 (see `G-Switch/GT-3321667P-01.md`).

## Application circuit and required passives

None expected. ESD as for the primary jack (TPD1E10B06, BOM line 36).

## Interfaces and timing

Not applicable.

## Linux driver

None.

## Simulation models available

None listed in `manifest.toml`.

## Design notes for the T1

- Request the drawing from Nippon DICS with the quote, then compare it pad by pad with the G-Switch drawing.

## Sources

- OpenDAP board BOM v1, line 31; Datasheets table row "Pentaconn 4.4 mm jack".
