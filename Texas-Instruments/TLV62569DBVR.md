# Texas Instruments TLV62569DBVR

- **Function:** 2 A synchronous step-down converter, adjustable output, SOT-23-5
- **T1 use:** board BOM v1 line 6 (Core, `vcc3v3_sys`) and line 38 (Power, `HAT_3V3`), status Proposed
- **Datasheet:** TLV62569 2-A High Efficiency Synchronous Buck Converter in SOT Package, SLVSDG1C (December 2016, revised October 2017), <https://www.ti.com/lit/ds/symlink/tlv62569.pdf>
- **Package:** SOT-23 5-pin (DBV, drawing DBV0005A)

## Summary

The TLV62569 is a 1.5 MHz synchronous buck converter with integrated 100 mΩ / 60 mΩ switches, a 2.5–5.5 V input range, power-save mode at light load, 100 % duty-cycle dropout operation and a sub-2 µA shutdown current (SLVSDG1C p. 1, §1). The DBV variant has no power-good pin (p. 3, Pin Functions). The T1 uses two: one makes `vcc3v3_sys` (3.3 V, 2 A) from VSYS for the eMMC, the RK809 VCC9 switch input and the 3.3 V logic, enabled by the RK809 `EXT_EN` (BOM line 6); the other makes `HAT_3V3` from VSYS ahead of eFuse #B (BOM line 38, power tree §3).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| VIN, EN, PG | −0.3 | 6 | V | SLVSDG1C p. 3, §6.1 |
| SW (DC) | −0.3 | VIN + 0.3 | V | p. 3, §6.1 |
| SW (AC, < 10 ns, while switching) | −3.0 | 9 | V | p. 3, §6.1 |
| FB | −0.3 | 5.5 | V | p. 3, §6.1 |
| Operating junction temperature TJ | −40 | 150 | °C | p. 3, §6.1 |
| Storage temperature | −65 | 150 | °C | p. 3, §6.1 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 4, §6.2 |
| ESD, CDM (JESD22-C101) | — | ±500 | V | p. 4, §6.2 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Input voltage VIN | 2.5 | — | 5.5 | V | SLVSDG1C p. 4, §6.3 |
| Output voltage VOUT | 0.6 | — | VIN | V | p. 4, §6.3 |
| Output current IOUT | 0 | — | 2 | A | p. 4, §6.3 |
| Junction temperature TJ | −40 | — | 125 | °C | p. 4, §6.3 |
| Feedback voltage VFB | 0.588 | 0.6 | 0.612 | V | p. 4, §6.5 |
| Switching frequency (VOUT = 2.5 V) | — | 1.5 | — | MHz | p. 5, §6.5 |
| High-side FET current limit (DBV) | — | 3 | — | A | p. 5, §6.5 |
| UVLO, VIN falling | — | 2.3 | 2.45 | V | p. 4, §6.5 |
| UVLO hysteresis | — | 100 | — | mV | p. 4, §6.5 |
| Thermal shutdown, rising / falling | — | 150 / 130 | — | °C | p. 4, §6.5 |

Thermal (DBV, p. 4, §6.4): RθJA 188.2 °C/W, RθJC(top) 137.5 °C/W, RθJB 41.2 °C/W, ψJB 40.6 °C/W.

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Shutdown | EN = 0 V, VIN = 5 V, TJ = 25 °C | 0.1 | 2 | µA | SLVSDG1C p. 4, §6.5 |
| Quiescent, not switching | VIN = 5 V, TJ = 25 °C | 35 | — | µA | p. 4, §6.5 |
| Power-save mode | light load, discontinuous inductor current | reduced switching frequency, no figure | — | — | p. 6, §7.3.1 |
| PWM | medium to heavy load | 1.5 MHz | — | — | p. 6, §7.1 |

Efficiency at VOUT = 3.3 V is given only as a curve (p. 11, Figure 9); no tabulated value.

## Pinout and package

| Pin (DBV) | Name | Type | Function |
|---|---|---|---|
| 1 | EN | I | Enable; high enables, low shuts down. Do not leave floating |
| 2 | GND | PWR | Ground |
| 3 | SW | PWR | Switch node to the inductor |
| 4 | VIN | PWR | Supply input |
| 5 | FB | I | Feedback from the external divider |

Source: SLVSDG1C p. 3, §5 Pin Functions. Marking 16AF (p. 1, Device Comparison). Body 2.90 × 2.80 mm nominal including leads (p. 1, Device Information); SOT-23, 1.45 mm maximum height (p. 21, DBV0005A). MSL 1, 260 °C peak, NiPdAu or Sn lead finish (p. 16, Orderable Addendum). Tape: 8 mm, 4 mm pitch, pin 1 in quadrant Q3, 3000 per reel (p. 18).

## Recommended footprint / land pattern

TI example board layout DBV0005A (SLVSDG1C p. 22): five pads 1.1 × 0.6 mm, pitch 0.95 mm, 1.9 mm between outer pins on a side, 2.6 mm between pad-row centres, corner radius 0.05 mm, solder mask opening 0.07 mm around each pad (non-solder-mask-defined preferred). The stencil example on the following drawing pages was not transcribed (**UNVERIFIED** values; read the drawing before making the KiCad footprint).

## Application circuit and required passives

- Output divider: VOUT = 0.6 V × (1 + R1/R2), R2 ≤ 200 kΩ (SLVSDG1C p. 9, §8.2.2.2, Equation 2). For 3.3 V: R1/R2 = 4.5; with R2 = 100 kΩ, R1 = 453 kΩ (E96) gives 3.318 V (calculation).
- Optional feed-forward capacitor C3 across R1: 6.8 pF for R2 = 100 kΩ (p. 9, §8.2.2.2).
- Input capacitor: 4.7 µF X7R/X5R is sufficient for most applications (p. 10, §8.2.2.5); example C1 = 4.7 µF 10 V X7R 0805 (p. 8, Table 3).
- Output capacitor: 10–47 µF (p. 10, §8.2.2.5); 2.2 µH with 10 µF is the standard combination recommended for most applications (p. 9, Table 4 note 3); example C2 = 10 µF 10 V X7R 0805 (p. 8, Table 3). Capacitance derating up to −50 % is anticipated in Table 4.
- Inductor: 2.2 µH; example Coilcraft XAL4020-222ME (p. 8, Table 3). Saturation current 20–30 % above IL,MAX = IOUT,MAX + ΔIL/2, with ΔIL = VOUT × (1 − VOUT/VIN) / (L × fSW) (p. 10, §8.2.2.4, Equation 3).
  - T1 calculation, VOUT = 3.3 V, L = 2.2 µH, fSW = 1.5 MHz, IOUT = 2 A: at VIN = 4.4 V, ΔIL = 0.25 A, IL,MAX = 2.13 A, so Isat ≥ 2.55–2.76 A. The DBV current limit is 3 A typ (p. 5), which a short-circuit can reach.
  - BOM line 7 pairs it with Murata DFE252012F-2R2M; check that part's saturation rating against these figures.
- Layout: input/output capacitors and inductor close to the IC, FB trace away from SW, capacitor grounds to power ground (p. 13, §10.1, Figure 20).

## Interfaces and timing

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| EN high threshold VIH (2.5 V ≤ VIN ≤ 5.5 V) | — | 0.95 | 1.2 | V | SLVSDG1C p. 4, §6.5 |
| EN low threshold VIL | 0.4 | 0.85 | — | V | p. 4, §6.5 |
| Soft-start time (DBV) | — | 800 | — | µs | p. 4, §6.5 |

The EN thresholds accept 1.8 V and 3.3 V logic. The device starts into a pre-biased output (p. 7, §7.3.3). No digital interface.

## Linux driver

None required. In the device tree the rails are `regulator-fixed` nodes: `vcc3v3_sys` with its enable owned by the RK809 `EXT_EN` (no GPIO), `HAT_3V3` with `gpio` = `HAT3V3_EN` (power tree §5). This mapping is OpenDAP's design, not a datasheet statement.

## Simulation models available

No model is listed in `manifest.toml`. The datasheet points to a WEBENCH model (SLVSDG1C p. 2, Revision History; p. 8, §8.2.2.1). Availability of a downloadable PSpice or SIMPLIS model is **UNVERIFIED**.

## Design notes for the T1

- **Dropout near VSYSMIN.** In 100 % duty cycle VIN(MIN) = VOUT + IOUT × (RDS(ON) + RL) (p. 6, §7.3.2, Equation 1). With VSYSMIN = 3.5 V and 0.1 Ω high-side RDS(ON), 3.3 V holds only while IOUT × (0.1 Ω + DCR) ≤ 0.2 V, i.e. below about 2 A minus the DCR share. At the expected `vcc3v3_sys` peak of 1.3 A (est., power tree §3) the margin is about 0.07 V minus 1.3 A × DCR. Pick a low-DCR inductor and check `vcc3v3_sys` at VSYSMIN.
- **HAT_3V3 (line 38):** the eFuse #B ILIM of 1.0 A sits below this converter's 2 A rating, so the converter is never the limiting element.
- **Thermal:** RθJA 188 °C/W is a JEDEC figure; use copper on VIN, GND and SW (p. 13, §10.3).
- **EN not floating:** both EN nets need a defined level with no software running (pull-down on `HAT3V3_EN`; RK809 `EXT_EN` drives `vcc3v3_sys`).

## Sources

- TI, TLV62569 / TLV62569P datasheet, SLVSDG1C, revised October 2017, <https://www.ti.com/lit/ds/symlink/tlv62569.pdf>, sha256 `1ba6f55dfe678d06d563acd6632f1f950a497d812270806021097b55cd81d3c4` (manifest). Page numbers are PDF page numbers.
- OpenDAP board BOM v1 lines 6, 7, 38 and power tree v0 §3, §5 (T1 context).
