# TPS62826DMQR

- **Manufacturer:** Texas Instruments
- **Function:** 3 A synchronous step-down converter, 2.4–5.5 V input, adjustable 0.6–4.0 V output, power save mode, power-good output, 100 % duty cycle
- **BOM v1 lines:** 6 (vcc3v3_sys 3.3 V system buck, always on, qty 1; v1.2, replaces TLV62569DBVR); its inductor is the DFE252012F-R47M on line 4
- **Package:** VSON-HR-6 (DMQ0006A), 1.5 × 1.5 mm nominal, 0.5 mm pitch, 1.0 mm max height
- **Datasheet:** *TPS6282x 2.4V to 5.5V Input, 1, 2, 3, 4A Step-Down Converter With 1% Output Accuracy*, SLVSEF9I, March 2018, revised March 2024. Cited below as "SLVSEF9I". File sha256 `8a309f2a40486a380242d3f178eb4bda3ef4dca3deca647fa82f763d14866f63` (matches the BOM v1 Datasheets table). The downloaded copy carries a package option addendum dated 31-Oct-2025 and package materials pages dated 3-Sep-2026.
  - Same datasheet as [TPS62827DMQR](TPS62827DMQR.md).
- **Status:** Partly UNVERIFIED

## Summary

The TPS6282x is a family of DCS-Control synchronous step-down converters with 4 µA quiescent current, 1 % feedback accuracy over −40 to 125 °C, 26 mΩ / 25 mΩ internal switches, 2.2 MHz switching, power save mode at light load, 100 % duty cycle, active output discharge, power-good output, thermal shutdown and hiccup short-circuit protection; the family members are pin-to-pin and BOM-to-BOM compatible (SLVSEF9I, p. 1). TPS62826DMQ is the adjustable-output, PSM/PWM, 3 A member (SLVSEF9I, p. 3, §4). In the T1 it makes vcc3v3_sys (3.3 V, always on) from VSYS and feeds RK809-5 VCC5–VCC9, the eMMC, the RP2354A and FP_3V3 (BOM v1 line 6; power tree v0 §2, rail table).

## Absolute maximum ratings

SLVSEF9I, p. 4, §6.1. Voltages to ground.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN, FB, EN, PG | −0.3 | 6 | V |
| SW (DC) | −0.3 | VIN + 0.3 | V |
| SW (DC, in current limit) | −1.0 | VIN + 0.3 | V |
| SW (AC, < 10 ns, while switching) | −2.5 | 10 | V |
| SW (AC, PFM mode, < 100 ns, while switching) | −1.0 | VIN + 1.0 | V |
| Operating junction TJ | −40 | 150 | °C |
| Storage Tstg | −65 | 150 | °C |

- After disabling the device, the SW voltage may exceed the minimum until the inductor and output capacitor are discharged (SLVSEF9I, p. 4, note 4).
- ESD (SLVSEF9I, p. 4, §6.2): HBM ±2000 V; CDM ±500 V.

## Recommended operating conditions

SLVSEF9I, p. 4, §6.3.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN (TPS62824x, TPS62825x, TPS62826x) | 2.4 | 5.5 | V |
| VOUT | 0.6 | 4.0 | V |
| IOUT (TPS62826x) | 0 | 3 | A |
| PG sink current | | 1 | mA |
| PG pull-up voltage | | 5.5 | V |
| TJ | −40 | 125 | °C |

Thermal (SLVSEF9I, pp. 4–5, §6.4):

| Metric | JEDEC | TPS62826EVM-794 | Unit |
|---|---|---|---|
| RθJA | 129.5 | 71.4 | °C/W |
| RθJC(top) | 103.9 | n/a | °C/W |
| RθJB | 33.1 | n/a | °C/W |
| ψJT | 3.8 | 3.9 | °C/W |
| ψJB | 33.1 | 38.6 | °C/W |

## Power by mode

SLVSEF9I, p. 5, §6.5; TJ −40 to 125 °C, VIN 2.4–5.5 V; typical at 25 °C and VIN = 5 V.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | EN low, TJ −40 to 85 °C | 0.05 | 0.5 | µA |
| Quiescent | EN high, no load, not switching | 4 | 10 | µA |
| Quiescent, forced-PWM (A) versions only | EN high, no load | 8 | — | mA |

- Light load: the device enters power save mode when the output current falls below half the inductor ripple current; the switching frequency then falls with the load (SLVSEF9I, p. 9, §7.3.2, Eq. 2). Above 90 % duty cycle it cannot enter PSM and stays in PWM (p. 9).
- 100 % mode: the high-side switch stays on; minimum input VIN,min = VOUT + IOUT,MAX × (RDS(on) + RL) (SLVSEF9I, p. 9, §7.3.3, Eq. 3).
- Efficiency up to 97 % (SLVSEF9I, p. 1); curves for VIN = 5 V on p. 1 and in §8.2.3.

## Pinout and package

VSON-HR-6, DMQ0006A, 1.45–1.55 mm × 1.45–1.55 mm, 0.8–1.0 mm height, 0.5 mm pitch (SLVSEF9I, p. 32, drawing 4222645/E 09/2023).

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | EN | I | Enable; high enables, low disables; do not leave floating |
| 2 | PG | O | Power-good, open drain; pull-up to ≤ 5.5 V; leave floating if unused |
| 3 | FB | I | Feedback; on fixed-output versions connect to the output |
| 4 | GND | | Ground |
| 5 | SW | PWR | Switch node |
| 6 | VIN | PWR | Input |

(SLVSEF9I, p. 3, Figure 5-1 and Table 5-1.) Ordering (SLVSEF9I, p. 27, addendum): TPS62826DMQR, 3000 per reel, Sn finish, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking CL. Tape: 8 mm, 4 mm pitch, pin 1 in Q2 (p. 30).

## Recommended footprint

SLVSEF9I, p. 33 (DMQ0006A example board layout) and p. 34 (stencil, 0.125 mm thick):

- Six pads, pitch (0.5) mm; three pads (1) mm long and three (0.6) mm long; pad widths (0.25) mm and (0.2) mm; reference dimensions (0.65) and (0.45) mm. Which pins take the long pads is read from the drawing, not stated in the text: **UNVERIFIED** until the footprint is drawn against p. 33.
- Non-solder-mask-defined pads preferred, 0.05 mm mask clearance all around.
- Stencil apertures equal to the pads on p. 34.
- No exposed thermal pad. Heat leaves through the pins: wide copper planes on the pads (SLVSEF9I, p. 23, §8.4.2.1).

## Application circuit and required passives

Typical application (SLVSEF9I, p. 11, Figure 8-1; p. 12, Table 8-2):

| Ref | Value | Note |
|---|---|---|
| C1 (input) | 4.7 µF, 6.3 V, X7R, 0603 | Minimum effective input capacitance 3 µF (p. 14, §8.2.2.5) |
| C2 (output) | 2 × 10 µF, 10 V, X7R, 0603 | Minimum effective output capacitance 10 µF for TPS62826x (p. 14) |
| C3 (feedforward) | 120 pF | C3 = 12 µ / R2 (p. 12, Eq. 5); required on the adjustable version |
| L1 | 0.47 µH | Standard value (p. 13, Table 8-3) |
| R1 | per Eq. 4 | R1 = R2 × (VOUT / 0.6 V − 1) (p. 12, Eq. 4) |
| R2 | 100 kΩ | Must not exceed 100 kΩ (p. 12) |
| R3 (PG pull-up) | 100 kΩ | |

- **L–C matrix** (SLVSEF9I, p. 13, Table 8-3): 0.47 µH is the only proven inductance; with it, COUT 10, 2 × 10 or 22 (standard, recommended) and 47 µF nominal are proven. Effective L may vary +20 / −30 %, effective C +20 / −35 %.
- **Inductor current** (SLVSEF9I, p. 13, Eq. 6): IL,MAX = IOUT,MAX + ΔIL / 2, ΔIL = VOUT × (1 − VOUT / VIN) / (L × fSW). Choose saturation current about 20–30 % above IL,MAX. Table 8-5 lists recommended 0.47 µH parts (Cyntec, Murata DFE201610E-R47M and DFE201210S-R47M, TDK, Coilcraft, Würth); the DFE252012F-R47M used in the T1 is not in that list.
- **For 3.3 V:** with R2 = 100 kΩ, Eq. 4 gives R1 = 450 kΩ (derived; nearest E96 value to be chosen in the schematic). TPS6282533 is a fixed 3.3 V version, but it is a 2 A part (p. 3, §4), so it does not replace the 3 A adjustable device.
- Layout: input and output capacitors and inductor as close as possible to the IC; capacitor grounds to the GND pin; FB trace away from SW, sensed at the output capacitor (SLVSEF9I, p. 22, §8.4.1; p. 23, Figure 8-49).

## Interfaces and timing

- EN: VIH 1.0 V min, VIL 0.4 V max (SLVSEF9I, p. 5); typical thresholds 0.9 V rising, 0.7 V falling (p. 10, §7.4.1). Leakage 0.01 / 0.1 µA.
- Soft start: 1.25 ms from EN high to 95 % of VOUT (TPS62824x/5x/6x/7A) (SLVSEF9I, p. 5); the ramp starts about 250 µs after EN; starts into a prebiased output (p. 9, §7.3.4).
- UVLO: VIN falling 2.1 / 2.2 / 2.3 V, hysteresis 160 mV (SLVSEF9I, p. 5).
- Power good (SLVSEF9I, p. 5; p. 10, Table 7-1): lower threshold 94 / 96 / 98 % rising, 90 / 92 / 94 % falling; upper threshold 108 / 110 / 112 % rising, 103 / 105 / 107 % falling; VOL 0.4 V at 1 mA; 100 µs rising blanking, 20 µs falling deglitch. PG is low when disabled, in UVLO or thermal shutdown.
- Output: VFB 594 / 600 / 606 mV in PWM; FB leakage 0.05 µA max; load regulation 0.1 %/A (1.8 V, 0.5–3 A) (SLVSEF9I, p. 5).
- Output discharge 75 / 400 mA through SW with EN low; needs VIN present (SLVSEF9I, p. 5; p. 10).
- Switches: 26 mΩ high side, 25 mΩ low side, typical (SLVSEF9I, p. 5).
- High-side current limit (TPS62826x): 3.7 / 4.3 / 5.0 A (SLVSEF9I, p. 6). Propagation delay about 60 ns lets the AC peak exceed it (p. 9).
- Hiccup: after 32 cycles in current limit (about 13 µs), high side off for about 100 µs, then soft-start again (SLVSEF9I, p. 10, §7.3.5).
- fSW 2.2 MHz typ (IOUT 1 A, VOUT 1.8 V) (SLVSEF9I, p. 6); PWM on-time TON = VOUT / VIN × 450 ns (p. 9, Eq. 1).
- Thermal shutdown 150 °C, hysteresis 20 °C (SLVSEF9I, p. 5).

## Linux driver

None. EN tied to VSYS (always on). Describe as a `regulator-fixed` always-on supply (BOM v1 line 6: driver path *none*).

## Simulation models

- The datasheet names only the WEBENCH Power Designer (SLVSEF9I, p. 24, §9.1.2). PSpice/TINA models on ti.com: **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **Margin (BOM v1 line 6, power tree §4.10):** peak 1.85 A (est.) = 62 % of the 3 A rating. Inductor peak 2.25 A = 1.85 A + ΔIL / 2, with ΔIL ≈ 0.80 A at L = 0.47 µH, fSW = 2.2 MHz, VIN = 4.4 V (Eq. 6, recomputed here and consistent with the BOM); 2.25 A is 61 % of the 3.7 A minimum current limit (SLVSEF9I, p. 6).
- **Dropout:** Eq. 3 with RDS(on) 26 mΩ and the DFE252012F-R47M 23 mΩ maximum DCR gives VIN,min = 3.3 + 1.85 × 0.049 = 3.39 V at the 1.85 A peak, as the BOM states. RDS(on) is a typical figure (p. 5); below that VSYS the rail follows VSYS down. PG falls at 92 % typ (about 3.04 V) and the device stops in UVLO at 2.1–2.3 V (p. 5).
- **Inductor (line 4):** 0.47 µH matches the recommended L in Table 8-3 (p. 13). The DFE252012F-R47M ratings (4.9 A thermal, 6.7 A at −30 % L, per its sheet) sit above the 5.0 A maximum current limit only for the 6.7 A figure; the thermal rating is below it. Not in the TI list of Table 8-5.
- **Output capacitance:** 2 × 10 µF or 22 µF nominal, ≥ 10 µF effective after DC bias at 3.3 V (p. 14). At 3.3 V the bias derating of 0603 10 µF parts is larger than at the 1.8 V example; check the effective value per capacitor.
- **Alternative:** TPS62827DMQR (4 A), same package and pinout, is named in BOM line 6 as the drop-in. It needs ≥ 20 µF effective output capacitance and is proven only with 22 µF, 3 × 10 µF, 47 or 100 µF (p. 14; p. 13, Table 8-4), and VIN ≥ 2.5 V (p. 4). See [TPS62827DMQR](TPS62827DMQR.md).
- **Thermal:** RθJA 129.5 °C/W JEDEC, 71.4 °C/W on the EVM (p. 4). The BOM's ≈ 0.2 W loss and ≈ +15 °C rise are estimates (**UNVERIFIED**).
- Off-state cost of the always-on rail: 4 µA typ, 10 µA max quiescent with no load (p. 5), plus the loads.

## Sources

- TI, TPS6282x datasheet, SLVSEF9I (March 2024): <https://www.ti.com/lit/ds/symlink/tps62826.pdf>
- OpenDAP board BOM v1 (v1.2), lines 4 and 6, Changes in v1.2 item 1; power tree v0 §2, rail table, §4.10 (`public/board/docs/specs/`).
