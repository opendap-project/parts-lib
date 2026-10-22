# SN74LVC1G27DCKR

- **Manufacturer:** Texas Instruments
- **Function:** Single 3-input positive-NOR gate, 1.65–5.5 V supply, 5.5 V-tolerant inputs, Ioff
- **BOM v1 lines:** 98 (MaskROM combo NOR gate)
- **Package:** SC70-6 (DCK), 0.65 mm pitch
- **Datasheet:** SN74LVC1G27, SCES488E (September 2003, revised December 2013), sha256 `52eba79ea5ba…` in `manifest.toml`
- **Status:** Partly UNVERIFIED

## Summary

The SN74LVC1G27 computes Y = NOT(A + B + C): the output is high only when all three inputs are low (SCES488E Description and Function Table, pp. 1–2). Inputs accept up to 5.5 V at any supply, and Ioff disables the output when the device is unpowered (p. 1). In the T1 it is the AND-of-lows of the MaskROM combo (ADR 0009). Its inputs are PWRON_N (through the BAT54, line 78), VOLDN_N and WINDOW_N (TPS3839, line 97). Its output turns on the DMG1012T (line 35), which pulls eMMC_D0 to GND through 100 Ω. It runs from vcca1v8_pmu (BOM v1 line 98).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, VCC | — | −0.5 | 6.5 | V | SCES488E p. 2, Absolute Maximum Ratings |
| Input voltage, VI | — | −0.5 | 6.5 | V | p. 2 |
| Output voltage, high-impedance or power-off state | — | −0.5 | 6.5 | V | p. 2 |
| Output voltage, high or low state | — | −0.5 | VCC + 0.5 | V | p. 2 |
| Input clamp current, IIK | VI < 0 | — | −50 | mA | p. 2 |
| Output clamp current, IOK | VO < 0 | — | −50 | mA | p. 2 |
| Continuous output current, IO | — | — | ±50 | mA | p. 2 |
| Continuous current through VCC or GND | — | — | ±100 | mA | p. 2 |
| Package thermal impedance, θJA (DCK) | JESD 51-7 | — | 259 | °C/W | p. 2 |
| Storage temperature | — | −65 | 150 | °C | p. 2 |
| ESD, HBM (A114-A) | — | — | 2000 | V | p. 1 |
| ESD, MM (A115-A) | — | — | 200 | V | p. 1 |
| ESD, CDM (C101) | — | — | 1000 | V | p. 1 |

## Recommended operating conditions

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VCC, operating | — | 1.65 | 5.5 | V | p. 3, Recommended Operating Conditions |
| VCC, data retention only | — | 1.5 | — | V | p. 3 |
| VIH | VCC 1.65–1.95 V | 0.65 × VCC | — | V | p. 3 |
| VIL | VCC 1.65–1.95 V | — | 0.35 × VCC | V | p. 3 |
| Input voltage, VI | — | 0 | 5.5 | V | p. 3 |
| Output voltage, VO | — | 0 | VCC | V | p. 3 |
| IOH / IOL | VCC = 1.65 V | — | −4 / 4 | mA | p. 3 |
| Input transition rise or fall rate, Δt/Δv | VCC = 1.8 V ± 0.15 V | — | 20 | ns/V | p. 3 |
| Input transition rise or fall rate, Δt/Δv | VCC = 3.3 V ± 0.3 V | — | 10 | ns/V | p. 3 |
| Operating free-air temperature | — | −40 | 125 | °C | p. 3 |

Unused inputs must be held at VCC or GND (p. 3, note 1).

### Electrical characteristics (selected, −40 to 85 °C)

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VOH | IOH = −100 µA, VCC 1.65–5.5 V | VCC − 0.1 | — | V | p. 4, Electrical Characteristics |
| VOH | IOH = −4 mA, VCC = 1.65 V | 1.2 | — | V | p. 4 |
| VOL | IOL = 100 µA, VCC 1.65–5.5 V | — | 0.1 | V | p. 4 |
| VOL | IOL = 4 mA, VCC = 1.65 V | — | 0.45 | V | p. 4 |
| Input current, II | VI = 5.5 V or GND, VCC 0–5.5 V | — | ±5 | µA | p. 4 |
| Ioff | VCC = 0, VI or VO = 5.5 V | — | ±10 | µA | p. 4 |
| Input capacitance, Ci | VCC = 3.3 V | — | 3.5 typ | pF | p. 4 |

## Power by mode

| Mode | Condition | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|
| Static, ICC | VI = 5.5 V or GND, IO = 0, VCC 1.65–5.5 V | — | 10 | µA | p. 4 |
| Extra current per input at VCC − 0.6 V, ΔICC | VCC 3–5.5 V | — | 500 | µA | p. 4 |
| Dynamic | Cpd at VCC = 1.8 V, f = 10 MHz, 25 °C | 17 | — | pF | p. 5, Operating Characteristics |

ΔICC is specified only for VCC ≥ 3 V; the figure for an input resting between rails at VCC = 1.8 V is not given (**UNVERIFIED**).

## Pinout and package

DCK pin numbers (top view, p. 1):

| Pin | Name | Description |
|---|---|---|
| 1 | A | Input |
| 2 | GND | Ground |
| 3 | B | Input |
| 4 | Y | Output, Y = NOT(A + B + C) |
| 5 | VCC | Supply |
| 6 | C | Input |

Outline DCK0006A (drawing 4214835/D, p. 13): body 1.85–2.15 × 1.1–1.4 mm, lead span 1.8–2.4 mm, 0.65 mm pitch, 1.1 mm maximum height; JEDEC MO-203 variation AB. MSL Level-1-260C-UNLIM, NiPdAu or Sn, −40 to 125 °C, reel 3000 (p. 9).

## Recommended footprint

DCK0006A example board layout (p. 14, drawing 4214835/D): 6 pads 0.9 × 0.4 mm (reference), 0.65 mm pitch, 2.2 mm between pad-column centres (reference); non-solder-mask-defined preferred, 0.07 mm maximum mask clearance. Stencil on p. 15. This is the same outline and drawing as the SN74AXC1T45DCKR.

## Application circuit and required passives

The datasheet gives no application circuit or bypass value. A 0.1 µF bypass capacitor on VCC is the design choice (**UNVERIFIED** against the datasheet). Every input must be at a valid level (p. 3, note 1): in the T1 each input has a pull-up to the 1.8 V domain on its net.

## Interfaces and timing

Function table (p. 2):

| A | B | C | Y |
|---|---|---|---|
| H | X | X | L |
| X | H | X | L |
| X | X | H | L |
| L | L | L | H |

Propagation delay, A, B or C to Y, −40 to 85 °C (p. 4):

| VCC | CL = 15 pF | CL = 30 or 50 pF | Unit |
|---|---|---|---|
| 1.8 V ± 0.15 V | 2–18.2 | 2.2–20.5 | ns |
| 3.3 V ± 0.3 V | 1–4.5 | 1.3–5.4 | ns |

At −40 to 125 °C and CL = 30 or 50 pF, the maximum at 1.8 V is 23.3 ns (p. 5). The same p. 5 table also lists fmax and PRE/CLR/CLK rows that do not apply to a combinational gate; they are ignored here.

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. Whether TI publishes an IBIS model for this device is **UNVERIFIED**.

## Design notes for the T1

- **Logic.** Y is high only when PWRON_N, VOLDN_N and WINDOW_N are all low (Function Table, p. 2). Power alone, Vol− alone, or any press after the TPS3839 window has closed (WINDOW_N high) keeps Y low, as BOM v1 line 98 requires.
- **Thresholds at 1.8 V.** VIL is 0.35 × VCC ≈ 0.63 V and VIH is 0.65 × VCC ≈ 1.17 V (p. 3). The PWRON_N input sits at the BAT54 anode, so its "low" equals the BAT54 forward voltage at the pull-up current. That drop must stay below 0.63 V over temperature (BAT54 sheet; RK809 PWRON idle level is **UNVERIFIED** per BOM v1 line 78). The VOLDN_N node on SARADC_VIN1 must reach below 0.63 V when Vol− is pressed.
- **Slow inputs.** The datasheet limits input transitions to 20 ns/V at VCC = 1.8 V (p. 3). Button nodes, any RC debounce and the TPS3839 power-up ramp are far slower. The inputs have no specified hysteresis, so a slow edge may cause output chatter and extra supply current while it crosses the threshold. Chatter on Y only toggles the D0 pull-down during a press inside the window, but the effect on the BootROM and on the always-on rail current is **UNVERIFIED**. A gate with Schmitt-trigger inputs would remove the question; no such part has been checked in this sheet.
- **Always-on current.** On vcca1v8_pmu the gate draws at most 10 µA static (p. 4), plus the current of the input pull-ups whenever an input is held low.
- **Output drive.** Y drives only the DMG1012T gate; at 1.65 V the output sources up to 4 mA with VOH ≥ 1.2 V (p. 4). The MOSFET must be fully on at that gate voltage (DMG1012T VGS(th) ≤ 1.0 V per BOM v1 line 35).

## Sources

- TI, *SN74LVC1G27 Single 3-Input Positive-NOR Gate*, SCES488E, revised December 2013, <https://www.ti.com/lit/ds/symlink/sn74lvc1g27.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 35, 78, 97, 98
