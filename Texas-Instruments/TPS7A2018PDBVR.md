# Texas Instruments TPS7A2018PDBVR

- BOM: board BOM v1, line 29 (DAC1 VA and DAC2 VA low-noise LDOs, 1.8 V, qty 2).
- Datasheet: *TPS7A20 300mA, Ultra-Low-Noise, Low-IQ, High PSRR LDO*, SBVS338H, March 2020, revised July 2024. Cited below as "SBVS338H".
- Datasheet file: `~/.cache/opendap/parts/Texas-Instruments/TPS7A2018PDBVR/tps7a20.pdf`, sha256 `b6c487d79ebed6dd43bf220b07fc5b3ecb9ee55d87e6daa2312acda6546046c0` (matches the BOM v1 Datasheets table).
- Same datasheet as [TPS7A2033PDBVR](TPS7A2033PDBVR.md).

## Summary

The TPS7A20 is a 300 mA CMOS LDO with 7 µVrms output noise without a noise-bypass capacitor, 95 dB PSRR at 1 kHz, 6.5 µA quiescent current, 1.6 V to 6.0 V input, ±1.5 % accuracy and a smart enable pulldown (SBVS338H, p. 1). TPS7A2018PDBVR is the fixed 1.8 V version with active output discharge ("P") in SOT-23-5 (DBV), 3000 per reel (SBVS338H, p. 33, Table 8-1). In the T1, two of them make DAC1_VA and DAC2_VA (1.8 V, 7.8 mA each), the analog supplies of the two CS43198 DACs, from the 2.2 V AUDIO_2V2 rail of the TPS62840; one LDO per DAC keeps the dual-mono layout independent (BOM v1 line 29; power tree v0 §2, §4.3).

## Absolute maximum ratings

SBVS338H, p. 5, §5.1. Voltages to GND.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN | −0.3 | 6.5 | V |
| VOUT | −0.3 | lesser of 6.5 or VIN + 0.3 | V |
| VEN | −0.3 | 6.5 | V |
| Output current | internally limited | | |
| Operating junction TJ | −40 | 150 | °C |
| Storage Tstg | −65 | 150 | °C |

ESD (SBVS338H, p. 5, §5.2): HBM ±2000 V; CDM ±750 V.

## Recommended operating conditions

SBVS338H, p. 5, §5.3.

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | 1.6 | | 6.0 | V |
| VEN | 0 | | 6.0 | V |
| VOUT (family range) | 0.8 | | 5.5 | V |
| IOUT | 0 | | 300 | mA |
| CIN | | 1 | | µF |
| COUT | 1 | | 200 | µF |
| COUT ESR | | | 100 | mΩ |
| TJ | −40 | | 125 | °C |

- CIN is not needed for stability; ≥ 0.47 µF effective is recommended against source impedance (SBVS338H, p. 5, note 2).
- Effective COUT 0.47 µF minimum to 200 µF maximum for stability (SBVS338H, p. 5, note 3).

Thermal, DBV (SBVS338H, p. 6, §5.4): RθJA 187.1 °C/W, RθJB 54.4 °C/W, ψJB 54.1 °C/W.

## Power by mode

SBVS338H, p. 6, §5.5; typical at TJ = 25 °C.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | VEN = 0 V, VIN = 6.0 V, TJ = 25 °C | 0.07 | 0.2 | µA |
| Quiescent, no load | VEN = VIN = 6 V, TJ = 25 °C | 6.5 | 8.5 | µA |
| Quiescent, no load | TJ −40 to 85 °C | — | 10 | µA |
| Quiescent, no load | TJ −40 to 125 °C | — | 15 | µA |
| Ground current, full load | IOUT = 300 mA | 2000 | — | µA |
| Ground current in dropout | VIN ≤ VOUT(NOM), IOUT = 0 | 6.5 | 15 | µA |

Dissipation: PD = (VIN − VOUT) × IOUT (SBVS338H, p. 28, Eq. 2).

## Pinout and package

SOT-23-5 (DBV0005A), 2.9 mm × 2.8 mm nominal, 1.45 mm max height (SBVS338H, p. 1; p. 56, drawing 4214839/K 08/2024).

| Pin | Name | Function |
|---|---|---|
| 1 | IN | Input; capacitor close to IN and GND |
| 2 | GND | Ground |
| 3 | EN | Enable, active high; internal 500 kΩ pulldown disconnected once VEN > VEN(HI); low disables and discharges OUT |
| 4 | N/C | No internal connection |
| 5 | OUT | Output; low-ESR capacitor to ground; 150 Ω internal discharge when disabled |

(SBVS338H, p. 4, Figure 4-4 and Pin Functions.) Addendum: NiPdAu or Sn finish, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking 2AUF (SBVS338H, p. 42).

## Recommended footprint / land pattern

SBVS338H, p. 57 (DBV0005A example board layout) and p. 58 (stencil, 0.125 mm):

- 5 pads (1.1) mm × (0.6) mm; pitch 0.95 mm along each side (pins 1–3 side: 2 × 0.95 mm; pins 4–5 at 1.9 mm); pad-row centre distance (2.6) mm.
- Non-solder-mask-defined pads preferred, 0.07 mm mask clearance.
- Stencil apertures equal to the pads.

## Application circuit and required passives

Typical application (SBVS338H, p. 30, Figure 7-4):

| Ref | Value | Note |
|---|---|---|
| CIN | 1.0 µF | X5R/X7R/C0G; recommended if source impedance > 0.5 Ω (p. 27, §7.1.2) |
| COUT | 1.0 µF | Within 1–200 µF, ESR ≤ 100 mΩ |

- No noise-bypass capacitor exists or is needed: the reference is filtered internally at about 0.1 Hz (SBVS338H, p. 24, §6.3.1).
- Expect up to 50 % capacitance loss with bias and temperature; the recommended values account for it (SBVS338H, p. 27, §7.1.1).
- Layout: capacitors close to the device, copper planes, thermal vias around the device (SBVS338H, p. 31, §7.4.1; Figure 7-7).

## Interfaces and timing

- EN: VEN(HI) 0.9 V max, VEN(LOW) 0.3 V min, VIN 1.6–6.0 V (SBVS338H, p. 7). Driven directly by 1.8 V logic.
- EN pulldown 500 kΩ; leakage 90 / 250 nA at 6 V (SBVS338H, p. 7).
- Start-up time 750 µs typ, 1150 µs max from VEN > VEN(HI) to 95 % VOUT (SBVS338H, p. 7, §5.6).
- UVLO (DBV): rising 1.17 / 1.35 / 1.59 V, falling 1.11 / 1.3 / 1.55 V, hysteresis 50 mV (SBVS338H, p. 7).
- Output tolerance for VOUT < 2.8 V on DBV: ±40 mV over VIN = VOUT + 0.3 V to 6.0 V, IOUT 1–300 mA (SBVS338H, p. 6). For 1.8 V this is ±2.2 %.
- Dropout, DBV, 1.5 V ≤ VOUT < 2.5 V, 300 mA: 205 mV max (SBVS338H, p. 6).
- Current limit 360 / 520 / 730 mA; short-circuit 160 mA (foldback) (SBVS338H, p. 7).
- PSRR at VIN = VOUT + 1.0 V, IOUT = 20 mA: 95 dB (100 Hz), 95 dB (1 kHz), 75 dB (10 kHz), 75 dB (100 kHz), 45 dB (1 MHz) (SBVS338H, p. 7).
- Noise 7 µVrms, 10 Hz–100 kHz, IOUT = 300 mA; 10 µVrms at IOUT = 1 mA; both at VOUT = 2.8 V (SBVS338H, p. 7).
- Thermal shutdown 165 °C rising, 140 °C falling (SBVS338H, p. 7).

## Linux driver

None. EN on `AUDIO_LN_EN` (power tree v0 §7). Describe as a `regulator-fixed` supply (BOM v1 line 29: driver path *none*).

## Simulation models available

- The Device Support section (SBVS338H, p. 33, §8.1) names no simulation model or EVM.
- PSpice/TINA models on ti.com: **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **Headroom:** VIN = 2.2 V, VOUT = 1.8 V gives 0.4 V. The PSRR and noise figures above are specified at VIN = VOUT + 1.0 V and VOUT = 2.8 V; at 0.4 V headroom and 7.8 mA the PSRR must be read from the datasheet curves or measured. The power tree's 75 dB coupling figure (power tree v0 §4.3) is **UNVERIFIED** for this operating point.
- The 2.2 V pre-rail is a valid TPS62840 code (RSET 4.32 kΩ, see [TPS62840DLCR](TPS62840DLCR.md)); the BOM line 29 open point is closed.
- Accuracy on DBV at 1.8 V is ±40 mV, wider than the ±1.5 % of the DQN/YCJ/YCK packages for VOUT ≥ 1.85 V (SBVS338H, p. 6). The CS43198 VA range is to be checked against 1.76–1.84 V on the CS43198 sheet.
- Active discharge (P version) pulls the output down through 150 Ω when EN is low (SBVS338H, p. 4, p. 26). Do not rely on it with large output capacitance after VIN collapses; reverse current is limited to 5 % of rated current for short periods (SBVS338H, p. 26, §6.3.7).
- Alternatives named in the BOM: TPS7A2018PDQNR (X2SON) and LP5907-1.8. The X2SON offers ±1.5 % at VOUT ≥ 1.85 V only, so 1.8 V stays at ±30 mV there (SBVS338H, p. 6).

## Sources

- TI, TPS7A20 datasheet, SBVS338H (July 2024): <https://www.ti.com/lit/ds/symlink/tps7a20.pdf>
- OpenDAP board BOM v1, line 29; power tree v0 §2, §4.3, §7 (`public/board/docs/specs/`).
