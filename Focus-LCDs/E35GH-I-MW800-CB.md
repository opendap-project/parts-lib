# E35GH-I-MW800-CB

- **Manufacturer:** Focus LCDs (Focus Display Solutions)
- **Function:** 3.5-inch 320 × 480 IPS TFT display module, 1-lane MIPI DSI, with capacitive touch panel (GT911) and white LED backlight
- **BOM v1 lines:** 81 (display), 82 (touch controller, see [`Goodix/GT911.md`](../Goodix/GT911.md)), 84 and 85 (mating connectors)
- **Package:** Module, 54.46 × 82.94 × 5.50 mm, 46.85 g; 20-pin TFT FPC tail and 6-pin CTP FPC tail
- **Datasheet:** Focus LCDs product specification E35GH-I-MW800-CB, Rev 1.0 (2025-03-04, drawing revision block p. 3), 15 pages, sha256 `2912a2ebd90e…` in `manifest.toml`
- **Status:** Partly UNVERIFIED

## Summary

The E35GH-I-MW800-CB is a transmissive, normally black 3.5-inch IPS TFT module, 320(RGB) × 480 pixels, rated 800 nits on the overview page. It has a chip-on-glass ILI9488 controller on a 1-lane MIPI DSI interface and a GT911 capacitive touch panel on I²C (spec pp. 1–2, 4). In the T1 it is the display of the default touch faceplate (BOM v1 line 81, decided in touch-faceplate ADR 0001). The faceplate flex carries it, through Hirose FH12 connectors (lines 84, 85).

## Absolute maximum ratings

Ta = 25 °C, VSS = 0 V (spec p. 10, §5.1).

| Parameter | Symbol | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Digital supply voltage | VDD (VCI) | −0.3 | 3.3 | V | p. 10, §5.1 |
| Logic supply voltage | IOVCC | −0.3 | 3.3 | V | p. 10, §5.1 |
| Operating temperature | TOP | −20 | +70 | °C | p. 10, §5.1 |
| Storage temperature | TST | −30 | +80 | °C | p. 10, §5.1 |

The §5.1 table labels the panel supply "VDD", while the pin table and §5.2 call it VCI. This sheet assumes they are the same supply (**UNVERIFIED**).

## Recommended operating conditions

TFT DC characteristics (spec p. 10, §5.2):

| Parameter | Symbol | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| Digital supply voltage | VCI | 2.5 | 2.8 | 3.3 | V |
| Logic supply voltage | IOVCC | 1.65 | 1.8 | 3.3 | V |
| Input high voltage | VIH | 0.7 × IOVCC | — | IOVCC | V |
| Input low voltage | VIL | −0.3 | — | 0.3 × IOVCC | V |
| Output high voltage | VOH | 0.8 × IOVCC | — | IOVCC | V |
| Output low voltage | VOL | 0.0 | — | 0.2 × IOVCC | V |

Backlight, edge-lit, 10 white LED chips (spec p. 11, §5.3):

| Parameter | Symbol | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| Forward current | IF | — | 60 | — | mA |
| Forward voltage | VF | 14.0 | 15.0 | 16.5 | V |
| Module luminance | LV | 680 | — | — | cd/m² |
| LED lifetime (to 50 % brightness, Ta = 25 °C, IF = 60 mA) | Hr | 50,000 | — | — | h |
| Uniformity (9 points) | Avg | 75 | 80 | — | % |

The outline drawing note 8 gives "10 LED white, VF = 15.6 V, IF = 60 mA" (p. 3), against 15.0 V typical in the §5.3 table. The spec recommends constant-current drive and notes that lifetime falls above 60 mA (p. 11, note 2).

Touch panel (CTP) working conditions (spec p. 13, §7.1): operating temperature −20 to +85 °C; AVDD (printed "ACDD28") typical 2.8 V, maximum 3.3 V; VDDIO typical 1.8 V, maximum 3.3 V. Minimum values are not given.

Environment: operating −20 to +70 °C, storage −30 to +80 °C (p. 2).

## Power by mode

TFT panel (VCI, IOVCC) current is not given in the specification (**UNVERIFIED**).

Backlight: about 0.9 W at IF = 60 mA and VF = 15.0 V typical. This is calculated from the §5.3 table, not stated in the spec.

Touch controller, at 25 °C, AVDD = 2.8 V, VDDIO = 1.8 V or VDDIO = AVDD (spec p. 13, §7.2):

| Mode | Min | Typ | Max | Unit |
|---|---|---|---|---|
| Normal | — | 8 | 14.5 | mA |
| Green | — | 3.3 | — | mA |
| Doze | — | 0.78 | — | mA |
| Sleep | 70 | — | 120 | µA |

## Pinout and package

TFT FPC tail, 20 pins (spec p. 5, §3.1):

| Pin | Symbol | Description | I/O |
|---|---|---|---|
| 1 | NC | No connection | — |
| 2 | LEDK | Backlight cathode | P |
| 3 | NC | No connection | — |
| 4 | LEDA | Backlight anode | P |
| 5 | NC | No connection | — |
| 6 | VCI | Power supply for LCD | P |
| 7 | IOVCC | Power supply for I/O | P |
| 8 | NC | No connection | — |
| 9 | RESET | Reset input | I |
| 10 | GND | Ground | P |
| 11–12 | NC | No connection | — |
| 13 | GND | Ground | P |
| 14 | MIPI_CLP | DSI clock + | I |
| 15 | MIPI_CLN | DSI clock − | I |
| 16 | GND | Ground | P |
| 17 | MIPI_D0P | DSI data lane 0 + | I/O |
| 18 | MIPI_D0N | DSI data lane 0 − | I/O |
| 19–20 | GND | Ground | P |

CTP FPC tail, 6 pins (spec p. 6, §3.2):

| Pin | Symbol | Description | I/O |
|---|---|---|---|
| 1 | RST | Reset input | I |
| 2 | INT | Interrupt request | I |
| 3 | SDA | I²C data | I/O |
| 4 | SCL | I²C clock | I |
| 5 | GND | Ground | P |
| 6 | VDD | CTP supply | P |

The spec marks INT as "I" (p. 6). On the GT911 it is an output during operation and an address-strap input during reset (see the GT911 sheet).

Mechanical (spec p. 2 and outline drawing p. 3): module 54.46 (H) × 82.94 (V) × 5.50 (D) mm typical; active area 48.96 × 73.44 mm; CTP view area 49.56 × 74.04 mm; general tolerance ±0.3 mm. Drawing p. 3: cover glass 0.55 mm (etched AG), sensor 0.55 mm, total thickness 5.50 mm. Both tails exit the bottom edge and bend behind the module ("Bend and Ship"). Exact tail lengths, widths and the contact pitch must be read from the drawing on p. 3. That drawing is not to scale, and the dimensions printed on it are hard to read at the available resolution (**UNVERIFIED**; request the DXF/PDF master drawing from Focus LCDs).

## Recommended footprint

Not applicable (module). Mating connectors:

- TFT tail: the spec recommends "FH12S-20S-0.5SH(55)" (p. 5). "FH12S" is taken as a typo for the Hirose FH12-20S-0.5SH(55) carried in BOM v1 line 84 (**UNVERIFIED** with Focus LCDs).
- CTP tail: the spec does not name a connector. BOM v1 line 85 states that the Focus spec names FH12-6S-0.5SH(55) for the CTP tail; that claim is not supported by Rev 1.0 (pp. 5–6). Pitch and contact side of the CTP tail must be confirmed from the drawing or with Focus LCDs before the faceplate layout.

## Application circuit and required passives

The specification gives no application circuit. Needed by inference from the pin table (decoupling values **UNVERIFIED**):

- VCI 2.5–3.3 V and IOVCC 1.65–3.3 V supplies, each decoupled at the connector.
- Constant-current backlight driver able to exceed 16.5 V at 60 mA (BOM line 51, TPS61169, on the main board; LEDA/LEDK run through the faceplate connector).
- RESET driven from a GPIO at IOVCC level (BOM line 96: SN74AXC1T45 translators on the faceplate, from the 3.3 V bank to IOVCC 1.8 V).
- GT911 tail: I²C pull-ups, RST and INT GPIOs (see the GT911 sheet).

## Interfaces and timing

- **Display:** 1-lane MIPI DSI (clock + D0), ILI9488 controller (pp. 1–2, 4). For the high-speed data–clock timing, turnaround, clock-lane LP switching and reset timing, the spec refers to the ILI9488 datasheet pp. 305, 330, 331 and 334 (spec p. 12, §6.1–6.5, <https://focuslcds.com/wp-content/uploads/Drivers/ILI9488.pdf>). That datasheet was not opened for this sheet (**UNVERIFIED**).
- **Touch:** I²C. The spec refers to the GT911 datasheet for I²C, power-on, reset and address timing (pp. 13–14, §7.4–7.8). Those values are transcribed in [`Goodix/GT911.md`](../Goodix/GT911.md).
- **Touch I/O levels** (p. 13, §7.2): VIL max 0.25 × VDD, VIH min 0.75 × VDD (max VDD + 0.3), VOL max 0.15 × VDD, VOH min 0.85 × VDD. CTP oscillator 59–61 MHz; I/O rise and fall time 0.5 ns maximum (p. 13, §7.3).
- **Optical** (p. 7, §4.1): contrast ratio 700 typical; response time 30 ms typical; viewing angle 80° in all four directions (CR ≥ 10); white chromaticity x 0.30, y 0.31 typical; colour gamut 50 % typical.

## Linux driver

- BOM v1 line 81: *DKMS (mainline compatible, off in Debian)*.
- The spec names the controller as ILI9488 with a 1-lane DSI interface. A mainline DRM panel driver for the ILI9488 over MIPI DSI could not be confirmed in this pass. The ILI9488 driver support known from mainline is for SPI/DBI variants, not DSI, and is also **UNVERIFIED**. The BOM's "mainline compatible" for this module is therefore **UNVERIFIED**. If no mainline DSI driver exists, a panel driver (for example a `panel-ilitek-ili9488` DSI driver, or a generic DSI panel with an init sequence) has to be written or carried as DKMS.
- Touch: mainline `goodix` touchscreen driver, compatible `goodix,gt911` (see the GT911 sheet).
- Backlight: `pwm-backlight` through the main-board driver (BOM line 51), not through this module.

## Simulation models

None listed in `manifest.toml`. No 3D model is provided in the specification. A STEP or DXF from Focus LCDs is **UNVERIFIED**.

## Design notes for the T1

- **Single DSI lane.** The module uses clock + D0 only (p. 5). BOM line 71 carries 4 DSI lanes to the faceplate connector for other faceplates; this faceplate uses one.
- **VCI margin.** The VCI absolute maximum (3.3 V, p. 10) equals the recommended maximum. A nominal 3.3 V rail with tolerance can exceed it. Run VCI at 2.8 V typical, or make sure FP_VCI never exceeds 3.3 V, including transients. BOM line 71 already routes a separate FP_VCI.
- **IOVCC at 1.8 V.** Matches the faceplate-side translators (line 96). VIH = 0.7 × IOVCC on RESET.
- **Backlight.** VF up to 16.5 V at 60 mA (p. 11). The boost driver (line 51) and the faceplate connector contacts (line 71) must be rated above that. BOM line 71 lists the 16.5 V rating of the FH35C contacts as **UNVERIFIED**.
- **Touch supply.** CTP VDD maximum 3.3 V (p. 13). BOM line 82 feeds it from FP_3V3, at the limit. Check the GT911 datasheet range in the GT911 sheet.
- **Handling.** Do not connect or disconnect the module with power on, and follow the power on/off sequence (p. 15, §9.1 items 13–14). The FPC circuitry is on the bottom side and must not be stressed (p. 15, §9.2 item 5). For the faceplate this means the panel is never hot-plugged; faceplate detect must gate FP power first.

## Sources

- Focus LCDs, *TFT Display Module E35GH-I-MW800-CB*, specification Rev 1.0, 2025-03-04, <https://focuslcds.com/wp-content/uploads/2025/09/E35GH-I-MW800-CB_Spec.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 51, 71, 81, 82, 84, 85, 96
