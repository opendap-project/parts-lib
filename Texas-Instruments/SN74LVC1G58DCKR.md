# SN74LVC1G58DCKR

- **Manufacturer:** Texas Instruments
- **Function:** Configurable multiple-function gate (3-bit input), Schmitt-trigger inputs, 1.65–5.5 V supply, 5.5 V-tolerant inputs, Ioff
- **BOM v1 lines:** 98 (MaskROM combo gate 2, wired as a 2-input AND with one inverted input, qty 1; replaces SN74LVC1G27DCKR together with the SN74LVC1G57DCKR in BOM v1.1)
- **Package:** SC70-6 (DCK, DCK0006A), 2.0 × 1.25 mm nominal, 0.65 mm pitch
- **Datasheet:** *SN74LVC1G58 Configurable Multiple-Function Gate*, SCES415N, November 2002, revised December 2013. Cited below as "SCES415N". File sha256 `c9f14665a6c5631feeee9a82ccb5328b51a83ad3ea90c49e2d53713520877e8a` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The SN74LVC1G58 sets its output from eight patterns of a 3-bit input; tying inputs to VCC or GND selects AND, OR, NAND, NOR, XOR, inverter or noninverter (SCES415N, p. 1). Its inputs are Schmitt triggers and accept up to 5.5 V at any supply; Ioff disables the output when unpowered (p. 1). Its function table is the complement of the SN74LVC1G57's. In the T1 it is gate 2 of the MaskROM combo (ADR 0009): In2 = WINDOW_N (TPS3839, line 97), In1 = VCC, In0 = BOTH (gate 1, [SN74LVC1G57DCKR](SN74LVC1G57DCKR.md)). Its output drives the DMG1012T (line 35), which pulls eMMC_D0 to GND through 100 Ω. It runs from vcca1v8_pmu (BOM v1 line 98).

## Absolute maximum ratings

SCES415N, p. 4.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| Supply voltage VCC | −0.5 | 6.5 | V |
| Input voltage VI | −0.5 | 6.5 | V |
| VO, high-impedance or power-off state | −0.5 | 6.5 | V |
| VO, high or low state | −0.5 | VCC + 0.5 | V |
| Input clamp current IIK (VI < 0) | — | −50 | mA |
| Output clamp current IOK (VO < 0) | — | −50 | mA |
| Continuous output current IO | — | ±50 | mA |
| Continuous current through VCC or GND | — | ±100 | mA |
| Package thermal impedance θJA, DCK (JESD 51-7) | — | 259 | °C/W |
| Storage temperature Tstg | −65 | 150 | °C |

ESD (p. 1): HBM 2000 V (A114-A), MM 200 V (A115-A), CDM 1000 V (C101).

## Recommended operating conditions

SCES415N, p. 4.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VCC, operating | — | 1.65 | 5.5 | V |
| VCC, data retention only | — | 1.5 | — | V |
| VI | — | 0 | 5.5 | V |
| VO | — | 0 | VCC | V |
| IOH / IOL | VCC = 1.65 V | — | −4 / 4 | mA |
| IOH / IOL | VCC = 3 V | — | −24 / 24 | mA |
| TA | — | −40 | 125 | °C |

All unused inputs must be held at VCC or GND (p. 4, note 1). No input transition-rate limit is listed.

### Electrical characteristics (selected)

SCES415N, p. 5; the same limits apply at −40 to 85 °C and −40 to 125 °C unless noted.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VT+, positive-going threshold | VCC = 1.65 V | 0.79 | 1.16 | V |
| VT−, negative-going threshold | VCC = 1.65 V | 0.35 | 0.62 | V |
| ΔVT, hysteresis | VCC = 1.65 V | 0.3 | 0.62 | V |
| VT+ | VCC = 2.3 V | 1.11 | 1.56 | V |
| VT− | VCC = 2.3 V | 0.58 | 0.87 | V |
| ΔVT | VCC = 2.3 V | 0.4 | 0.8 | V |
| VOH | VCC 1.65–5.5 V, IOH = −100 µA | VCC − 0.1 | — | V |
| VOH | VCC = 1.65 V, IOH = −4 mA | 1.2 | — | V |
| VOL | VCC 1.65–5.5 V, IOL = 100 µA | — | 0.1 | V |
| VOL | VCC = 1.65 V, IOL = 4 mA | — | 0.45 | V |
| II | VCC 0–5.5 V, VI = 5.5 V or GND | — | ±1 | µA |
| Ioff | VCC = 0, VI or VO = 5.5 V | — | ±10 | µA |
| Ci | VCC = 3.3 V | 3.5 typ | — | pF |

Thresholds are tabulated at VCC = 1.65 V and 2.3 V only; values at the 1.8 V operating point are not given (**UNVERIFIED** by interpolation).

## Power by mode

| Mode | Condition | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|
| Static, ICC | VCC 1.65–5.5 V, VI = 5.5 V or GND, IO = 0 | — | 10 | µA | p. 5 |
| Extra current per input at VCC − 0.6 V, ΔICC | VCC 3–5.5 V | — | 500 | µA | p. 5 |
| Dynamic | Cpd at VCC = 1.8 V, f = 10 MHz, 25 °C | 22 | — | pF | p. 6 |

ΔICC is specified only for VCC ≥ 3 V; the supply current while a slow input crosses the thresholds at VCC = 1.8 V is not given (**UNVERIFIED**).

## Pinout and package

DCK pin numbers, top view (SCES415N, p. 1):

| Pin | Name | Description |
|---|---|---|
| 1 | In1 | Logic input 1 |
| 2 | GND | Ground |
| 3 | In0 | Logic input 0 |
| 4 | Y | Logic output |
| 5 | VCC | Supply |
| 6 | In2 | Logic input 2 |

The pin names and numbers equal those of the SN74LVC1G57 DCK package (SCES414P, p. 3). Outline DCK0006A (drawing 4214835/D 11/2024, p. 15): body 1.85–2.15 × 1.1–1.4 mm, lead span 1.8–2.4 mm, 0.65 mm pitch, 1.1 mm maximum height. Orderable SN74LVC1G58DCKR: active, 3000 per reel, NiPdAu or Sn, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking one of CP5, CPF, CPK, CPR (p. 9, orderable addendum).

## Recommended footprint

DCK0006A example board layout (p. 16, drawing 4214835/D): 6 pads 0.9 × 0.4 mm (reference), 0.65 mm pitch, 2.2 mm between pad-column centres (reference); 0.07 mm maximum mask clearance (non-solder-mask-defined) or 0.07 mm minimum (solder-mask-defined). Stencil on p. 17. Same land as the [SN74LVC1G57DCKR](SN74LVC1G57DCKR.md).

## Application circuit and required passives

The SCES415N datasheet gives no application circuit or bypass value. A 0.1 µF bypass on VCC follows the SN74LVC1G57 datasheet's single-supply recommendation (SCES414P, p. 12, §10); for this part it is **UNVERIFIED** against its own datasheet. In1 is tied to VCC (BOM v1 line 98). Every input must be at a valid level (p. 4, note 1).

## Interfaces and timing

Function table (p. 2):

| In2 | In1 | In0 | Y |
|---|---|---|---|
| L | L | L | L |
| L | L | H | H |
| L | H | L | L |
| L | H | H | H |
| H | L | L | H |
| H | L | H | H |
| H | H | L | L |
| H | H | H | L |

Propagation delay, any input to Y (p. 6): VCC = 1.8 V ± 0.15 V, 3.2–14.4 ns at −40 to 85 °C and 3.2–16.4 ns at −40 to 125 °C (CL = 30 pF, RL = 1 kΩ, p. 7).

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. The datasheet names no simulation model; whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **Logic check of the BOM wiring.** With In1 = VCC, the function table reduces to the rows In1 = H: (In2, In0) = (L, L) → L; (L, H) → H; (H, L) → L; (H, H) → L. So Y = In0 AND NOT In2 = BOTH AND NOT WINDOW_N. WINDOW_N is the TPS3839 active-low RESET, low during the delay td after vcc_1v8 rises ([TPS3839G18DBZR](TPS3839G18DBZR.md)), so Y is high only when both buttons are pressed inside the window, as BOM v1 line 98 states. Confirmed.
- **Hysteresis.** ΔVT is 0.30–0.62 V at VCC = 1.65 V (p. 5), as BOM v1 line 98 states.
- **WINDOW_N levels.** The TPS3839 RESET gives VOH ≥ VDD − 0.4 V at −0.5 mA and VOL ≤ 0.4 V at 0.5 mA ([TPS3839G18DBZR](TPS3839G18DBZR.md)). VOH ≈ 1.4 V clears VT+ maximum 1.16 V. The 0.4 V VOL figure is above the 0.35 V VT− minimum; into a CMOS input of ±1 µA leakage the actual low level is far lower, but the datasheet gives no VOL at that current (**UNVERIFIED**).
- **Undefined window at power-up.** Before vcc_1v8 reaches the TPS3839 V(POR) (0.6 V max), WINDOW_N is undefined while this gate may already be powered from vcca1v8_pmu. A low there only opens the window early, and Y still needs BOTH high ([TPS3839G18DBZR](TPS3839G18DBZR.md)).
- **Output drive.** Y drives only the DMG1012T gate: VOH ≥ 1.2 V at −4 mA and VCC − 0.1 V at −100 µA (p. 5). The MOSFET must be fully on at that gate voltage (DMG1012T VGS(th) ≤ 1.0 V per BOM v1 line 35).
- **Always-on current.** At most 10 µA static on vcca1v8_pmu (p. 5).

## Sources

- TI, *SN74LVC1G58 Configurable Multiple-Function Gate*, SCES415N (December 2013): <https://www.ti.com/lit/ds/symlink/sn74lvc1g58.pdf>
- TI, SN74LVC1G57, SCES414P (November 2016), for the bypass recommendation and pinout comparison: <https://www.ti.com/lit/ds/symlink/sn74lvc1g57.pdf>
- OpenDAP board BOM v1 (v1.1), lines 35, 97, 98 and §9 D10 (`public/board/docs/specs/bom-v1.md`).
