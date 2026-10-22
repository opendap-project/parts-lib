# TPD8S300ARUKR

- **Manufacturer:** Texas Instruments
- **Function:** USB Type-C port protector: 4-channel short-to-VBUS overvoltage protection (CC1, CC2, SBU1, SBU2) and 8-channel IEC 61000-4-2 ESD protection
- **BOM v1 lines:** 63 (main USB-C CC and SBU protection)
- **Package:** WQFN-20 (RUK), 3.0 × 3.0 mm, 0.4 mm pitch, exposed thermal pad
- **Datasheet:** TPD8S300A, SLVSEL9 (June 2018, initial release), sha256 `2c1d5b68b194…` in `manifest.toml`
- **Status:** Partly UNVERIFIED

## Summary

The TPD8S300A places high-voltage FETs in series with the USB Type-C CC and SBU lines and opens them when the connector side exceeds the OVP threshold, so a 20 V VBUS shorted onto CC or SBU does not reach the system side (24 V DC tolerant). It also integrates IEC 61000-4-2 clamps on CC, SBU and four USB 2.0 pins, and switchable dead-battery Rd pull-downs on CC (SLVSEL9 §1, §3, p. 1). In the T1 it protects the CC and SBU pins of the main USB-C receptacle in front of the CC/PD controller (BOM v1 line 63); its integrated dead-battery Rd lets a source supply VBUS when the T1 battery is empty.

## Absolute maximum ratings

| Parameter | Pins | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Input voltage | VPWR | −0.3 | 4 | V | SLVSEL9 p. 5, §7.1 |
| Input voltage | RPD_G1, RPD_G2 | −0.3 | 24 | V | p. 5, §7.1 |
| Output voltage | FLT | −0.3 | 6 | V | p. 5, §7.1 |
| Output voltage | VBIAS | −0.3 | 24 | V | p. 5, §7.1 |
| I/O voltage | D1, D2 | −0.3 | 6 | V | p. 5, §7.1 |
| I/O voltage | CC1, CC2, SBU1, SBU2 (system side) | −0.3 | 6 | V | p. 5, §7.1 |
| I/O voltage | C_CC1, C_CC2, C_SBU1, C_SBU2 (connector side) | −0.3 | 24 | V | p. 5, §7.1 |
| Operating free-air temperature, TA | — | −40 | 85 | °C | p. 5, §7.1 |
| Storage temperature, Tstg | — | −65 | 150 | °C | p. 5, §7.1 |
| ESD, HBM | ANSI/ESDA/JEDEC JS-001 | — | ±2000 | V | p. 5, §7.2 |
| ESD, CDM | JESD22-C101 | — | ±500 | V | p. 5, §7.2 |
| ESD, IEC 61000-4-2 contact | C_CC1, C_CC2, D1, D2 | — | ±8000 | V | p. 5, §7.3 |
| ESD, IEC 61000-4-2 air gap | C_CC1, C_CC2, D1, D2 | — | ±15000 | V | p. 5, §7.3 |
| ESD, IEC 61000-4-2 contact | C_SBU1, C_SBU2 | — | ±6000 | V | p. 5, §7.3 |
| ESD, IEC 61000-4-2 air gap | C_SBU1, C_SBU2 | — | ±15000 | V | p. 5, §7.3 |

The IEC figures were measured on the TPD6S300 EVM connected to the TPS65982 EVM (§7.3 note 1).

## Recommended operating conditions

| Parameter | Min | Nom | Max | Unit | Reference |
|---|---|---|---|---|---|
| VPWR | 2.7 | 3.3 | 3.6 | V | p. 5, §7.4 |
| RPD_G1, RPD_G2 | 0 | — | 5.5 | V | p. 5 |
| FLT pull-up rail | 2.7 | — | 5.5 | V | p. 5 |
| D1, D2 | −0.3 | — | 5.5 | V | p. 5 |
| CC1, CC2, C_CC1, C_CC2 | 0 | — | 5.5 | V | p. 5 |
| SBU1, SBU2, C_SBU1, C_SBU2 | 0 | — | 4.3 | V | p. 5 |
| VCONN current through CC, VCCx − VC_CCx ≤ 250 mV or TJ ≤ 105 °C | — | — | 600 | mA | p. 5 |
| VCONN current through CC, TJ ≤ 85 °C | — | — | 1.25 | A | p. 5 |
| FLT pull-up resistance | 1.7 | — | 300 | kΩ | p. 6 |
| VBIAS capacitance (≥ 35 V rated, 50 V recommended) | — | 0.1 | — | µF | p. 6, note 2 |
| VPWR capacitance | 0.3 | 1 | — | µF | p. 6 |

### Electrical characteristics

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| CC OVP FET on-resistance | CCx = 5.5 V, TJ ≤ 85 °C | — | 278 | 392 | mΩ | p. 6, §7.6 |
| CC equivalent on-capacitance | powered, 0–1.2 V, 400 kHz | 60 | 74 | 120 | pF | p. 6 |
| Dead-battery pull-down RD (unpowered) | V_C_CCx = 2.6 V | 4.1 | 5.1 | 6.1 | kΩ | p. 6 |
| Dead-battery FET threshold VTH_DB | I_CC = 80 µA | 0.5 | 0.9 | 1.2 | V | p. 6 |
| CC OVP threshold | rising | 5.75 | 6 | 6.2 | V | p. 6 |
| CC on bandwidth (−3 dB) | 50 Ω | — | 100 | — | MHz | p. 6 |
| Short-to-VBUS tolerance, CC and SBU | hot plug, 1 m cable | — | — | 24 | V | p. 7 |
| System-side clamp during short-to-VBUS, CC and SBU | C_xx = 24 V, VPWR = 3.3 V | — | 8 | — | V | p. 7 |
| SBU OVP FET on-resistance | SBUx = 3.6 V, −40 to 85 °C | — | 4 | 6.5 | Ω | p. 7 |
| SBU equivalent on-capacitance | 0.3–3.6 V | — | 6 | — | pF | p. 7 |
| SBU OVP threshold | rising | 4.35 | 4.5 | 4.7 | V | p. 7 |
| SBU on bandwidth (−3 dB) | 50 Ω | — | 1000 | — | MHz | p. 7 |
| VPWR UVLO, rising | — | 2.1 | 2.3 | 2.5 | V | p. 7 |
| VPWR supply current | VPWR = 3.3 V typ / 3.6 V max | — | 90 | 120 | µA | p. 7 |
| Dx leakage | V_Dx = 3.6 V | — | — | 1 | µA | p. 8 |
| FLT low-level output | IOL = 3 mA | — | — | 0.4 | V | p. 8 |
| Thermal shutdown, rising / falling | — | 150 / 130 | 175 / 140 | — | °C | p. 8 |
| Dx VRWM (Dx to GND) | IDX ≤ 1 µA | — | — | 5.5 | V | p. 8 |
| Dx breakdown (Dx to GND) | IBR = 1 mA | 7 | — | — | V | p. 8 |
| Dx capacitance | f = 1 MHz, VIO = 2.5 V | — | 1.7 | — | pF | p. 8 |
| Dx dynamic resistance | — | — | 0.4 | — | Ω | p. 8 |

Thermal (RUK): RθJA 45.2 °C/W, RθJB 17.1 °C/W, RθJC(bot) 3.7 °C/W (p. 6, §7.5).

## Power by mode

Device mode table (Table 1, p. 20) and supply current (§7.6):

| Mode | VPWR | CC / SBU FETs | FLT | Supply current |
|---|---|---|---|---|
| Unpowered, RPD_Gx grounded | < UVLO | off | Hi-Z | 0 |
| Unpowered, dead-battery support (RPD_Gx shorted to C_CCx) | < UVLO | off; RD present on C_CCx | Hi-Z | 0 |
| Powered, normal | > UVLO | on; RD forced off | Hi-Z | 90 µA typ, 120 µA max (p. 7) |
| CC or SBU overvoltage | > UVLO | off | low (asserted) | **UNVERIFIED** (not specified separately) |
| Thermal shutdown | > UVLO | off | low (asserted) | **UNVERIFIED** |

The D1–D4 clamps are always present, powered or not (§8.4, p. 20).

## Pinout and package

WQFN-20 (RUK), top view (Pin Functions, pp. 3–4):

| Pin | Name | Type | Description |
|---|---|---|---|
| 1 | C_SBU1 | I/O | Connector side of SBU1 OVP FET (or a USB 2.0 connector pin) |
| 2 | C_SBU2 | I/O | Connector side of SBU2 OVP FET (or a USB 2.0 connector pin) |
| 3 | VBIAS | Power | ESD support capacitor, 0.1 µF to GND |
| 4 | C_CC1 | I/O | Connector side of CC1 OVP FET |
| 5 | C_CC2 | I/O | Connector side of CC2 OVP FET |
| 6 | RPD_G2 | I/O | Short to C_CC2 for dead-battery RD, else to GND |
| 7 | RPD_G1 | I/O | Short to C_CC1 for dead-battery RD, else to GND |
| 8 | GND | GND | Ground |
| 9 | FLT | O | Open-drain fault output |
| 10 | VPWR | Power | 2.7–3.6 V supply |
| 11 | CC2 | I/O | System side of CC2 OVP FET, to the CC/PD controller |
| 12 | CC1 | I/O | System side of CC1 OVP FET, to the CC/PD controller |
| 13 | GND | GND | Ground |
| 14 | SBU2 | I/O | System side of SBU2 OVP FET |
| 15 | SBU1 | I/O | System side of SBU1 OVP FET |
| 16 | D4 | I/O | USB 2.0 IEC ESD clamp |
| 17 | D3 | I/O | USB 2.0 IEC ESD clamp |
| 18 | GND | GND | Ground |
| 19 | D2 | I/O | USB 2.0 IEC ESD clamp |
| 20 | D1 | I/O | USB 2.0 IEC ESD clamp |
| 21 | Thermal pad | GND | Internally connected to GND; connect to the PCB GND plane |

Outline RUK0020B (drawing 4222676/A, PDF p. 33): body 2.9–3.1 × 2.9–3.1 mm, 0.8 mm maximum height, 0.4 mm pitch, exposed pad 1.7 ± 0.05 mm square, terminals 0.15–0.25 mm wide and 0.3–0.5 mm long. MSL and finish: NiPdAu, reel of 3000 (package option addendum, PDF p. 29).

## Recommended footprint

RUK0020B example board layout (PDF p. 34, drawing 4222676/A, scale 20:1):

- 20 pads 0.6 × 0.2 mm (reference) at 0.4 mm pitch; pad row centre-to-centre 2.8 mm (reference) in both axes.
- Thermal pad 1.7 × 1.7 mm (reference) with optional Ø 0.2 mm vias (filled, plugged or tented if under paste, note 5).
- Non-solder-mask-defined pads preferred, 0.05 mm maximum mask clearance.
- Stencil: example on PDF p. 35 (0.1 mm stencil).

## Application circuit and required passives

| Passive | Value | Placement | Reference |
|---|---|---|---|
| VBIAS capacitor | 0.1 µF, ≥ 35 V rated; 50 V X7R recommended (e.g. GRM188R71H104KA93D, 0603) | As close as possible to VBIAS, solid ground | p. 6 note 2; §9.2.2.1, Table 3, p. 23; §11.1 |
| VPWR decoupling | 1 µF (0.3 µF effective minimum) | As close as possible to VPWR | p. 6; §10, p. 26 |
| FLT pull-up | 1.7–300 kΩ to a 2.7–5.5 V rail | — | p. 5–6 |
| CC capacitor (system side) | Sized so the total CC capacitance stays within the USB PD cReceiver window of 200–600 pF (the TPD8S300A contributes 60–120 pF) | CC line | §9.2.2.3, Tables 4 and 5, p. 24 |

- Dead-battery support: short RPD_G1 to C_CC1 and RPD_G2 to C_CC2 (§9.2.2.2, p. 23). If not needed, ground RPD_Gx; unused Dx pins must also be grounded (§9.2.2.6, p. 25).
- Any extra ESD diode on CC or SBU must have a reverse stand-off above 21.5 V (24 V recommended) and must not be a deep-snapback type unless its trigger voltage is above 42 V (§9.2.2.4, p. 24).

## Interfaces and timing

| Parameter | Typ | Max | Unit | Reference |
|---|---|---|---|---|
| VPWR UVLO crossing to CC and SBU FETs on, tON_FET | 1.3 | 3.5 | ms | p. 8, §7.7 |
| VPWR UVLO crossing to FETs on and dead-battery RD off, tON_FET_DB | 5.7 | 9.5 | ms | p. 8 |
| OVP response, CC | 70 | — | ns | p. 9 |
| OVP response, SBU | 80 | — | ns | p. 9 |
| OVP to FLT assertion | 20 | — | µs | p. 9 |
| CC FET turn-on after OVP to FLT deassertion | 4.1 | — | ms | p. 9 |

FLT is an open-drain output asserted on CC overvoltage, SBU overvoltage or thermal shutdown (Table 1, p. 20). The datasheet recommends that the PD controller force a detach when FLT asserts (§9.2.2.5, p. 25).

## Linux driver

None (no software interface). The FLT output can be wired to a GPIO and reported through a generic GPIO or interrupt binding; no T1 decision on this exists yet.

## Simulation models

None listed in `manifest.toml`. Whether TI publishes an IBIS or SPICE model for this device is **UNVERIFIED**.

## Design notes for the T1

- In the dead-battery case the FETs are off while VPWR is below UVLO, which isolates the CC/PD controller's own Rd; the TPD8S300A's internal RD must then be connected (RPD_Gx shorted to C_CCx) so a source applies VBUS (§9.2.2.2, p. 23). The datasheet also asks that the PD controller's own dead-battery Rd stay present on the system side, and that the TPD8S300A share the supply that the PD controller uses during dead-battery boot (§10, p. 26). How this maps onto the T1 CC controller (FUSB302B, BOM line 41) and its supply rail is **UNVERIFIED**.
- The integrated CC capacitance (60–120 pF) counts toward the 200–600 pF USB PD cReceiver budget together with the CC controller and any external capacitor (§9.2.2.3).
- The D1–D4 clamps (1.7 pF typ) can protect the USB 2.0 D+/D− pins of the receptacle. BOM v1 line 62 also places a TPD4E05U06 (0.5 pF) on D+/D−; whether both are fitted on the same pins is a schematic decision, and unused Dx pins must then be grounded (§9.2.2.6).
- SBU pass range is 0–4.3 V (p. 5). Whether the T1 receptacle (GCT USB4105-GF-A) routes SBU at all is **UNVERIFIED** here; if it does not, the C_SBUx/SBUx handling for unused SBU pins is not stated in the datasheet (**UNVERIFIED**).
- Operating ambient is limited to −40 to 85 °C (p. 5).
- Layout: place close to the connector, VBIAS and VPWR capacitors close to their pins on solid ground, straight USB 2.0 and SBU routing, and do not via directly into the Dx pins from another layer (§11.1, p. 27).
- LCSC stock is low (BOM v1 line 63); TPD4S311A is the listed alternative.

## Sources

- TI, *TPD8S300A USB Type-C Port Protector: Short-to-VBUS Overvoltage and IEC ESD Protection*, SLVSEL9, June 2018, <https://www.ti.com/lit/ds/symlink/tpd8s300a.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 41, 61, 62, 63
