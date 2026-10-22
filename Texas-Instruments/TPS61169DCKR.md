# Texas Instruments TPS61169DCKR

- **Function:** boost white-LED driver, 40 V / 1.8 A integrated switch, 204 mV feedback, PWM-controlled analog dimming
- **T1 use:** board BOM v1 line 51 (Power), panel backlight; inductor line 52, rectifier line 53; status Proposed
- **Datasheet:** TPS61169 38V High Current-Boost WLED Driver With PWM Control, SNVSA40B (October 2014, revised June 2024), <https://www.ti.com/lit/ds/symlink/tps61169.pdf>
- **Package:** SC70 5-pin (DCK, drawing DCK0005A), 2.00 × 1.25 mm nominal body

## Summary

The TPS61169 is a 1.2 MHz current-mode boost converter for series LED strings up to 38 V, with a 40 V, 1.8 A switch (1.2 A minimum current limit), a 204 mV feedback reference, open-LED protection, soft start and thermal foldback (SNVSA40B p. 1, §1 and §3). A PWM signal on CTRL scales the internal reference, so the LED current is DC, not chopped (p. 9, §6.3.5). In the T1 it sits on the main board, powered from VSYS, and drives the Focus E35GH panel's 5S2P LED array at up to 60 mA through the faceplate FPC (BOM line 51, power tree §4.5).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| VIN, CTRL, PWM, FB | −0.3 | 7 | V | SNVSA40B p. 4, §5.1 |
| SW | −0.3 | 40 | V | p. 4, §5.1 |
| Operating junction temperature | −40 | 150 | °C | p. 4, §5.1 |
| Storage temperature | −65 | 150 | °C | p. 4, §5.1 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 4, §5.2 |
| ESD, CDM (JESD22-C101) | — | ±500 | V | p. 4, §5.2 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Input voltage VIN | 2.7 | — | 5.5 | V | SNVSA40B p. 4, §5.3 |
| Output voltage VOUT | VIN | — | 38 | V | p. 4, §5.3 |
| Inductor L | 4.7 | — | 10 | µH | p. 4, §5.3 |
| Input capacitor | 1 | — | — | µF | p. 4, §5.3 |
| Output capacitor | 1 | — | 10 | µF | p. 4, §5.3 |
| PWM dimming frequency | 5 | — | 100 | kHz | p. 4, §5.3 |
| PWM dimming duty cycle | 1 | — | 100 | % | p. 4, §5.3 |
| Junction temperature | −40 | — | 125 | °C | p. 4, §5.3 |
| Feedback reference VREF (duty 100 %, TA ≥ 25 °C) | 188 | 204 | 220 | mV | p. 5, §5.5 |
| FB bias current (VFB = 204 mV) | — | — | 2.5 | µA | p. 5, §5.5 |
| Switch RDS(on) | — | 0.35 | 0.7 | Ω | p. 5, §5.5 |
| Switching frequency (VIN = 3 V) | 0.75 | 1.2 | 1.5 | MHz | p. 5, §5.5 |
| Switch current limit (D = DMAX, TA ≤ 85 °C) | 1.2 | 1.8 | 2.4 | A | p. 5, §5.5 |
| Start-up current limit (TA ≤ 85 °C) | — | 0.72 | — | A | p. 5, §5.5 |
| Output overvoltage threshold VOVP | 36 | 37.5 | 39 | V | p. 5, §5.5 |
| UVLO, VIN falling / rising | — | 2.3 / 2.6 | — | V | p. 5, §5.5 |
| Thermal shutdown / hysteresis | — | 160 / 15 | — | °C | p. 5, §5.5 |

Thermal (DCK, p. 4, §5.4): RθJA 263.8 °C/W, RθJC(top) 76.1 °C/W, RθJB 51.4 °C/W, ψJB 50.7 °C/W. Thermal foldback reduces ILIM above TJ = 100 °C (p. 10, §6.3.7). The orderable TPS61169DCKR is listed for −40 to 85 °C (p. 18, Package Option Addendum).

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Shutdown | CTRL = GND | 1 | 2 | µA | SNVSA40B p. 5, §5.5 |
| Operating, no load | enabled, switching at 1.2 MHz | 0.3 | 0.45 | mA | p. 5, §5.5 |
| Running | VIN = 3.6 V, 10 LEDs, RSET = 10.2 Ω | efficiency vs dimming duty given as curves only | — | — | p. 14, Figures 7-2 to 7-5 |

Shutdown leaves a DC path VIN → inductor → diode → LEDs; the LED string's minimum forward voltage must exceed the maximum VIN to keep the LEDs dark (p. 9, §6.3.3).

## Pinout and package

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | SW | I | Drain of the internal power FET |
| 2 | GND | O | Ground |
| 3 | FB | I | Current feedback; sense resistor RSET from FB to GND |
| 4 | CTRL | I | Enable and PWM dimming input |
| 5 | VIN | I | Supply input |

Source: SNVSA40B p. 3, Table 4-1. Marking SZL, MSL 1 at 260 °C (p. 18). SC70, 1.1 mm maximum height (p. 21, DCK0005A). Tape 8 mm, 4 mm pitch, pin 1 in Q3, 3000 per reel (p. 19).

## Recommended footprint / land pattern

TI example board layout DCK0005A (SNVSA40B p. 22): five pads 0.95 × 0.4 mm, pitch 0.65 mm (pins 1–3 side), 1.3 mm between pins 1 and 3 centres, 2.2 mm between pad-row centres, corner radius 0.05 mm, non-solder-mask-defined preferred (0.07 mm mask clearance). Stencil example on p. 23. Board layout example: Figure 7-15 (p. 16).

## Application circuit and required passives

- **RSET:** ILED = VFB / RSET (p. 9, §6.3.4, Equation 1). The T1 uses 3.40 Ω 1 % for 60 mA (power tree §4.5); dissipation 0.204 V × 60 mA = 12 mW.
- **Inductor:** 4.7–10 µH (p. 4, §5.3; p. 12, §7.2.2.1). Peak current IL(P) = IL(DC) + ΔIL/2 with IL(DC) = VOUT × IOUT / (VIN × η) and ΔIL = 1 / (L × (1/(VOUT − VIN) + 1/VIN) × FS) (p. 12, Equations 3–5). Inductance may fall 20–35 % near saturation (p. 12). TI's listed parts: Coilcraft LPS4018-103ML (10 µH, 1.3 A sat), Cyntec PCMB051H-100M (10 µH, 3 A sat) (p. 12, Table 7-2).
  - T1 calculation (worst case VIN = 3.5 V, VOUT = 16.5 V + 0.204 V, IOUT = 60 mA, η = 0.85, L = 10 µH, FS = 1.2 MHz): IL(DC) = 0.34 A, ΔIL = 0.23 A, IL(P) = 0.45 A. This matches power tree §4.5; the BOM line 52 inductor (Murata LQH3NPN100MJRL) must saturate above this with margin (its rating is **UNVERIFIED**, datasheet not downloaded).
- **Schottky diode:** low VF, fast, low capacitance; average and peak current above the output and peak inductor currents; reverse breakdown above the open-LED protection voltage (p. 12, §7.2.2.2). TI recommends onsemi NSR0240.
- **Output capacitor:** 1–4.7 µF ceramic recommended (p. 13, §7.2.2.3); COUT ≥ (VOUT − VIN) × IOUT / (VOUT × FS × Vripple) (Equation 6). It sees up to VOVP (39 V max) in an open-LED event; choose its voltage rating accordingly (design inference).
- **Input capacitor:** ≥ 1 µF (p. 4); 4.7 µF in the typical application (p. 11, Figure 7-1).
- **Layout:** CIN close to VIN, SW loop short and wide, COUT ground close to GND, RSET close to FB, signal ground joined to power ground at one point near GND (p. 16, §7.5.1).

## Interfaces and timing

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| CTRL logic high VH | 1.2 | — | — | V | SNVSA40B p. 5, §5.5 |
| CTRL logic low VL | — | — | 0.4 | V | p. 5, §5.5 |
| CTRL internal pull-down | — | 300 | — | kΩ | p. 5, §5.5 |
| CTRL low time to shutdown | — | 2.5 | — | ms | p. 5, §5.5 |
| VREF filter time constant | — | 1 | — | ms | p. 5, §5.5 |
| Soft-start reduced current limit period | — | 6.5 | — | ms | p. 5, §5.5; p. 8, §6.3.1 |

- Dimming: VFB = duty × 204 mV (p. 9, Equation 2). The regulation voltage does not depend on the PWM logic level (p. 9).
- Below 5 kHz the internal filter no longer smooths the reference; output ripple grows and audible noise may result (p. 9).
- Open-LED protection: if SW exceeds VOVP and FB stays below 30 mV for three switching cycles, the device shuts down and stays off until CTRL is toggled (p. 8, §6.3.2).

## Linux driver

`pwm-backlight` (Kconfig `BACKLIGHT_PWM`, enabled as a module in Debian per BOM v1) driving CTRL from a SoC PWM; the TPS61169 itself has no register interface. A `power-supply` or `enable-gpios` property is not needed because CTRL is both enable and dimming input. Mainline driver presence is from the BOM driver column; the DT binding details are **UNVERIFIED** for this board.

## Simulation models available

No model is listed in `manifest.toml`. A TI PSpice or TINA model is **UNVERIFIED** (not checked).

## Design notes for the T1

- **LED current tolerance:** with RSET = 3.40 Ω, VREF 188–220 mV gives 55.3–64.7 mA (calculation from p. 5). Check the upper figure against the panel's LED maximum current (Focus spec sheet), or size RSET for the VREF maximum.
- **Diode rating margin:** the diode must block above the OVP threshold (p. 12). VOVP is 39 V maximum (p. 5); the BOM line 53 PMEG4010CEH is a 40 V part (its datasheet is **UNVERIFIED**, not downloaded), which leaves 1 V of margin at the OVP maximum. TI's recommended NSR0240 is also a 40 V class part (rating not stated in this datasheet).
- **PWM and shutdown:** keep the dimming PWM between 5 and 100 kHz. A 0 % duty held for 2.5 ms or longer shuts the device down, and the next turn-on runs the 6.5 ms soft start (pp. 5, 8–9). The `pwm-backlight` minimum brightness should map to a non-zero duty if the panel must stay lit at its lowest level.
- **Shutdown leakage path:** the panel string VF minimum is 14.0 V (power tree §4.5), far above VSYS maximum 4.4 V, so the LEDs stay dark in shutdown (p. 9, §6.3.3).
- **Temperature grade:** the DCKR orderable is listed at −40 to 85 °C (p. 18) while TJ operates to 125 °C (p. 4); check this against the T1 internal temperature once modelled (power tree risk 10).
- **Other faceplates:** VOUT up to 38 V and OVP 36–39 V bound the string length for future faceplates (BRD-048).

## Sources

- TI, TPS61169 datasheet, SNVSA40B, revised June 2024, <https://www.ti.com/lit/ds/symlink/tps61169.pdf>, sha256 `7d0b8ace2459a9fd22fe7145086cbad4ccb3bb43219247459313fcba75230151` (manifest). Page numbers are PDF page numbers.
- OpenDAP board BOM v1 lines 51–53 and power tree v0 §4.5 (T1 context).
