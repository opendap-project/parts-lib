# TPS7A2031PDBVR

- **Manufacturer:** Texas Instruments
- **Function:** 300 mA ultra-low-noise LDO, fixed 3.1 V output, active output discharge
- **BOM v1 lines:** 29 (MCLK_3V1 low-noise LDO from VSYS, 3.1 V, qty 1; BOM v1.1, replaces the TPS7A2033PDBVR); ADR 0010 (supply part amended in BOM v1.1)
- **Package:** SOT-23-5 (DBV0005A), 2.9 × 2.8 mm nominal, 1.45 mm max height
- **Datasheet:** *TPS7A20 300mA, Ultra-Low-Noise, Low-IQ, High PSRR LDO*, SBVS338H, March 2020, revised July 2024. Cited below as "SBVS338H". File sha256 `b6c487d79ebed6dd43bf220b07fc5b3ecb9ee55d87e6daa2312acda6546046c0` (matches the BOM v1.1 Datasheets table).
  - Same datasheet as [TPS7A2018PDBVR](TPS7A2018PDBVR.md) and [TPS7A2033PDBVR](TPS7A2033PDBVR.md); this sheet repeats the shared data in short form and details what differs for the 3.1 V version and the clock supply.
- **Status:** Partly UNVERIFIED

## Summary

The TPS7A2031PDBVR is the fixed 3.1 V, active-discharge ("P") TPS7A20 in SOT-23-5 (DBV), listed as Active, 3000 per reel, NiPdAu or Sn finish, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking 2GDF (SBVS338H, p. 44, Package Option Addendum). The TPS7A20 is a 300 mA LDO with 7 µVrms noise, 95 dB PSRR at 1 kHz and 6.5 µA quiescent current (SBVS338H, p. 1). In the T1 it makes MCLK_3V1 from VSYS, the dedicated supply of the two NDK NSC5083D master-clock oscillators, of which one runs at a time (BOM v1 line 29; ADR 0010; power tree v0 §1 item 12, §3). It replaces the TPS7A2033PDBVR, whose 0.2 V headroom at VSYS = 3.5 V was below the datasheet recommendation (BOM v1 §9, D5).

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
| IOUT | 0 | | 300 | mA |
| CIN | | 1 | | µF |
| COUT | 1 | | 200 | µF |
| COUT ESR | | | 100 | mΩ |
| TJ | −40 | | 125 | °C |

- For a well-regulated output and optimum dynamic performance the input must be at least VOUT(nom) + 0.3 V or 1.6 V, whichever is greater (SBVS338H, p. 31, §7.3). For 3.1 V: VIN ≥ 3.4 V.

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

Dissipation: PD = (VIN − VOUT) × IOUT (SBVS338H, p. 28, Eq. 2). T1 worst case: (4.4 V − 3.1 V) × 15 mA = 19.5 mW, about +3.6 °C at RθJA 187.1 °C/W (calculation; VSYS maximum and the 15 mA load from power tree v0 §2–§3).

## Pinout and package

Identical to TPS7A2018PDBVR: SOT-23-5 (DBV0005A), 2.9 mm × 2.8 mm nominal, 1.45 mm max height (SBVS338H, p. 1; p. 56, drawing 4214839/K 08/2024).

| Pin | Name | Function |
|---|---|---|
| 1 | IN | Input; capacitor close to IN and GND |
| 2 | GND | Ground |
| 3 | EN | Enable, active high; internal 500 kΩ pulldown disconnected once VEN > VEN(HI); low disables and discharges OUT |
| 4 | N/C | No internal connection |
| 5 | OUT | Output; low-ESR capacitor to ground; 150 Ω internal discharge when disabled |

(SBVS338H, p. 4, Figure 4-4 and Pin Functions.) Tape and reel: 180 mm reel, 8.4 mm width, pin 1 quadrant Q3 (SBVS338H, p. 51); box 210 × 185 × 35 mm (p. 54).

## Recommended footprint

Identical to TPS7A2018PDBVR: SBVS338H, p. 57 (DBV0005A example board layout) and p. 58 (stencil, 0.125 mm):

- 5 pads (1.1) mm × (0.6) mm; pitch 0.95 mm along each side; pad-row centre distance (2.6) mm.
- Non-solder-mask-defined pads preferred, 0.07 mm mask clearance.
- Stencil apertures equal to the pads.

## Application circuit and required passives

Typical application (SBVS338H, p. 30, Figure 7-4):

| Ref | Value | Note |
|---|---|---|
| CIN | 1.0 µF | X5R/X7R/C0G; TI highly recommends ≥ 1 µF against input impedance and transients (p. 31, §7.3) |
| COUT | 1.0 µF | Within 1–200 µF, ESR ≤ 100 mΩ |

- No noise-bypass pin; the reference is filtered internally (SBVS338H, p. 24, §6.3.1).
- The oscillator catalogue asks for about 0.01 µF between VCC and GND close to each oscillator (see [NSC5083D-22.5792M](../NDK/NSC5083D-22.5792M.md)); that capacitor is in addition to COUT. BOM v1 §5 lists 10 nF XO bypass and 100 kΩ ST pull-downs ×2.

## Interfaces and timing

- EN: VEN(HI) 0.9 V max, VEN(LOW) 0.3 V min; 500 kΩ smart pulldown (SBVS338H, p. 7). Driven directly by 1.8 V logic (`AUDIO_LN_EN`).
- Start-up time 750 µs typ, 1150 µs max (SBVS338H, p. 7, §5.6).
- Output tolerance, DBV, VOUT ≥ 2.8 V: ±1.5 % over VIN = VOUT(NOM) + 0.3 V to 6.0 V, IOUT 1–300 mA (SBVS338H, p. 6). For 3.1 V: 3.054–3.147 V.
- Dropout, DBV, 2.5 V ≤ VOUT < 5.5 V, 300 mA: 145 mV max (SBVS338H, p. 6). Dropout scales with current through RDS(ON) = VDO / IRATED (SBVS338H, p. 24, Eq. 1).
- Current limit 360 / 520 / 730 mA; short-circuit 160 mA (foldback) (SBVS338H, p. 7).
- PSRR at VIN = VOUT + 1.0 V, IOUT = 20 mA: 95 dB at 100 Hz and 1 kHz, 75 dB at 10 kHz and 100 kHz, 45 dB at 1 MHz (SBVS338H, p. 7).
- Noise 7 µVrms, 10 Hz–100 kHz, IOUT = 300 mA, VOUT = 2.8 V (SBVS338H, p. 7).
- Thermal shutdown 165 °C rising, 140 °C falling (SBVS338H, p. 7).

## Linux driver

None. EN on `AUDIO_LN_EN` (power tree v0 §5); describe as `regulator-fixed`. Driver path *none* (BOM v1 line 29).

## Simulation models

- None named in the Device Support section (SBVS338H, p. 33, §8.1). ti.com models **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **Input headroom:** VSYS follows VBAT on battery (power tree v0 §2–§3: 3.4–4.4 V). At VSYS = 3.4 V the headroom is 0.3 V, which meets the VIN ≥ VOUT(nom) + 0.3 V recommendation (SBVS338H, p. 31, §7.3). Below 3.4 V the output still regulates as long as VIN exceeds 3.1 V plus the dropout at 15 mA (145 mV × 15 / 300 ≈ 7 mV, scaled with Eq. 1), but the accuracy and dynamic figures are no longer specified. Whether VSYS can fall below 3.4 V on battery before the system cut-off is **UNVERIFIED** here.
- **PSRR at the operating point:** PSRR and noise are specified at 1.0 V headroom and VOUT = 2.8 V; at 0.3–1.3 V headroom and 15 mA they must be read from the datasheet curves or measured. The effect on oscillator phase noise is **UNVERIFIED** (BOM v1 §7 item 10).
- **Clock supply range:** 3.1 V ±1.5 % (3.054–3.147 V) sits inside the NSC5083D 2.97–3.63 V supply range (BOM v1 line 29, D5). NDK characterises phase noise at 3.3 V only; the 3.1 V figure is **UNVERIFIED** until measured (BOM v1 line 29; power tree v0 §4.4).
- **Load:** one NSC5083D at 15 mA max operating plus one in standby at 35 µA (NZ2520SDA catalogue, power tree v0 §4.4), far inside the 300 mA rating.
- VSYS maximum must stay ≤ 6.0 V (recommended VIN max) and ≤ 6.5 V absolute.
- Same footprint and datasheet as the TPS7A2033PDBVR it replaces; the BOM keeps the TPS7A2033PDBVR as an option only if VSYS stays ≥ 3.6 V (BOM v1 line 29).

## Sources

- TI, TPS7A20 datasheet, SBVS338H (July 2024): <https://www.ti.com/lit/ds/symlink/tps7a20.pdf>
- OpenDAP board BOM v1.1, line 29, §5, §7 item 10, §9 D5; ADR 0010; power tree v0 §1, §2, §3, §4.4, §5 (`public/board/docs/`).
