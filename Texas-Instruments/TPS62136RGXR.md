# TPS62136RGXR

- **Manufacturer:** Texas Instruments
- **Function:** 4 A synchronous step-down converter, 3–17 V input, adjustable 0.8–12 V output, DCS-Control, 1 MHz, 100 % mode, power-good output, output discharge
- **BOM v1 lines:** 113 (Power, pre-regulator VSYS → VSYS_LV 3.8 V, qty 1; new in BOM v1.5, board ADR 0014); inductor on line 114 ([XGL4020-152MEC](../Coilcraft/XGL4020-152MEC.md)); passives on line 115
- **Package:** VQFN-HR-11 (RGX0011A), 3.0 × 2.0 mm nominal, 1 mm maximum height
- **Datasheet:** *TPS62136, TPS621361 1-MHz High Accuracy 3-V to 17-V 4-A Step-Down Converters with DCS-Control*, SLVSDV2, March 2017 (initial release, no later revision listed), 46 pages with the addendum. Cited below as "SLVSDV2". File sha256 `b445aeace2de2d6b9f657bb692104d848c17b8158f727f8e15a6ac738a13a70a`.
- **Status:** Partly UNVERIFIED

## Summary

The TPS62136 is a synchronous buck converter for multi-cell Li-ion and 12 V rails: 3–17 V input, 4 A continuous output, 0.8–12 V output set by a divider (VFB 0.7 V), ±1 % output accuracy in PWM, 18 µA quiescent current, power-save mode at light load, 100 % duty-cycle mode, adjustable soft start and tracking, power good, VSEL/FB2 output-voltage scaling, active output discharge and hiccup current limit (SLVSDV2, pp. 1, 3). In the T1 it makes VSYS_LV, a fixed 3.8 V rail from the 2S VSYS (6.0–8.8 V), and feeds every part the 1S power tree fed from VSYS (board BOM v1.5 line 113; board 2S study §4.2).

## Absolute maximum ratings

SLVSDV2, p. 4, §7.1. Voltages to ground.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN | −0.3 | 20 | V |
| SW, VOS | −0.3 | VIN + 0.3 | V |
| SW (transient < 10 ns, while switching) | −2 | 25.5 | V |
| EN, MODE, VSEL, PG, FB, FB2, SS/TR | −0.3 | VIN + 0.3 | V |
| Operating TJ | −40 | 150 | °C |
| Tstg | −65 | 150 | °C |

ESD (SLVSDV2, p. 4, §7.2): HBM ±2000 V; CDM ±500 V.

## Recommended operating conditions

SLVSDV2, p. 4, §7.3.

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | 3 | | 17 | V |
| VOUT | 0.8 | | 12 | V |
| Effective inductance | 0.7 | 1.5 | 2.9 | µH |
| Effective output capacitance | 12 | 47 | 200 | µF |
| Effective input capacitance | 3 | 10 | | µF |
| TJ | −40 | | 125 | °C |

Thermal (SLVSDV2, p. 5, §7.4; JEDEC 51-5 4-layer board with 6 thermal vias): RθJA 38.4 °C/W, RθJC(top) 2.0 °C/W, RθJB 7.6 °C/W, ψJT 0.1 °C/W, ψJB 7.6 °C/W, RθJC(bot) 3.2 °C/W.

## Power by mode

SLVSDV2, p. 5, §7.5 (TJ −40 to 125 °C, VIN 3–17 V; typical at VIN 12 V, 25 °C).

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Quiescent | EN high, no load, not switching | 18 | 46 | µA |
| Quiescent | as above, TJ 85 °C | | 35 | µA |
| Shutdown | EN low (max at TJ 85 °C) | 1 | 8 | µA |

- Power-save mode (MODE low): the device enters PFM below half the inductor ripple; TON = 250 ns × VIN / (VIN − VOUT) (SLVSDV2, p. 10, Eq. 1–2). It stays in PWM when VIN falls to about 15 % above VOUT.
- 100 % duty cycle: the high-side switch stays on as VIN approaches VOUT (SLVSDV2, p. 10, §9.4.3).

## Pinout and package

SLVSDV2, p. 3, pin functions.

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | VIN | P | Supply input |
| 2 | SW | P | Switch node |
| 3 | GND | P | Ground |
| 4 | FB2 | O | Open drain to GND when VSEL is high (output scaling) |
| 5 | FB | I | Feedback divider input |
| 6 | VOS | I | Output sense, to the output capacitor |
| 7 | PG | O | Open-drain power good |
| 8 | EN | I | Enable; never floating |
| 9 | SS/TR | I | Soft-start capacitor or tracking input |
| 10 | MODE | I | Low: PFM/PWM; high: forced PWM; never floating |
| 11 | VSEL | I | Turns FB2 on when high |

Device options (SLVSDV2, p. 3, §5): TPS62136RGX has output discharge and hiccup current limit; TPS621361RGX has no output discharge. Ordering (SLVSDV2, package option addendum, p. 38): TPS62136RGXR 3000 per reel, TPS62136RGXT 250 per reel, MSL 1 at 260 °C (unlimited), −40 to 125 °C, marking 62136.

## Recommended footprint

TI outline, example land pattern and stencil for RGX0011A: SLVSDV2, pp. 42–44. Not transcribed here: **UNVERIFIED** until the footprint is drawn against those pages. Layout guidance and example: SLVSDV2, p. 34 (§12.1–§12.2); thermal considerations p. 35 (§12.3).

## Application circuit and required passives

SLVSDV2, p. 7, Table 1 (measurement setup) and pp. 13–14, 17:

| Ref | Value | Note |
|---|---|---|
| L | 1.5 µH | Coilcraft XEL4020-152 in Table 1; 1.5 or 2.2 µH nominal (§10.1.3) |
| CIN | 10 µF, 25 V, 0805 | 10 µF nominal recommended (§10.1.4.2) |
| COUT | 2 × 22 µF, 16 V, 0805 | 47 µF nominal recommended (§10.1.4.1); Table 2: 1.5 µH with 47 µF is the standard combination |
| CSS | 3.3 nF in Table 1 | Soft-start: 2.5 µA source current (§10.1.4.3, p. 15) |
| R1, R2 | per Eq. 8 | R1 = R2 × (VOUT / 0.7 V − 1); R2 ≤ 400 kΩ for ≥ 2 µA divider current (p. 13) |
| R3 | 470 kΩ | PG pull-up |

- **Inductor selection** (SLVSDV2, pp. 13–14, Eq. 9–10): IL(max) = IOUT(max) + ΔIL(max) / 2, ΔIL(max) = VIN(max) / L(min) × 100 ns; saturation current with about 20 % margin. Table 3 (p. 14) lists XEL4020-152ME, XFL4020-152ME, XEL4030-152ME, XEL4030-222ME and Murata DFE322512F-1R5M.
- **For 3.8 V:** R1 = 4.43 × R2; with R2 = 100 kΩ, R1 = 442 kΩ (E96) gives 3.794 V (calculated; not a Table 5 entry).

## Interfaces and timing

- EN threshold 0.77 / 0.8 / 0.83 V rising, 0.67 / 0.7 / 0.73 V falling; MODE and VSEL VIH 0.9 V, VIL 0.3 V; leakage ≤ 100 nA (SLVSDV2, p. 5).
- UVLO 2.8 / 2.9 / 3.0 V rising, 2.5 / 2.6 / 2.7 V falling (p. 5).
- Power good 93 / 96 / 98 % rising, 3–4.5 % hysteresis; VOL 0.3 V max at 2 mA (p. 5).
- High-side and low-side current limits 4.8 / 5.6 / 6.5 A (dc); negative current limit 1.5 A (p. 6).
- RDS(on) 100 / 180 mΩ high side, 39 / 67 mΩ low side (typ / max, VIN ≥ 4 V) (p. 6).
- VFB 0.7 V, ±1 % in PWM with VIN ≥ VOUT + 1 V (p. 6). fSW 1 MHz typ (p. 6).
- Thermal shutdown 160 °C, 20 °C hysteresis (p. 5).

## Linux driver

None. Always-on `regulator-fixed` supply (EN tied to VSYS); VSEL unused.

## Simulation models

The datasheet points to TI WEBENCH; PSpice or TINA models on ti.com were not checked: **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **Why it is there (board ADR 0014):** every part the 1S tree fed from VSYS is rated ≤ 5.5 V (6.5 V for the TPS62840), and the 2S VSYS spans 6.0–8.8 V (OVP up to ≈ 9.9 V). VSYS_LV at 3.8 V keeps every one of them inside the range it was chosen for (board 2S study §4.2).
- **Margin (BRD-049):** ≈ 1.6 A continuous and 2 A peak (est.) = 40–50 % of 4 A; with a 3 W system and the full-scale balanced 32 Ω headphone sine, ≈ 2.05 A = 51 % (board power tree §4.7). VIN ≤ 9.9 V = 58 % of the 17 V maximum.
- **Inductor:** 1.5 µH; the XGL4020-152MEC (line 114) carries a 3.03 A peak at 2 A (VSYS 9.9 V, L −20 %), 40 % of its 7.5 A Isat (30 % drop), and stays above the 6.5 A maximum current limit; the switch peak is 63 % of the 4.8 A minimum limit. Eq. 10 (100 ns) understates the ripple; ΔIL = 250 ns × VIN / L from the Eq. 1 on-time, confirmed by TI's model ([boost and MaskROM simulation](https://github.com/opendap-project/board/blob/main/docs/research/2026-10-boost-and-maskrom-simulation.md) §4.2; board BOM v1.6 correction of the 2.41 A figure). It is not in Table 3; the listed XEL4020-152MEC is its second source. Loop with TI's model: 49° phase margin at VSYS 6.0 V, 54° at 8.8 V.
- **Dropout:** with VIN ≥ 6.0 V and VOUT 3.8 V the converter never reaches 100 % mode on battery.
- **Thermal:** ≈ 0.5 W at the 6 W peak system load (board 2S study §6, est.) → ≈ +19 °C at 38.4 °C/W (JEDEC board; the T1 board differs).
- **Quiescent cost:** 18 µA typ at 7.4 V ≈ 0.13 mW (board 2S study §4.3).

## Sources

- TI, TPS62136/TPS621361 datasheet, SLVSDV2 (March 2017): <https://www.ti.com/lit/ds/symlink/tps62136.pdf>
- OpenDAP board ADR 0014 and BOM v1.5, lines 113–115; power tree v0 §2, §3, §4.7, §4.10; board 2S battery study §4.2–§4.4, §6 (`public/board/docs/`).
