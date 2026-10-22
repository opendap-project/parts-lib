# SN74LVC1G57DCKR

- **Manufacturer:** Texas Instruments
- **Function:** Configurable multiple-function gate (3-bit input), Schmitt-trigger inputs, 1.65–5.5 V supply, 5.5 V-tolerant inputs, Ioff
- **BOM v1 lines:** 98 (MaskROM combo gate 1, wired as a 2-input NOR, qty 1; replaces SN74LVC1G27DCKR in BOM v1.1)
- **Package:** SC70-6 (DCK, DCK0006A), 2.0 × 1.25 mm nominal, 0.65 mm pitch
- **Datasheet:** *SN74LVC1G57 Configurable Multiple-Function Gate*, SCES414P, November 2002, revised November 2016. Cited below as "SCES414P". File sha256 `078364de617898af0dd4cee99931ab1d36b622824a06e8f9b7fa95087644af24` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The SN74LVC1G57 sets its output from eight patterns of a 3-bit input; tying inputs to VCC or GND selects AND, OR, NAND, NOR, XNOR, inverter or buffer (SCES414P, p. 1; p. 8, §8.1). Its inputs are Schmitt triggers, accept up to 5.5 V at any supply, and Ioff disables the output when unpowered (p. 1; p. 8, §8.3). In the T1 it is gate 1 of the MaskROM combo (ADR 0009): In2 = PWRON_N (through the BAT54, line 78), In1 = GND, In0 = VOLDN_N, so its output BOTH is high only while Power and Vol− are both pressed. It runs from vcca1v8_pmu and replaces the SN74LVC1G27, whose inputs had no specified hysteresis (BOM v1 line 98; §9 D10).

## Absolute maximum ratings

SCES414P, p. 4, §6.1 and §6.2.

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
| Junction temperature TJ | — | 150 | °C |
| Storage temperature Tstg | −65 | 150 | °C |

ESD: HBM ±2000 V; CDM ±1000 V (p. 4, §6.2).

## Recommended operating conditions

SCES414P, p. 4, §6.3.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VCC, operating | — | 1.65 | 5.5 | V |
| VCC, data retention only | — | 1.5 | — | V |
| VI | — | 0 | 5.5 | V |
| VO | — | 0 | VCC | V |
| IOH / IOL | VCC = 1.65 V | — | −4 / 4 | mA |
| IOH / IOL | VCC = 3 V | — | −24 / 24 | mA |
| TA | DCK and other leaded packages | −40 | 125 | °C |

All unused inputs must be held at VCC or GND (p. 4, note 1). The table sets no input transition-rate limit; a Schmitt-trigger input has no rise and fall time limitation (p. 11, §9.2.1.2).

Thermal, DCK (p. 5, §6.4): RθJA 271.7 °C/W, RθJC(top) 129.8 °C/W, RθJB 73.1 °C/W, ψJT 8.3 °C/W, ψJB 72.4 °C/W.

### Electrical characteristics (selected)

SCES414P, p. 5, §6.5, over the recommended temperature range.

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
| Ioff | VCC = 0 V, VI or VO = 5.5 V | — | ±10 | µA |
| Ci | VCC = 3.3 V | 3.5 typ | — | pF |

Thresholds are tabulated at VCC = 1.65 V and 2.3 V only; values at the 1.8 V operating point are not given (**UNVERIFIED** by interpolation).

## Power by mode

| Mode | Condition | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|
| Static, ICC | VCC 1.65–5.5 V, VI = 5.5 V or GND, IO = 0 | — | 10 | µA | p. 5 |
| Extra current per input at VCC − 0.6 V, ΔICC | VCC 3–5.5 V | — | 500 | µA | p. 5 |
| Dynamic | Cpd at VCC = 1.8 V, f = 10 MHz, 25 °C | 20 | — | pF | p. 6 |

ΔICC is specified only for VCC ≥ 3 V; the supply current while a slow input crosses the thresholds at VCC = 1.8 V is not given (**UNVERIFIED**).

## Pinout and package

DCK pin numbers, top view (SCES414P, p. 3, Pin Functions):

| Pin | Name | Description |
|---|---|---|
| 1 | In1 | Logic input 1 |
| 2 | GND | Ground |
| 3 | In0 | Logic input 0 |
| 4 | Y | Logic output |
| 5 | VCC | Supply |
| 6 | In2 | Logic input 2 |

Outline DCK0006A (drawing 4214835/D 11/2024, p. 28): body 1.85–2.15 × 1.1–1.4 mm, lead span 1.8–2.4 mm, 0.65 mm pitch, 1.1 mm maximum height. Orderable SN74LVC1G57DCKR: active, 3000 per reel, NiPdAu or Sn, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking one of CL5, CLF, CLJ and others (orderable addendum, p. 14).

## Recommended footprint

DCK0006A example board layout (p. 29, drawing 4214835/D): 6 pads 0.9 × 0.4 mm (reference), 0.65 mm pitch, 2.2 mm between pad-column centres (reference); 0.07 mm maximum mask clearance (non-solder-mask-defined) or 0.07 mm minimum (solder-mask-defined). Stencil on p. 30. Same outline and drawing number as the [SN74LVC1G58DCKR](SN74LVC1G58DCKR.md) and the [SN74LVC1G27DCKR](SN74LVC1G27DCKR.md) it replaces.

## Application circuit and required passives

| Ref | Value | Note |
|---|---|---|
| CVCC | 0.1 µF | Single-supply bypass, as close to VCC as possible (p. 12, §10) |
| Input pull-ups | value not given | Every input must be at a valid level (p. 4, note 1); the T1 circuit sets PWRON_N and VOLDN_N with pull-ups to the 1.8 V domain (BOM v1 line 78) |

The datasheet example (p. 10, Figure 9) uses 10 kΩ pull-ups and 0.1 µF on the inputs, as a reference for an RC-filtered switch input.

## Interfaces and timing

Function table (p. 8, Table 1):

| In2 | In1 | In0 | Y |
|---|---|---|---|
| L | L | L | H |
| L | L | H | L |
| L | H | L | H |
| L | H | H | L |
| H | L | L | L |
| H | L | H | L |
| H | H | L | H |
| H | H | H | H |

Propagation delay, any input to Y (p. 6, §6.6): VCC = 1.8 V ± 0.15 V, 3.2–14.4 ns at −40 to 85 °C and 3.2–16.4 ns at −40 to 125 °C (CL = 30 pF, RL = 1 kΩ, p. 7).

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. The datasheet names no simulation model; whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **Logic check of the BOM wiring.** With In1 = GND, Table 1 reduces to the rows In1 = L: (In2, In0) = (L, L) → H; (L, H) → L; (H, L) → L; (H, H) → L. So Y = NOT(In2 OR In0), a 2-input NOR of PWRON_N and VOLDN_N. Both buttons pull their nets low when pressed, so BOTH is high only when Power and Vol− are pressed together, as BOM v1 line 98 states. Confirmed.
- **Hysteresis.** ΔVT is 0.30–0.62 V at VCC = 1.65 V (p. 5), as BOM v1 line 98 states. Slow button edges and RC debounce are allowed (p. 11, §9.2.1.2).
- **PWRON_N low level against VT−.** A Schmitt input is guaranteed to switch low only below VT− minimum, 0.35 V at VCC = 1.65 V (p. 5); the SN74LVC1G27's VIL was 0.35 × VCC ≈ 0.63 V. In2 sees the BAT54 forward voltage above the pressed PWRON level. BAT54 VF is 240 mV maximum at 0.1 mA and 320 mV at 1 mA ([BAT54](../Nexperia/BAT54.md)), which leaves 110 mV and 30 mV of margin against 0.35 V if PWRON sits at 0 V when pressed. Keep the In2 pull-up current near 0.1 mA or below (≥ 18 kΩ from 1.8 V, a design estimate), and confirm the RK809 PWRON level when pressed (**UNVERIFIED**, BOM v1 line 78).
- **VOLDN_N low level.** The SARADC_VIN1 node must fall below 0.35 V when Vol− is pressed; its divider is not yet fixed (**UNVERIFIED**).
- **Always-on current.** At most 10 µA static on vcca1v8_pmu (p. 5), plus the pull-up currents while a button is held.
- **Output.** Y drives In0 of the SN74LVC1G58 only; VOH ≥ 1.2 V at −4 mA and VCC − 0.1 V at −100 µA (p. 5) is far above that gate's VT+ maximum of 1.16 V.

## Sources

- TI, *SN74LVC1G57 Configurable Multiple-Function Gate*, SCES414P (November 2016): <https://www.ti.com/lit/ds/symlink/sn74lvc1g57.pdf>
- OpenDAP board BOM v1 (v1.1), lines 35, 78, 97, 98 and §9 D10 (`public/board/docs/specs/bom-v1.md`).
