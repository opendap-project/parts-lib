# TPS7A2033PDBVR

- **Manufacturer:** Texas Instruments
- **Function:** 300 mA ultra-low-noise LDO, fixed 3.3 V output, active output discharge
- **BOM v1 lines:** 29 (MCLK_3V3 low-noise LDO, 3.3 V, qty 1); ADR 0010
- **Package:** SOT-23-5 (DBV0005A)
- **Datasheet:** *TPS7A20 300mA, Ultra-Low-Noise, Low-IQ, High PSRR LDO*, SBVS338H, March 2020, revised July 2024. Cited below as "SBVS338H". File sha256 `b6c487d79ebed6dd43bf220b07fc5b3ecb9ee55d87e6daa2312acda6546046c0` (matches the BOM v1 Datasheets table).
  - Same datasheet as [TPS7A2018PDBVR](TPS7A2018PDBVR.md); this sheet repeats only what differs for the 3.3 V version and the clock supply.
- **Status:** Partly UNVERIFIED

## Summary

The TPS7A2033PDBVR is the fixed 3.3 V, active-discharge ("P") TPS7A20 in SOT-23-5 (DBV), 3000 per reel, marking 2AZF (SBVS338H, p. 33, Table 8-1; p. 42, addendum). The TPS7A20 is a 300 mA LDO with 7 µVrms noise, 95 dB PSRR at 1 kHz and 6.5 µA quiescent current (SBVS338H, p. 1). In the T1 it makes MCLK_3V3 from VSYS, a dedicated supply for the two NDK NSC5083D master-clock oscillators, of which one runs at a time (BOM v1 line 29; ADR 0010; power tree v0 §2).

## Absolute maximum ratings

SBVS338H, p. 5, §5.1.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN | −0.3 | 6.5 | V |
| VOUT | −0.3 | lesser of 6.5 or VIN + 0.3 | V |
| VEN | −0.3 | 6.5 | V |
| Output current | internally limited | | |
| Operating junction TJ | −40 | 150 | °C |
| Storage Tstg | −65 | 150 | °C |

ESD (SBVS338H, p. 5): HBM ±2000 V; CDM ±750 V.

## Recommended operating conditions

SBVS338H, p. 5, §5.3: VIN 1.6–6.0 V; VEN 0–6.0 V; IOUT 0–300 mA; CIN 1 µF nominal; COUT 1–200 µF, ESR ≤ 100 mΩ; TJ −40 to 125 °C. For regulation, VIN ≥ VOUT(nom) + 0.3 V (SBVS338H, p. 31, §7.3).

Thermal, DBV (SBVS338H, p. 6): RθJA 187.1 °C/W, RθJB 54.4 °C/W.

## Power by mode

SBVS338H, p. 6, §5.5.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Shutdown | VEN = 0 V, VIN = 6.0 V, TJ = 25 °C | 0.07 | 0.2 | µA |
| Quiescent, no load | TJ = 25 °C | 6.5 | 8.5 | µA |
| Quiescent, no load | TJ −40 to 125 °C | — | 15 | µA |
| Ground current in dropout | IOUT = 0 | 6.5 | 15 | µA |

## Pinout and package

Identical to TPS7A2018PDBVR: SOT-23-5 DBV0005A; pin 1 IN, 2 GND, 3 EN, 4 N/C, 5 OUT (SBVS338H, p. 4, Figure 4-4; p. 56). MSL Level-1-260C-UNLIM, NiPdAu or Sn (SBVS338H, p. 42).

## Recommended footprint

Identical to TPS7A2018PDBVR: SBVS338H, p. 57–58, five (1.1) mm × (0.6) mm pads, 0.95 mm pitch, (2.6) mm row distance.

## Application circuit and required passives

SBVS338H, p. 30, Figure 7-4: 1.0 µF on IN, 1.0 µF on OUT (X5R/X7R/C0G, ESR ≤ 100 mΩ). No noise-bypass pin. The datasheet's worked example (TPS7A2028, 3.3 V input) uses the same values (SBVS338H, p. 31, §7.2.2).

The oscillator catalogue asks for about 0.01 µF between VCC and GND close to each oscillator (see [NSC5083D-22.5792M](../NDK/NSC5083D-22.5792M.md)); that capacitor is in addition to COUT.

## Interfaces and timing

- EN: VEN(HI) ≤ 0.9 V, VEN(LOW) ≥ 0.3 V; 500 kΩ smart pulldown (SBVS338H, p. 7).
- Start-up 750 µs typ, 1150 µs max (SBVS338H, p. 7, §5.6).
- Output tolerance for VOUT ≥ 2.8 V on DBV: ±1.5 % (SBVS338H, p. 6).
- Dropout, DBV, 2.5 V ≤ VOUT < 5.5 V, 300 mA: 145 mV max (SBVS338H, p. 6). Dropout scales with current through RDS(ON) = VDO / IRATED (SBVS338H, p. 24, Eq. 1).
- PSRR at VIN = VOUT + 1.0 V, IOUT = 20 mA: 95 dB at 100 Hz and 1 kHz, 75 dB at 10 kHz and 100 kHz, 45 dB at 1 MHz (SBVS338H, p. 7).
- Noise 7 µVrms (10 Hz–100 kHz, 300 mA, VOUT = 2.8 V) (SBVS338H, p. 7).

## Linux driver

None. EN on `AUDIO_LN_EN` (power tree v0 §7); describe as `regulator-fixed`. Driver path *none* (BOM v1 line 29).

## Simulation models

- None named in the Device Support section (SBVS338H, p. 33, §8.1). ti.com models **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **Input headroom:** VSYS minimum 3.5 V (VSYSMIN, ADR 0010 consequences) gives 0.2 V over 3.3 V. The datasheet recommends VIN ≥ VOUT + 0.3 V for optimum regulation and dynamic performance (SBVS338H, p. 31, §7.3); 0.2 V is below that recommendation, although above the dropout at 15 mA scaled from 145 mV at 300 mA. PSRR is specified at 1.0 V headroom only; at 0.2 V it is lower and must be read from the curves or measured. **UNVERIFIED** for the oscillator phase-noise budget.
- VSYS maximum must stay ≤ 6.0 V (recommended VIN max) and ≤ 6.5 V absolute.
- Load: one NSC5083D at 15 mA max operating plus one in standby at 35 µA max (NZ2520SDA catalogue); well inside the 300 mA rating.
- The BOM lists TPS7A2033PDBVR stock as **UNVERIFIED**; LP5907-3.3 is the named alternative (BOM line 29).

## Sources

- TI, TPS7A20 datasheet, SBVS338H (July 2024): <https://www.ti.com/lit/ds/symlink/tps7a20.pdf>
- OpenDAP board BOM v1, line 29; ADR 0010; power tree v0 §2, §7 (`public/board/docs/`).
