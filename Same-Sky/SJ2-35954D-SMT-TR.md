# Same Sky SJ2-35954D-SMT-TR

**Datasheet not downloaded.** The manifest URL (<https://www.sameskydevices.com/product/resource/sj2-3595xd-smt.pdf>) returned HTTP 404 on 2026-10-22, and the PDF linked from LCSC C4992270 is the datasheet of a different part (SJ2-35364B-SMT-TR), so it was not used. Every value below comes from BOM v1 and is **UNVERIFIED** against the manufacturer's document.

- **BOM:** board BOM v1, line 30 (Audio), quantity 1
- **Second source (BOM):** SJ2-35894D-SMT-TR

## Summary

3.5 mm audio jack, surface mount, with a detect switch (BOM v1 line 30). In the T1 it is the single-ended headphone output, driven by two OPA1622 packages; its detect switch is read through the TCA6416A GPIO expander (BOM v1 line 30, pin plan §2.1). All part characteristics: **UNVERIFIED**.

## Absolute maximum ratings

**UNVERIFIED** (datasheet not downloaded).

## Recommended operating conditions

**UNVERIFIED** (datasheet not downloaded).

## Power by mode

Not applicable (passive connector).

## Pinout and package

Number of poles, pin numbering, detect-switch type and mechanical dimensions: **UNVERIFIED** (datasheet not downloaded).

## Recommended footprint / land pattern

**UNVERIFIED** (datasheet not downloaded).

## Application circuit and required passives

None expected for a connector. In the T1 the L, R and detect lines carry TPD1E10B06 ESD diodes (BOM line 36).

## Interfaces and timing

Not applicable.

## Linux driver

None for the jack itself. Jack detection is exposed through the TCA6416A GPIO with `gpio-keys` or the `simple-audio-card` jack-detect GPIO (BOM v1 line 30); the binding choice is **UNVERIFIED**.

## Simulation models available

None listed in `manifest.toml`.

## Design notes for the T1

- Obtain the SJ2-3595xD-SMT datasheet from Same Sky before drawing the footprint.
- The BOM note on paralleling OPA1622 halves for 16 Ω loads on this output is **UNVERIFIED** (see `Texas-Instruments/OPA1622IDRCR.md`).

## Sources

- OpenDAP board BOM v1, lines 30 and 36; Datasheets table row "SJ2-35954D-SMT-TR".
