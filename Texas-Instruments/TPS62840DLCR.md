# TPS62840DLCR

- **Manufacturer:** Texas Instruments
- **Function:** 1.8 V to 6.5 V input, 750 mA, 60 nA IQ step-down converter
- **BOM v1 lines:** 27 (audio 2.2 V pre-buck, AUDIO_2V2)
- **Package:** VSON-HR-8 (DLC), 1.5 × 2 mm, 0.5 mm pitch, no exposed pad
- **Datasheet:** *TPS62840 1.8-V to 6.5-V, 750-mA, 60-nA IQ Step-Down Converter*, SLVSEC6D, June 2019, revised March 2020. Cited below as "SLVSEC6D". File sha256 `b715ae80beb8f08b5c4a417537c5f52e01ad0a52f3791c240146b72fec5f3214` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The TPS62840 is a DCS-Control step-down converter, 1.8 V to 6.5 V input, up to 750 mA output, 60 nA typical operating quiescent current and 25 nA shutdown current, with 16 output voltages selected by one resistor on VSET (SLVSEC6D, p. 1). The DLC option (VSON-HR-8, 1.5 mm × 2 mm) has the MODE and STOP pins and output discharge, and covers 1.8 V to 3.3 V in 100 mV steps (SLVSEC6D, p. 3, Device Comparison Table). In the T1 it makes AUDIO_2V2 (2.2 V) from VSYS as the pre-regulator of the two TPS7A2018 DAC VA LDOs (BOM v1 line 27; power tree v0 §2, §4.3).

**VSET check (BOM line 29 flag):** 2.2 V is a valid TPS62840DLC code: RSET = 4.32 kΩ nominal (E96), accepted range 4.15 kΩ to 4.49 kΩ (SLVSEC6D, p. 13, Table 1). No fallback to 2.1 V is needed.

## Absolute maximum ratings

SLVSEC6D, p. 6, §7.1. Voltages to GND.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN | −0.3 | 7 | V |
| SW (DC) | −0.3 | VIN + 0.3 | V |
| SW (AC, < 10 ns, while switching) | −2.0 | 8.5 | V |
| EN, MODE, STOP | −0.3 | 6.5 | V |
| VSET | −0.3 | VIN + 0.3, < 3.6 | V |
| VOS | −0.3 | 3.7 | V |
| Operating junction TJ | −40 | 150 | °C |
| Storage Tstg | −65 | 150 | °C |

ESD (SLVSEC6D, p. 6, §7.2): HBM ±2000 V; CDM ±500 V.

## Recommended operating conditions

SLVSEC6D, p. 6, §7.3.

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | 1.8 | | 6.5 | V |
| Effective inductance L | 1.51 | 2.2 | 2.9 | µH |
| Effective output capacitance COUT | 3 | 10 | 40 | µF |
| Effective input capacitance CIN | 1 | 4.7 | | µF |
| Parasitic capacitance at VSET | | | 100 | pF |
| RSET nominal range (E96) | 0.909 | | 267 | kΩ |
| RSET tolerance | | | 1 | % |
| RSET temperature coefficient | | | ±200 | ppm/°C |
| TJ | −40 | | 125 | °C |

Thermal, DLC package (SLVSEC6D, p. 6, §7.4): RθJA 105.6 °C/W, RθJB 31.9 °C/W, ψJB 31.5 °C/W.

## Power by mode

SLVSEC6D, p. 7, §7.5, VIN = 3.6 V, typical at TJ = 25 °C.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown (EN = GND, VSET = GND) | TJ −40 to 85 °C | 25 | 300 | nA |
| Power-save, no load, switching | VOUT = 1.8 V | 60 | — | nA |
| Forced PWM, no load | VOUT = 1.8 V, MODE = VIN | 3 | — | mA |
| 100 % mode | VIN = VOUT = 3.3 V, TJ −40 to 85 °C | 120 | — | nA |
| STOP mode, into VIN | STOP high, VOUT = 1.8 V, TJ −40 to 85 °C | 70 | 175 | µA |

- Power-save mode (MODE low): PFM at light load, PWM at moderate to heavy load, automatic transition (SLVSEC6D, p. 12, §8.3.3; p. 15, §8.4.1).
- Forced PWM (MODE high): fixed frequency over the full load range, lower light-load efficiency; MODE may change during operation and must be terminated (SLVSEC6D, p. 15, §8.4.2).
- Thermal shutdown is disabled in power-save mode (SLVSEC6D, p. 14, §8.3.8).

## Pinout and package

VSON-HR-8 (DLC), body 1.4–1.6 mm × 1.9–2.1 mm, 1 mm max height, 0.5 mm pitch, no exposed pad (SLVSEC6D, p. 4; p. 36, DLC0008B, drawing 4224310/A 05/2018).

| Pin | Name | Function |
|---|---|---|
| 1 | GND | Ground; close to CIN and COUT ground |
| 2 | VIN | Supply; 4.7 µF ceramic required close to the pin |
| 3 | MODE | Low: power-save with PFM/PWM; high: forced PWM; must be terminated |
| 4 | EN | High enables; internal pulldown active until regulation |
| 5 | VSET | Resistor to GND selects VOUT at start-up |
| 6 | STOP | High stops switching (output held by COUT); internal pulldown |
| 7 | SW | Switch node, to the inductor |
| 8 | VOS | Output sense; discharges VOUT when disabled |

(SLVSEC6D, p. 5, Pin Functions.) Orderable TPS62840DLCR: 3000 per reel, Sn finish, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking E5 (SLVSEC6D, package addendum).

## Recommended footprint

SLVSEC6D, p. 37 (DLC0008B example board layout) and p. 38 (stencil, 0.1 mm):

- 8 pads (0.6) mm × (0.25) mm at 0.5 mm pitch, two rows, (1.3) mm between row centres as drawn.
- Non-solder-mask-defined pads preferred, 0.05 mm mask clearance.
- Stencil apertures equal to the pads at 0.1 mm thickness.

## Application circuit and required passives

Application circuit (SLVSEC6D, p. 16, Figure 13; p. 17, Table 2; Table 3):

| Ref | Datasheet value | Note |
|---|---|---|
| CI | 4.7 µF / 10 V / X5R, 0402 (GRM155R61A475MEAAD) | Closest to VIN/GND; most critical placement (p. 28, §11.1) |
| CO | 10 µF / 4 V / X5R, 0402 (GRM155R60G106ME44D) | 10 µF typical, 22 µF alternative (Table 3) |
| L | 2.2 µH, 116 mΩ DCR (Murata DFE201612E-2R2M) | Listed alternatives: DFE201612E, DFE201210S (p. 18, Table 4) |
| RSET | 4.32 kΩ, 1 %, E96, ±200 ppm/°C for 2.2 V | Table 1, p. 13 |

- Inductor saturation current: above ILmax = IOUT(max) + ΔIL/2, or conservatively above ILIMF (1.4 A max) (SLVSEC6D, p. 17, Eq. 4–5).
- Keep parasitic capacitance or leakage on VSET below 100 pF, or the R2D read-out sets a wrong voltage (SLVSEC6D, p. 13, §8.3.4).
- VOS is high-impedance: route it to COUT away from SW (SLVSEC6D, p. 28, §11.1).

## Interfaces and timing

- EN, MODE, STOP: VIH ≥ 1.1 V, VIL ≤ 0.4 V; EN/STOP pulldown 200–450 kΩ (SLVSEC6D, p. 7). Compatible with 1.8 V GPIO by threshold.
- Start-up delay 200 µs from EN high (VIN present); 10 ms when EN ramps with VIN (SLVSEC6D, p. 8).
- Soft-start 120 µs typ at no load; up to about 700 µs (SLVSEC6D, p. 8; p. 12, §8.3.2).
- RSET is read once during the start-up delay; also re-read after UVLO recovery, not after thermal shutdown (SLVSEC6D, p. 12–14).
- UVLO: rising 1.72 / 1.8 V, falling 1.45 / 1.75 V (typ / max) (SLVSEC6D, p. 7).
- Current limit: high-side 1.0 / 1.2 / 1.4 A; soft-start 0.15 / 0.225 / 0.3 A; negative 533 mA (SLVSEC6D, p. 8).
- Switching frequency 1.8 MHz typ in PWM (VIN 3.6 V, VOUT 1.8 V) (SLVSEC6D, p. 8).
- Output accuracy ±1.5 % (PWM, VOUT ≥ 1.8 V) (SLVSEC6D, p. 8).
- Output discharge 16 / 35 / 44 mA into VOS when disabled (SLVSEC6D, p. 8).
- Thermal shutdown 160 °C, 5 °C hysteresis (SLVSEC6D, p. 8).

## Linux driver

None. No digital interface; EN (`AUDIO_LN_EN`) and optionally MODE/STOP are GPIOs. Describe as a `regulator-fixed` supply (BOM v1 line 27: driver path *none*).

## Simulation models

- The Device Support section (SLVSEC6D, p. 30, §12.1) names no simulation model.
- An EVM, TPS62841-2EVM123, is named only in the thermal table (SLVSEC6D, p. 6, §7.4).
- PSpice/TINA/WEBENCH models on ti.com: **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **2.2 V is selectable** with RSET = 4.32 kΩ (Table 1); the BOM line 29 open point is closed by the datasheet.
- **1 µH is outside the recommended range:** the effective inductance must be 1.51–2.9 µH (SLVSEC6D, p. 6). The BOM line 28 alternative "DFE201610E-1R0M if the datasheet allows 1 µH" is not allowed. The BOM part DFE201610E-2R2M (2.2 µH) is not in the datasheet's inductor list (Table 4); its saturation current against 1.4 A and its DCR are to be checked on that part's sheet.
- Power-save mode bursts may fall in the audio band; the TPS7A2018 PSRR downstream is the filter (power tree v0 §4.3). MODE high (forced PWM, 3 mA no-load) or STOP high (switching halted, 70 µA) are available on the DLC package if measurement shows audible residue. **UNVERIFIED** until measured.
- 100 % mode adds +30 mV to the set point near dropout (SLVSEC6D, p. 15, §8.4.3); not reached with VSYS ≥ 3.4 V (power tree v0 §3; on battery VSYS follows VBAT) and 2.2 V out.
- EN can be driven directly by the 1.8 V `AUDIO_LN_EN` GPIO (VIH 1.1 V).

## Sources

- TI, TPS62840 datasheet, SLVSEC6D (March 2020): <https://www.ti.com/lit/ds/symlink/tps62840.pdf>
- OpenDAP board BOM v1, lines 27–29; power tree v0 §2, §4.3 (`public/board/docs/specs/`).
