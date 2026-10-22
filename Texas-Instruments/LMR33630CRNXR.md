# LMR33630CRNXR

- **Manufacturer:** Texas Instruments
- **Function:** SIMPLE SWITCHER 3.8–36 V, 3 A synchronous step-down converter, 2.1 MHz ("C" version); used in the T1 as an inverting buck-boost for −7 V
- **BOM v1 lines:** 116 (Audio, −7.0 V HP-amp pre-rail AUDIO_N7V0 from VSYS, qty 1; new in BOM v1.6, board ADR 0015); inductor on line 117 ([XGL4020-222MEC](../Coilcraft/XGL4020-222MEC.md)); passives on line 118; EN level shifter on line 119
- **Package:** VQFN-HR-12 (RNX), 2 × 3 mm
- **Datasheet:** *LMR33630 SIMPLE SWITCHER 3.8-V to 36-V, 3-A Synchronous Step-down Voltage Converter*, SNVSAN3F, August 2017, revised November 2020. Cited below as "SNVSAN3F". File sha256 `3b0920a4e56a0b3f5f214a6317d3c06cff6e541e5054024adc31c30acc50c04a`.
  - Topology: TI application note *Working With Inverting Buck-Boost Converters*, SNVA856B (May 2020, revised October 2022), sha256 `806345f00ea5d4bd5148149e96a73941d791c04746f12b0316d5f983c47c3478`. Cited as "SNVA856B".
- **Status:** Partly UNVERIFIED

## Summary

The LMR33630 is a synchronous buck converter with 75 / 50 mΩ internal switches, 3.8–36 V input, 1–24 V adjustable output, 3 A output, 24 µA non-switching quiescent current, PFM at light load, internal compensation, soft start and power good (SNVSAN3F, p. 1, §7.3, §7.5). In the T1 it runs as an inverting buck-boost (IBB) per SNVA856B: VIN on VSYS, its AGND and PGND on the −7 V rail, the inductor from SW to system ground, so it makes −7.06 V for the two LT3094 regulators of the negative amplifier rail (board ADR 0015; board output-stage simulation §5). The C version (2.1 MHz) keeps its beat with the TPS65131 (1.25–1.5 MHz) at or above 0.3 MHz.

## Absolute maximum ratings

SNVSAN3F, p. 6, §7.1. In the IBB, "PGND/AGND" is the −7 V rail.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN to PGND | −0.3 | 38 | V |
| EN to AGND | −0.3 | VIN + 0.3 | V |
| FB to AGND | −0.3 | 5.5 | V |
| PG to AGND | 0 | 22 | V |
| AGND to PGND | −0.3 | 0.3 | V |
| SW to PGND | −0.3 | VIN + 0.3 | V |
| SW to PGND, < 100 ns transients | −3.5 | 38 | V |
| BOOT to SW | −0.3 | 5.5 | V |
| VCC to AGND | −0.3 | 5.5 | V |
| TJ | −40 | 150 | °C |
| Tstg | −55 | 150 | °C |

ESD (p. 6, §7.2): HBM ±2500 V; CDM ±750 V.

## Recommended operating conditions

SNVSAN3F, p. 6, §7.3: VIN to PGND 3.8–36 V; EN 0 to VIN; PG 0–18 V; VOUT 1–24 V (buck use); IOUT 0–3 A; −40 to 125 °C.

Thermal (p. 7, §7.4, JEDEC simulation, not for design): RNX RθJA 72.5 °C/W, RθJC(top) 35.9 °C/W, RθJB 23.3 °C/W, ψJT 0.8 °C/W, ψJB 23.5 °C/W.

## Power by mode

SNVSAN3F, p. 7, §7.5 (VIN 12 V, VEN 4 V): non-switching IQ 24 µA typ, 34 µA max; shutdown 5 µA typ, 10 µA max. Light load runs in PFM (minimum peak inductor current 0.69 A typ, p. 8).

## Pinout and package

SNVSAN3F, p. 5, Figure 6-2 and Table 6-1 (RNX).

| Pin | Name | Function |
|---|---|---|
| 1, 11 | PGND | Power ground (−7 V in the IBB) |
| 2, 10 | VIN | Input |
| 3 | NC | No internal connection; connect to SW on the PCB |
| 4 | BOOT | 100 nF to SW |
| 5 | VCC | Internal 5 V LDO; 1 µF to AGND |
| 6 | AGND | Analog ground (−7 V in the IBB) |
| 7 | FB | Feedback divider tap |
| 8 | PG | Open-drain power good |
| 9 | EN | Enable; do not float |
| 12 | SW | Switch node, to the inductor |

Ordering (addendum, p. 42): LMR33630CRNXR, 3000 per reel, MSL 2 at 260 °C (1 year), −40 to 125 °C, marking 33630C.

## Recommended footprint

TI land pattern and stencil for RNX: SNVSAN3F, from p. 49. Not transcribed here: **UNVERIFIED** until the footprint is drawn against those pages.

## Application circuit and required passives

The T1 IBB (board output-stage simulation §5.2, after SNVA856B Figure 3-1 and §5): feedback 100 kΩ (ground to FB) / 16.5 kΩ (FB to −7 V) → VOUT = −1.0 V × (1 + 100 / 16.5) = −7.06 V, 22 pF feed-forward; 2 × 10 µF from VIN to −7 V and 4.7 µF from VIN to ground; output 3 × 22 µF 16 V X7R; BOOT 100 nF; VCC 1 µF; inductor 2.2 µH ([XGL4020-222MEC](../Coilcraft/XGL4020-222MEC.md)).

- **Voltage stress** (SNVA856B §4.1): VIN-to-IC-ground = VSYS + |VOUT| ≤ 9.9 + 7.24 = 17.1 V = 48 % of 36 V.
- **Inductor current** (SNVA856B Eq. 4–6): average IOUT × (1 + |VOUT| / (VIN × η)), largest at the lowest VIN.

## Interfaces and timing

- EN: switching starts at 1.2 / 1.231 / 1.26 V rising, 100 mV hysteresis; ≥ 1 V turns on the internal LDO (p. 7). In the IBB, EN is referenced to the −7 V IC ground, so system logic drives it through a level shifter (SNVA856B §7.1, Figure 7-1).
- VFB 0.985 / 1.0 / 1.015 V (p. 7).
- Current limits (LMR33630): high side 3.85 / 4.5 / 5.05 A; low side (valley) 2.9 / 3.5 / 4.1 A (p. 7).
- Soft start 2.9 / 4 / 6 ms (p. 8). Power good 92–97 % rising, 60–170 µs filter (p. 8).
- fSW, C version, RNX: 1.8 / 2.1 / 2.3 MHz (p. 8). RDS(on) high side 75 / 145 mΩ (RNX, p. 8).

## Linux driver

None. The pre-rail is switched by `HPA_RAIL_EN` through the level shifter (board BOM line 119).

## Simulation models

TI transient models with inverting configurations: SNVMBF9, SNVMBH1, SNVMBG5 (unencrypted; SNVMBG5 used by the board output-stage simulation, run in ngspice with `gmin = 1e-10`). Not in the repository.

## Design notes for the T1

- **Simulated margins** (board output-stage simulation §5.2, VSYS 6.0 V): full-scale sine (433 mA rail peak) inductor peak 1.80 A = 47 % of the 3.85 A high-side minimum; LDO current-limit case (0.78 A DC) 2.13 A = 55 %, valley 1.39 A = 48 % of 2.9 A; 6 mVpp ripple; SNVA856B Eq. 6 cross-check ≤ 63 %.
- **Second source:** LMR33620CRNXR (2 A, same package and pins): 83 % of its 2.9 A high-side minimum at the 0.78 A limit case; datasheet not read here.
- **Light load:** PFM bursts may fall in the audio band at the idle load (**UNVERIFIED**); the LT3094 rejects ≥ 100 dB at 1 kHz.
- **Thermal:** 0.4–0.9 W at 0.78 A (est.); bench item.
- **Stock (2026-10-22):** Mouser 2,748 @ $2.94 (CRNXT 885); LCSC C2071783 1,399 @ $2.15. LMR33620CRNXR: Mouser 33,872 @ $2.27.

## Sources

- TI, LMR33630 datasheet SNVSAN3F: <https://www.ti.com/lit/ds/symlink/lmr33630.pdf>
- TI, SNVA856B: <https://www.ti.com/lit/an/snva856b/snva856b.pdf>
- OpenDAP board ADR 0015; BOM v1.6, lines 116–119; output-stage simulation §5 (`public/board/docs/`).
