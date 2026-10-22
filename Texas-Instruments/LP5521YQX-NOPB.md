# LP5521YQX/NOPB

- **Manufacturer:** Texas Instruments
- **Function:** Three-channel RGB LED driver with 25.5 mA programmable current sources, 8-bit PWM, three program engines, I2C interface and an adaptive 1×/1.5× charge pump
- **BOM v1 lines:** 105 (RGB status LED driver on the main board for the faceplate LED of line 79, qty 1; new in BOM v1.2, change 7)
- **Package:** WQFN-24 (NJA0024A), 5.0 × 4.0 mm nominal, 0.5 mm pitch, 0.8 mm max height, exposed thermal pad
- **Datasheet:** *LP5521 Three-Channel RGB, White-LED Driver With Internal Program Memory and Integrated Charge Pump*, SNVS441I, January 2007, revised November 2016. Cited below as "SNVS441I". File sha256 `095c9a07852dbef1a85d26afebefc23f2f8f001c7b5d89512bd31d0ebc37011f` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The LP5521 drives three LEDs from constant current sources programmable to 25.5 mA in 100 µA steps, each with 8-bit PWM and its own program engine; an adaptive charge pump selects 1× or 1.5× gain from the LED headroom, and the device enters an automatic power-save mode when no output is active (SNVS441I, p. 1; p. 13, §7.3.2). It needs four ceramic capacitors and no inductor (p. 1). LP5521YQX/NOPB is the WQFN (NJA) version on a 4500-piece reel (p. 42, orderable addendum). In the T1 it sits on the main board, powered from VSYS, and drives the faceplate RGB status LED (Everlight [19-337/R6GHBHC-A01/2T](../Everlight/19-337-R6GHBHC-A01-2T.md)) over LED_R, LED_G and LED_B on the faceplate connector; the charge pump keeps the green and blue dies (VF up to 3.8 V) lit as VSYS falls toward 3.0 V (BOM v1 line 105 and v1.2 change 7; power tree v0 rail table, LED_R/G/B).

## Absolute maximum ratings

SNVS441I, p. 5, §6.1. Voltages to GND.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VDD, VOUT, R, G, B | −0.3 | 6 | V |
| Logic pins | −0.3 | VDD + 0.3, 6 V max | V |
| Continuous power dissipation | internally limited | | |
| Junction temperature TJ-MAX | | 125 | °C |
| Storage Tstg | −65 | 150 | °C |

- Thermal shutdown engages at TJ = 150 °C typ and releases at 130 °C typ (p. 5, note 4).
- ESD (p. 5, §6.2): HBM ±2000 V; CDM ±200 V.

## Recommended operating conditions

SNVS441I, p. 5, §6.3.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VDD | 2.7 | 5.5 | V |
| Charge pump load current IOUT | 0 | 100 | mA |
| Junction temperature TJ | −30 | 125 | °C |
| Ambient temperature TA | −30 | 85 | °C |

Thermal, NJA (WQFN) (p. 6, §6.4): RθJA 38.4 °C/W, RθJC(top) 27.3 °C/W, RθJB 15.4 °C/W, ψJB 15.4 °C/W, RθJC(bot) 3.1 °C/W.

## Power by mode

SNVS441I, p. 6, §6.5; 2.7 V ≤ VDD ≤ 5.5 V, CIN = COUT = 1 µF, CFLY = 0.47 µF, TJ = 25 °C unless noted. Only typical values are given unless stated.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Standby | EN = 0, CHIP_EN = 0 | 0.2 | — | µA |
| Standby | EN = 0, CHIP_EN = 0, −30 °C < TA < 85 °C | — | 2 | µA |
| Standby, EN high | EN = 1, CHIP_EN = 0, external 32 kHz clock not running | 1 | — | µA |
| Standby, EN high | EN = 1, CHIP_EN = 0, external 32 kHz clock running | 1.4 | — | µA |
| Normal | charge pump and LED drivers disabled | 0.25 | — | mA |
| Normal | charge pump 1×, no load, LED drivers disabled | 0.7 | — | mA |
| Normal | charge pump 1.5×, no load, LED drivers disabled | 1.5 | — | mA |
| Normal | charge pump 1×, no load, LED drivers enabled | 1.2 | — | mA |
| Power save | external 32 kHz clock running | 10 | — | µA |
| Power save | internal oscillator running | 0.25 | — | mA |

Charge pump ground current (p. 7, §6.6): 1.2 mA at 1.5×, 0.5 mA at 1×.

Power save (p. 15, §7.3.3): enabled by PWRSAVE_EN (register 08H). With the internal clock only the charge pump and LED drivers turn off, because the program engines stay clocked; with an external clock almost all analog blocks turn off.

## Pinout and package

LP5521YQ pin functions (SNVS441I, p. 4; pinout p. 3, NJA package):

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | CFLY2P | A | Flying capacitor 2, positive |
| 2 | CFLY1P | A | Flying capacitor 1, positive |
| 3 | VDD | P | Supply |
| 4 | GND | G | Ground |
| 5 | CLK_32K | I | 32 kHz clock input; tie to GND if unused (p. 17, §7.3.5.5) |
| 6 | INT | OD/O | Interrupt output (active low, open drain) or GPO |
| 7 | TRIG | I/OD | Trigger input/output (open drain); tie to GND if unused (p. 17, §7.3.5.3) |
| 8–12 | N/C | — | No connection |
| 13 | SDA | I/OD | I2C data |
| 14 | EN | I | Chip enable; also the I/O reference for SDA, SCL, TRIG, CLK_32K |
| 15 | SCL | I | I2C clock |
| 16 | GPO | O | General-purpose output, VDD level |
| 17 | R | A | Current source output (charge pump or VDD, see R_TO_BATT) |
| 18 | G | A | Current source output (charge pump) |
| 19 | B | A | Current source output (charge pump) |
| 20 | ADDR_SEL0 | I | I2C address select, VDD referenced |
| 21 | ADDR_SEL1 | I | I2C address select, VDD referenced |
| 22 | VOUT | A | Charge pump output |
| 23 | CFLY2N | A | Flying capacitor 2, negative |
| 24 | CFLY1N | A | Flying capacitor 1, negative |
| 25 | Exposed pad | — | Thermal pad, soldered to the board (p. 48, note 3) |

Package NJA0024A (drawing 4215212/A 04/2017, p. 48): body 4.0 ± 0.1 × 5.0 ± 0.1 mm, 0.8 mm max height, pitch 0.5 mm, leads 0.4 ± 0.1 × 0.25 ± 0.05 mm as drawn, exposed pad 2.4 ± 0.1 × 3.4 ± 0.1 mm. Orderable addendum (p. 42): LP5521YQX/NOPB, WQFN (NJA) 24, 4500 per large reel, SnAgCu finish, MSL Level-1-260C-UNLIM, −30 to 85 °C, marking L5521YQ.

## Recommended footprint

SNVS441I, p. 49 (example board layout, 4215212/A) and p. 50 (stencil):

- 24 pads (0.4) × (0.25) mm at 0.5 mm pitch; pad-row extents (4.4) mm and (3.4) mm as drawn.
- Thermal pad (2.4) × (3.4) mm, with optional (0.2) mm vias; vias under paste filled, plugged or tented (p. 49, note 6).
- Non-solder-mask-defined pads preferred, 0.07 mm mask clearance (p. 49).
- Stencil 0.1 mm: six (1.06) × (0.98) mm apertures on the thermal pad, 76 % paste coverage (p. 50).
- The text layer of the drawing does not resolve every dimension unambiguously; the KiCad footprint must be checked against the PDF (**UNVERIFIED** transcription of the exact pad origins).

## Application circuit and required passives

Typical application with charge pump (SNVS441I, p. 36, Figure 26; p. 37, §8.2.1.2.1):

| Ref | Value | Note |
|---|---|---|
| CIN | 1 µF | X5R/X7R, ≥ 6.3 V; DC-bias loss better than −50 % at 5 V |
| COUT | 1 µF | X5R/X7R, 10 V recommended for DC bias |
| CFLY1, CFLY2 | 470 nF | X5R/X7R, ≥ 6.3 V |

- TI example parts: C1005X5R1A105K or ECJ0EB1A105M (1 µF, 0402, 10 V); C1005X5R1A474K or ECJ0EB0J474K (470 nF, 0402) (p. 37, Table 36).
- Place the capacitors as close to the device as possible (p. 40, §10.1; Figure 31).
- Without the charge pump the flying capacitors may be omitted and the pump must be set to 1× (p. 38, §8.2.2). Not applicable to the T1: green and blue need the pump.
- The VDD supply must not dip below 2.7 V on load transients (p. 40, §9).
- INT and TRIG are open drain and need pull-ups when used (p. 16–17).

## Interfaces and timing

- **I2C:** up to 400 kHz (SNVS441I, p. 8, §6.9). 7-bit address from ADDR_SEL[1:0]: 00 → 0x32 (8-bit 64H/65H), 01 → 0x33, 10 → 0x34, 11 → 0x35 (p. 20, Table 9).
- **Logic levels:** SCL, SDA, TRIG and CLK_32K follow the EN pin voltage: VIL 0.2 × V(EN), VIH 0.8 × V(EN), V(EN) from 1.65 V to VDD (p. 8, §6.8; p. 16, §7.3.5.1). EN itself: VIL 0.5 V, VIH 1.2 V (p. 7). ADDR_SEL0/1 thresholds are 0.2 / 0.8 × VDD (p. 8). SDA/TRIG/INT VOL 0.5 V max at 3 mA (p. 8).
- **Start-up:** 1 ms typ after EN rises before I2C access; 500 µs typ after CHIP_EN = 1 (p. 7, note 1; p. 18, §7.4.1). EN low resets CHIP_EN (p. 18). POR below VDD 1.5 V typ (0.8 V min) (p. 18).
- **Charge pump** (p. 7, §6.6): ROUT 3.5 Ω typ at 1.5×, 1 Ω at 1×; fSW 1.25 MHz; regulated output 4.55 V typ at VDD = 3.6 V, no load, 1.5×; turn-on to 1.5× in 100 µs typ at 60 mA. Out of regulation, VOUT = 1.5 × VIN − IOUT × ROUT (p. 12, §7.3.1.1). CP_MODE (08H bits 4:3): off, forced 1×, forced 1.5×, automatic (p. 12, Table 1). In automatic mode the pump drops to 1× after 50 ms with the LEDs inactive (p. 13).
- **R_TO_BATT** (08H bit 2): connects the R current source to VDD instead of the pump; its saturation monitor is then disabled (p. 13). TI lists "RGB LED with low VF red" as R to battery with automatic pump mode (p. 13, Table 2).
- **LED drivers** (p. 7, §6.7): IMAX 25.5 mA; accuracy ±4 % at 17.5 mA (±5 % over −30 to 85 °C); matching 1 % typ, 2 % max; VSAT 50 mV typ, 100 mV max at 17.5 mA (current down 10 % from its value at VOUT − 1 V); leakage 0.1 µA typ, 1 µA max over temperature. Default current 17.5 mA (p. 14, Table 3).
- **PWM:** 256 Hz (32 kHz clock) or 558 Hz (PWM_HF = 1, internal oscillator); linear or logarithmic scale (LOG_EN) (p. 7; p. 14).
- **Clock:** internal oscillator ±4 % (±7 % over temperature) (p. 6); CLK_32K tied to GND when no external clock (p. 15).

## Linux driver

Mainline `leds-lp5521` (`LEDS_LP55XX_COMMON`, `LEDS_LP5521`), devicetree compatible `national,lp5521`; Debian trixie-backports 7.2 does not set these options, so it ships as DKMS (BOM v1 line 105 and §3; opendap-os ADR 0007). No local Linux tree was opened for this sheet: the binding properties (clock mode, per-channel current and maximum current, multicolor grouping) are **UNVERIFIED**.

## Simulation models

None. The datasheet points to the LP5521TM evaluation kit, *LP5521 Programming Considerations* and *LP5521 Power Efficiency Considerations* (SNVA185) (SNVS441I, p. 15, p. 41). No manifest entry beyond the datasheet.

## Design notes for the T1

- **Charge pump headroom (BOM v1 line 105, change 7):** the BOM computes VOUT ≥ 1.5 × 3.0 V − 3 × 20 mA × 3.5 Ω = 4.29 V at VSYS 3.0 V, then subtracts VSAT 0.1 V max and the LED's worst VF 3.8 V + 0.1 V tolerance ([19-337/R6GHBHC-A01/2T](../Everlight/19-337-R6GHBHC-A01-2T.md)), leaving 0.29 V. The arithmetic is correct, with these caveats from SNVS441I:
  - ROUT 3.5 Ω is a typical value with no maximum (p. 7), so the 4.29 V figure is typical, not a guaranteed floor.
  - VSAT 100 mV max is specified at 17.5 mA (p. 7), not 20 mA; the 20 mA value is **UNVERIFIED**.
  - With R_TO_BATT = 1, as the BOM sets, the pump only carries G and B (2 × 20 mA), so the same model gives 4.36 V; using 3 × 20 mA is conservative.
  - The red channel on VDD then needs VSYS ≥ 2.5 V (VF 2.4 V + 0.1 V) + VSAT: at VSYS 3.0 V the margin is about 0.4 V.
  - The 4.5 V regulation target (p. 12) also caps VOUT: at VDD above about 3.0 V the pump regulates instead of following 1.5 × VDD.
- **I2C on 1.8 V:** EN on vcca1v8_pmu sets the I2C thresholds to 0.36 / 1.44 V, compatible with I2C2 at 1.8 V (BOM v1 §4.2, PMUIO2 row). The EN VIH of 1.2 V is met. ADDR_SEL0/1 to GND gives 0x32, the BOM address.
- **Standby cost:** with EN tied high and CHIP_EN = 0, 1 µA typ (p. 6). Power save with the internal clock costs 0.25 mA typ; with CLK_32K tied to GND the internal clock is the only option, so a lit LED or a running program keeps at least that draw (p. 6, p. 15).
- **Channel cap:** the BOM limits each channel to 20 mA in the devicetree, 80 % of the LED's 25 mA IF (line 79). The binding property name is **UNVERIFIED** (the BOM writes `led-max-microamp`; see Linux driver).
- Unused pins: CLK_32K and TRIG to GND (p. 15, p. 17); INT needs a pull-up if routed to the SoC.
- Alternative named in the BOM: LP5521TMX/NOPB (DSBGA-20, same die, 3000 per reel, p. 42).

## Sources

- TI, LP5521 datasheet, SNVS441I (November 2016): <https://www.ti.com/lit/ds/symlink/lp5521.pdf>
- OpenDAP board BOM v1.2, lines 79, 105, §3, §4.2, Changes in v1.2 item 7; power tree v0, rail table and gating map (`public/board/docs/specs/`).
- File name: the MPN's slash is written as a hyphen.
