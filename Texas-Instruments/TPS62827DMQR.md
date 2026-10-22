# TPS62827DMQR

- **Manufacturer:** Texas Instruments
- **Function:** 4 A synchronous step-down converter, 2.5–5.5 V input, adjustable 0.6–4.0 V output, power save mode, power-good output, 100 % duty cycle
- **BOM v1 lines:** 6 (named alternative to the TPS62826DMQR for vcc3v3_sys, the drop-in if the schematic re-sum exceeds 2.4 A; not placed)
- **Package:** VSON-HR-6 (DMQ0006A), 1.5 × 1.5 mm nominal, 0.5 mm pitch, 1.0 mm max height
- **Datasheet:** *TPS6282x 2.4V to 5.5V Input, 1, 2, 3, 4A Step-Down Converter With 1% Output Accuracy*, SLVSEF9I, March 2018, revised March 2024. Cited below as "SLVSEF9I". File sha256 `8a309f2a40486a380242d3f178eb4bda3ef4dca3deca647fa82f763d14866f63` (matches the BOM v1 Datasheets table).
  - Same datasheet as [TPS62826DMQR](TPS62826DMQR.md); values common to the family are given in full there and repeated here only where the TPS62827 differs or the T1 needs them.
- **Status:** Partly UNVERIFIED

## Summary

TPS62827DMQ is the adjustable-output, PSM/PWM, 4 A member of the TPS6282x family (SLVSEF9I, p. 3, §4): DCS-Control, 4 µA quiescent current, 1 % feedback accuracy, 26 mΩ / 25 mΩ switches, 2.2 MHz, 100 % duty cycle, power good, hiccup short-circuit protection (p. 1). The family is pin-to-pin and BOM-to-BOM compatible (p. 1), but the TPS62827 has a higher minimum input voltage, a longer soft start, a higher current limit and a larger minimum output capacitance than the TPS62826 (pp. 4–6, 13–14). In the T1 it is the fallback for vcc3v3_sys if the schematic re-sum exceeds 2.4 A (BOM v1 line 6; Changes in v1.2 item 1).

## Absolute maximum ratings

Same as the TPS62826DMQR (SLVSEF9I, p. 4, §6.1): VIN, FB, EN, PG −0.3 to 6 V; SW −0.3 to VIN + 0.3 V DC (−1.0 V in current limit), −2.5 to 10 V for < 10 ns; TJ −40 to 150 °C; Tstg −65 to 150 °C. ESD HBM ±2000 V, CDM ±500 V (p. 4, §6.2).

## Recommended operating conditions

SLVSEF9I, p. 4, §6.3.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN (TPS62827x) | 2.5 | 5.5 | V |
| VOUT | 0.6 | 4.0 | V |
| IOUT (TPS62827x) | 0 | 4 | A |
| PG sink current | | 1 | mA |
| PG pull-up voltage | | 5.5 | V |
| TJ | −40 | 125 | °C |

Thermal (SLVSEF9I, pp. 4–5, §6.4; family figures, EVM column measured on the TPS62826EVM-794): RθJA 129.5 °C/W JEDEC, 71.4 °C/W EVM; RθJB 33.1 °C/W; ψJT 3.8 °C/W.

## Power by mode

SLVSEF9I, p. 5, §6.5; typical at 25 °C and VIN = 5 V.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | EN low, TJ −40 to 85 °C | 0.05 | 0.5 | µA |
| Quiescent | EN high, no load, not switching | 4 | 10 | µA |

PSM at light load, 100 % mode below dropout: VIN,min = VOUT + IOUT,MAX × (RDS(on) + RL) (SLVSEF9I, p. 9, §7.3.2–7.3.3, Eq. 3).

## Pinout and package

Same as the TPS62826DMQR: VSON-HR-6, DMQ0006A (SLVSEF9I, p. 32); pin 1 EN, 2 PG, 3 FB, 4 GND, 5 SW, 6 VIN (p. 3, Table 5-1). Ordering (SLVSEF9I, p. 27, addendum): TPS62827DMQR, 3000 per reel, Sn finish, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking EH.

## Recommended footprint

Same land pattern as the TPS62826DMQR (SLVSEF9I, p. 33; stencil p. 34): one footprint serves both parts. Pad-to-pin mapping of the long and short pads **UNVERIFIED** until drawn against p. 33 (see the TPS62826DMQR sheet).

## Application circuit and required passives

Typical application (SLVSEF9I, p. 11, Figure 8-2; p. 12, Table 8-2):

| Ref | Value | Note |
|---|---|---|
| C1 (input) | 4.7 µF, 6.3 V, X7R, 0603 | Minimum effective input capacitance 3 µF (p. 14) |
| C2 (output) | 3 × 10 µF, 10 V, X7R, 0603 | Minimum effective output capacitance **20 µF** for the TPS62827 (p. 14) |
| C3 (feedforward) | 120 pF | C3 = 12 µ / R2 (p. 12, Eq. 5) |
| L1 | 0.47 µH | Recommended (p. 13, Table 8-4) |
| R1, R2, R3 | per Eq. 4; 100 kΩ; 100 kΩ | As for the TPS62826 (p. 12) |

- **L–C matrix for the TPS62827** (SLVSEF9I, p. 13, Table 8-4): with 0.47 µH, COUT 22 µF (standard, recommended), 3 × 10 µF and 47 µF nominal are proven. **2 × 10 µF is not a listed combination** for the TPS62827 (it is for the TPS62826, Table 8-3).
- Inductor: IL,MAX = IOUT,MAX + ΔIL / 2 (p. 13, Eq. 6); saturation current about 20–30 % above IL,MAX.

## Interfaces and timing

Differences from the TPS62826 (SLVSEF9I, pp. 5–6):

- Soft start 1.75 ms from EN high to 95 % of VOUT (TPS62826: 1.25 ms).
- High-side current limit 4.8 / 5.6 / 6.4 A (TPS62826: 3.7 / 4.3 / 5.0 A).

Common to both: EN VIH 1.0 V, VIL 0.4 V; UVLO 2.1 / 2.2 / 2.3 V falling, 160 mV hysteresis; PG window 92 % falling / 96 % rising (lower), 105 % falling / 110 % rising (upper), typical; VFB 600 mV ±1 %; fSW 2.2 MHz; thermal shutdown 150 °C (pp. 5–6). Note: the TPS62827 UVLO maximum (2.3 V) and its 2.5 V minimum recommended VIN leave the 2.4–2.5 V band outside the recommended range.

## Linux driver

None. Would be described as a `regulator-fixed` always-on supply, as for the TPS62826DMQR.

## Simulation models

- The datasheet names only the WEBENCH Power Designer (SLVSEF9I, p. 24, §9.1.2). PSpice/TINA models on ti.com: **UNVERIFIED**.

## Design notes for the T1

- **Drop-in condition:** BOM v1 line 6 and power tree v0 (open point 11, vcc3v3_sys peak) call the TPS62827 "pin- and BOM-compatible". The pinout and footprint are identical (p. 3), but the output capacitor is not the same: the TPS62827 needs ≥ 20 µF effective and is proven with 22 µF or 3 × 10 µF, not 2 × 10 µF (SLVSEF9I, p. 13, Table 8-4; p. 14). Lay out vcc3v3_sys with a single 22 µF or with a footprint for a third 10 µF so the swap stays a part change only.
- **Inductor:** the 6.4 A maximum current limit (p. 6) is below the DFE252012F-R47M 6.7 A inductance-based rating but above its 4.9 A thermal rating (per its sheet). Under a short circuit the inductor sees up to the current limit in hiccup bursts (p. 10, §7.3.5).
- **Input range:** 2.5 V minimum (p. 4); VSYS stays above that in all T1 operating states listed in the power tree (**UNVERIFIED** against the final battery cut-off).
- **Soft start:** 1.75 ms instead of 1.25 ms (p. 5); vcc3v3_sys is always on, so only the first power-up timing changes.

## Sources

- TI, TPS6282x datasheet, SLVSEF9I (March 2024): <https://www.ti.com/lit/ds/symlink/tps62826.pdf>
- OpenDAP board BOM v1 (v1.2), line 6, Changes in v1.2 item 1; power tree v0 rail table and open points (`public/board/docs/specs/`).
