# TPD4S311A

- **Manufacturer:** Texas Instruments
- **Function:** USB Type-C port protector: 4-channel short-to-VBUS overvoltage and IEC ESD protection (CC1, CC2, SBU1, SBU2)
- **Package:** DSBGA-16 (YBF), 1.69 × 1.69 mm nominal, 0.4 mm pitch; orderable TPD4S311AYBFR
- **Datasheet:** TPD4S311, TPD4S311A, SLVSF72C (December 2019, revised February 2021), sha256 `3f206dd65f48…` in `manifest.toml`
- **BOM v1 line:** 63 (second source)

## Summary

The TPD4S311A places high-voltage FETs in series with the USB Type-C CC and SBU lines, opens them above the OVP threshold (24 V DC tolerant), adds IEC 61000-4-2 clamps on the connector side and integrated dead-battery Rd on CC (SLVSF72C §1, §3, p. 1). The "A" variant adds ±35 V (CC) and ±30 V (SBU) IEC 61000-4-5 surge rating and 600 mA VCONN (p. 1). It is the BOM v1 second source for the TPD8S300A on line 63. Unlike the TPD8S300A it has no USB 2.0 D+/D− clamps and uses a different package.

## Absolute maximum ratings

| Parameter | Pins | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Input voltage | VPWR | −0.3 | 5 | V | SLVSF72C p. 5, §7.1 |
| Input voltage | RPD_G1, RPD_G2 | −0.3 | 24 | V | p. 5 |
| Output voltage | FLT | −0.3 | 6 | V | p. 5 |
| Output voltage | VBIAS | −0.3 | 24 | V | p. 5 |
| I/O voltage | CC1, CC2, SBU1, SBU2 | −0.3 | 6 | V | p. 5 |
| I/O voltage | C_CC1, C_CC2, C_SBU1, C_SBU2 | −0.3 | 24 | V | p. 5 |
| Output current (TPD4S311A) | C_CC1, C_CC2 | — | 1.2 | A | p. 5 |
| Operating free-air temperature, TA | — | −40 | 85 | °C | p. 5 |
| Storage temperature, Tstg | — | −65 | 150 | °C | p. 5 |
| ESD, HBM / CDM | — | — | ±2000 / ±500 | V | p. 5, §7.2 |
| IEC 61000-4-2 contact / air, C_CCx | — | — | ±8000 / ±15000 | V | p. 5, §7.3 |
| IEC 61000-4-2 contact / air, C_SBUx | — | — | ±6000 / ±15000 | V | p. 5, §7.3 |
| IEC 61000-4-5 surge, C_CCx / C_SBUx (TPD4S311A) | — | — | ±35 / ±30 | V | p. 5, §7.3 |

## Recommended operating conditions

| Parameter | Min | Nom | Max | Unit | Reference |
|---|---|---|---|---|---|
| VPWR | 2.7 | 3.3 | 4.5 | V | p. 5, §7.4 |
| CC1, CC2, C_CC1, C_CC2 | 0 | — | 5.5 | V | p. 5 |
| SBU1, SBU2, C_SBU1, C_SBU2 | 0 | — | 4.3 | V | p. 5 |
| VCONN current, 4.5 ≤ CCx ≤ 5.5 V, TJ ≤ 105 °C (TPD4S311A) | — | — | 600 | mA | p. 6 |
| FLT pull-up resistance | 1.7 | — | 300 | kΩ | p. 6 |
| VBIAS capacitance (≥ 35 V rated, 50 V recommended) | — | 0.1 | — | µF | p. 6 |
| VPWR capacitance | 0.3 | 1 | — | µF | p. 6 |

### Electrical characteristics

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| CC OVP FET on-resistance (TPD4S311A) | CCx = 5.5 V, TJ ≤ 85 °C | — | 232 | 405 | mΩ | p. 6, §7.6 |
| CC equivalent on-capacitance | powered | 45 | 74 | 120 | pF | p. 6 |
| Dead-battery RD (unpowered) | VC_CCx = 2.6 V | 4.1 | 5.1 | 6.1 | kΩ | p. 6 |
| CC OVP threshold | rising | 5.75 | 6.0 | 6.2 | V | p. 6 |
| SBU OVP FET on-resistance | SBUx = 3.6 V | — | 4 | 6.5 | Ω | p. 7 |
| SBU OVP threshold | rising | 4.35 | 4.5 | 4.7 | V | p. 7 |
| System-side clamp, short-to-VBUS 24 V, CC and SBU | VPWR = 3.3 V | — | 8 | — | V | p. 7 |
| VPWR UVLO, rising | — | 2.1 | 2.3 | 2.5 | V | p. 7 |
| VPWR supply current | 3.3 V typ, 4.5 V max | — | 90 | 135 | µA | p. 7 |

## Power by mode

As for the TPD8S300A: FETs off below UVLO (dead-battery RD present if RPD_Gx is strapped), on above UVLO with 90 µA typical supply current (p. 7), off with FLT asserted on overvoltage. Current in the fault modes is not specified separately (**UNVERIFIED**).

## Pinout and package

DSBGA-16 (YBF), top view (Figure 6-1, Table 6-1, p. 4):

| Ball | Name | Ball | Name |
|---|---|---|---|
| A1 | C_SBU2 | C1, C2, C3 | GND |
| A2 | C_CC1 | C4 | VPWR (2.7–4.5 V) |
| A3 | C_CC2 | D1 | SBU1 |
| A4 | VBIAS (0.1 µF to GND) | D2 | SBU2 |
| B1 | C_SBU1 | D3 | CC1 |
| B2 | RPD_G1 | D4 | CC2 |
| B3 | RPD_G2 | | |
| B4 | FLT (open drain) | | |

Outline YBF0016 (drawing 4225494/A 11/2019, PDF p. 30): D and E 1.66–1.72 mm, 0.55 mm maximum height, ball pitch 0.4 mm, ball Ø 0.23–0.27 mm. SnAgCu balls, reel of 3000 (package option addendum, p. 26).

## Recommended footprint / land pattern

YBF0016 example board layout (PDF p. 31): 16 Ø 0.23 mm pads at 0.4 mm pitch; non-solder-mask-defined preferred, 0.05 mm maximum clearance. Stencil on PDF p. 32.

## Application circuit and required passives

Same passives as the TPD8S300A: 0.1 µF ≥ 35 V (50 V recommended) on VBIAS, 1 µF on VPWR, FLT pull-up 1.7–300 kΩ, RPD_Gx strapped to C_CCx for dead-battery support or to GND (p. 4, pp. 5–6; §10, p. 23; §11.1, p. 24).

## Interfaces and timing

| Parameter | Typ | Max | Unit | Reference |
|---|---|---|---|---|
| VPWR UVLO to FETs on, tON_FET | 1.3 | 3.5 | ms | p. 8 |
| VPWR UVLO to FETs on and RD off, tON_FET_DB | 5.7 | 9.5 | ms | p. 8 |
| OVP response, CC / SBU | 70 / 80 | — | ns | p. 8 |

## Linux driver

None (no software interface).

## Simulation models available

None listed in `manifest.toml`. IBIS or SPICE availability is **UNVERIFIED**.

## Design notes for the T1

- Not footprint-compatible with the TPD8S300ARUKR (WQFN-20 versus 0.4 mm DSBGA-16); using it as second source needs its own footprint or a second layout option. A 0.4 mm-pitch DSBGA also sets PCB rules (via-in-pad or fine escape).
- It has no D1–D4 USB 2.0 clamps; with it, USB D+/D− rely on the TPD4E05U06 alone (BOM v1 line 62).
- VPWR range extends to 4.5 V (p. 5), wider than the TPD8S300A's 3.6 V.
- LCSC stock was 7 units on 2026-10-22 (BOM v1 line 63).

## Sources

- TI, *TPD4S311, TPD4S311A USB Type-C Port Protector: Short-to-VBUS Overvoltage and IEC ESD Protection*, SLVSF72C, revised February 2021, <https://www.ti.com/lit/ds/symlink/tpd4s311.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 62, 63
