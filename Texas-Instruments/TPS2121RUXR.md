# TPS2121RUXR

- **Manufacturer:** Texas Instruments
- **Function:** 2.8–22 V dual-input, single-output priority power multiplexer with seamless switchover, 4.5 A
- **BOM v1 lines:** 45 (Power), USB-C IN1 priority and powerbank HAT IN2 into the charger, status Proposed
- **Package:** VQFN-HR 12-pin, 2.0 mm × 2.5 mm (RUX, drawing RUX0012A)
- **Datasheet:** TPS212x 2.8-V to 22-V Priority Power MUX with Seamless Switchover, SLVSEA3F (August 2018, revised August 2020), <https://www.ti.com/lit/ds/symlink/tps2121.pdf>
- **Status:** Partly UNVERIFIED

## Summary

The TPS2121 selects one of two inputs (IN1, IN2) for its output, with ideal-diode reverse-current blocking during switchover, adjustable overvoltage supervisors per input (OV1, OV2), a priority supervisor (PR1) and comparator input (CP2), adjustable current limit (1–4.5 A) and soft start, and a status output (SLVSEA3F p. 1, §1, §3). Its typical RON is 56 mΩ and its fast switchover 5 µs (p. 3, §5). In the T1 it feeds `VBUS_CHG` (the BQ25895 input) from USB-C VBUS on IN1 (priority) or from the powerbank HAT `HAT_5V` on IN2. OV1 and OV2 also serve as interlocks: they are forced high whenever the T1 itself sources USB-C VBUS or `HAT_5V`, so the T1's own 5 V cannot re-enter the charger (BOM v1 line 45, power tree §1 finding 10, §4.6).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| IN1, IN2, OUT | −0.3 | 24 | V | SLVSEA3F p. 6, §7.1 |
| OV1, OV2 | −0.3 | 6 | V | p. 6, §7.1 |
| PR1 (PRI) and other control pins | −0.3 | 6 | V | p. 6, §7.1 |
| ST | −0.3 | 6 | V | p. 6, §7.1 |
| Output current | internally limited | — | — | p. 6, §7.1 |
| Junction temperature | internally limited | — | — | p. 6, §7.1 |
| Storage temperature | −65 | 150 | °C | p. 6, §7.1 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 6, §7.2 |
| ESD, CDM (JESD22-C101) | — | ±500 | V | p. 6, §7.2 |

The table names PRI and SEL; SEL exists only on the TPS2120, CP2 only on the TPS2121. The datasheet gives no separate CP2 row; treating CP2 like PR1 (−0.3 to 6 V) is **UNVERIFIED**.

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Input voltage IN1, IN2 | 2.8 | — | 22 | V | SLVSEA3F p. 6, §7.3 |
| Output voltage | 0 | — | 22 | V | p. 6, §7.3 |
| OV1, OV2, PR1 voltage | 0 | — | 5.5 | V | p. 6, §7.3 |
| ST voltage | 0 | — | 5.5 | V | p. 6, §7.3 |
| ST pull-up resistance | 6 | — | 20 | kΩ | p. 6, §7.3 |
| RILM | 18 | — | 100 | kΩ | p. 6, §7.3 |
| SS pin output voltage | — | — | 4 | V | p. 6, §7.3 |
| Continuous input current (TPS2121) | — | — | 4.5 | A | p. 6, §7.3 |
| Junction temperature | −40 | — | 125 | °C | p. 6, §7.3 |
| Input UVLO rising | 2.5 | 2.65 | 2.8 | V | p. 7, §7.5 |
| Input UVLO falling | 2.4 | 2.55 | 2.7 | V | p. 7, §7.5 |
| RON, IOUT = −200 mA, VINx ≥ 5 V, 25 °C | — | 56 | 70 | mΩ | p. 7, §7.5 |
| RON, same, −40 to 85 °C | — | — | 85 | mΩ | p. 7, §7.5 |
| RON, same, −40 to 125 °C | — | — | 100 | mΩ | p. 7, §7.5 |
| VREF rising (PR1, CP2, OV1, OV2) | 1.01 | 1.06 | 1.1 | V | p. 8, §7.5 |
| VREF falling | 0.99 | 1.04 | 1.09 | V | p. 8, §7.5 |
| Control pin leakage, 0–5.5 V | −0.1 | — | 0.1 | µA | p. 8, §7.5 |
| ILM, RILM = 80 kΩ | 1 | 1.5 | 2 | A | p. 8, §7.5 |
| ILM, RILM = 44.2 kΩ | 2 | 2.5 | 3 | A | p. 8, §7.5 |
| ILM, RILM = 29.8 kΩ | 3 | 3.5 | 4 | A | p. 8, §7.5 |
| ILM, RILM = 22.1 kΩ | 4 | 4.5 | 5 | A | p. 8, §7.5 |
| ILM, RILM < 1 kΩ | 1.5 | 2.5 | 3.5 | A | p. 8, §7.5 |
| Thermal shutdown / recovery | — | 160 / 150 | — | °C | p. 8, §7.5 |

Thermal (p. 6–7, §7.4, column labelled "RNW (PKG FAM) 11 pins"): RθJA 72.2 °C/W, RθJC(top) 38.5 °C/W, RθJB 15.4 °C/W, ψJB 15.5 °C/W.

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Quiescent from the input powering OUT | OUT open, −40 to 125 °C | 300 | 400 | µA | SLVSEA3F p. 7, §7.5 |
| Standby, input not powering OUT | VOUT = VINx, 25 °C | 15 | 25 | µA | p. 7, §7.5 |
| Leakage INx to OUT, \|VINx − VOUT\| ≤ 5 V | 25 °C | — | ±1 | µA | p. 7, §7.5 |
| Leakage INx to OUT, \|VINx − VOUT\| ≤ 22 V | −40 to 85 °C | — | ±35 | µA | p. 7, §7.5 |
| Both inputs invalid | OUT Hi-Z | — | — | — | p. 18, Table 9-3 |

The front page quotes 200 µA typical from the enabled input and 10 µA from the disabled input (p. 1, §1); the Electrical Characteristics table above (300 / 15 µA) is the specification.

## Pinout and package

| Pin | Name | Type | Function |
|---|---|---|---|
| 1, 8 | OUT | Power | Power output |
| 2 | IN2 | Power in | Power input for source 2 |
| 3 | CP2 | I | Enables comparator operation; compared to PR1 to set switchover. GND if not used |
| 4 | OV2 | I | Active-low enable supervisor for IN2 overvoltage. GND if not used |
| 5 | OV1 | I | Active-low enable supervisor for IN1 overvoltage. GND if not used |
| 6 | PR1 | I | Enables priority operation; connect to IN1 (divider) to set switchover voltage. GND if not used |
| 7 | IN1 | Power in | Power input for source 1 |
| 9 | ST | O | Status: high when OUT is IN1 or Hi-Z, low when OUT is IN2. GND if not used |
| 10 | ILM | O | Output current limit for both channels (resistor to GND) |
| 11 | SS | O | Input settling delay and output soft start (capacitor to GND) |
| 12 | GND | — | Device ground |

Source: SLVSEA3F p. 4–5, Figure 6-2, Pin Functions table; ST behaviour p. 18, §9.5. Marking 2121, MSL 1 at 260 °C, 3000 per reel (p. 41, Package Option Addendum).

## Recommended footprint

- Package outline, example board layout and stencil: drawing RUX0012A (4224010/A), SLVSEA3F p. 38–40. Pad pitch 0.5 mm (6× 0.5 on the drawing), stencil example based on 0.1 mm thickness (p. 40). The drawing shows vias under the power pads ("VIA TYP", p. 39). Exact pad sizes are to be taken from the drawing, not from extracted text (**UNVERIFIED** until the KiCad footprint is checked against p. 39).
- Use short, wide traces for IN1, IN2 and OUT; for high current place vias under the input and output pins (p. 33, §12.1–12.2).

## Application circuit and required passives

| Item | Value / rule | Source |
|---|---|---|
| RILM (kΩ, 18–100) | ILM = 65.2 / RILM^0.861 | SLVSEA3F p. 13, §9.3.2, Equation 2 |
| CSS | sets settling time and soft-start slew; 100 nF ≈ 780–880 V/s, 1 µF ≈ 88–92 V/s, 10 µF ≈ 8.8–10.4 V/s | p. 13, Table 9-1 |
| OVx divider | trip when VOVx reaches VREF (1.06 V typ): VTRIP = 1.06 V × (R1 + R2) / R2 | p. 15, Figure 9-5; p. 23, Equations 6–7 |
| PR1 divider (priority) | IN1 selected while VPR1 > VREF; e.g. 10.2 kΩ / 5 kΩ trips at 3.22 V | p. 23, Equation 5 |
| ST pull-up | 6–20 kΩ | p. 6, §7.3 |
| Bypass capacitors | close to IN1, IN2, OUT; low-ESR X5R or X7R | p. 33, §11 |
| Input TVS | for hot-plugged cable inputs; example TVS1800 clamps a 12 V cable hot-plug from > 30 V to 19.3 V | p. 31–32, §10.7 |
| Output dip during switchover | VDIP = tSW × IOUT / COUT | p. 15, §9.3.7, Equations 3–4 |

Reference schematic for a 12 V / 5 V priority mux with values: Figure 10-9, p. 25.

## Interfaces and timing

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Switchover time (CP2 < VREF) | — | 100 | — | µs | SLVSEA3F p. 7, §7.5 |
| Fast switchover time (CP2 ≥ VREF) | — | 5 | — | µs | p. 7, §7.5 |
| Input comparator VCOMP (VIN1 ≥ VIN2) | 0 | 280 | 600 | mV | p. 7, §7.5 |
| Comparator offset VOFST | 5 | 20 | 40 | mV | p. 8, §7.5 |
| Current-limit response time | — | 250 | — | µs | p. 8, §7.5 |
| Fast-trip OCP | ≈ 2.4 × ILM, off within 1 µs, off for about 25 ms then retry | — | — | — | p. 14, §9.3.3 |
| Fast reverse-current detection IRCB | 0.2 | 1 | 2 | A | p. 8, §7.5 |
| RCB release voltage VRCB | 0 | 25 | 50 | mV | p. 8, §7.5 |
| RCB response time | — | 10 | — | µs | p. 8, §7.5 |
| ST delay, L to H | — | 1 | — | µs | p. 8, §7.5 |

Source selection (p. 18, Table 9-3): an input is invalid when it is below UV or its OVx pin is ≥ VREF. Only one valid input → that input; both invalid → OUT Hi-Z; both valid, CP2 low, PR1 ≥ VREF → IN1; both valid, CP2 low, PR1 low → the higher voltage (IN2 wins ties); CP2 high → PR1 versus CP2 decides.

## Linux driver

None. The device has no digital bus. ST can be read on a GPIO to report the active input; the kernel consumer for it (for example a `gpio` power-supply or `extcon` node) is **UNVERIFIED** and is OpenDAP's choice, not a datasheet statement.

## Simulation models

No model is listed in `manifest.toml`. A TI PSpice model is **UNVERIFIED**.

## Design notes for the T1

- **Absolute maximum 24 V, operating 22 V** on IN1, IN2 and OUT (p. 6) confirms the figures used in the power tree §4.7 and risk 5.
- **RON (power tree §4.7):** 56 mΩ is the 25 °C typical. The maximum is 70 mΩ at 25 °C and 100 mΩ over −40 to 125 °C (p. 7). At 2 A input the worst-case loss is 0.40 W, not 0.22 W.
- **OV1 / OV2 forced high (power tree risk 6):** a channel is disabled when its OVx pin is at or above VREF, 1.1 V maximum rising (p. 8). Any drive that holds the pin between 1.1 V and 5.5 V (recommended maximum, absolute maximum 6 V, p. 6) disables the channel. A 1.8 V or 3.3 V logic level is sufficient; a direct 5.1 V drive stays inside 5.5 V but has little margin. The forcing source must not load the OVx divider in normal operation (for example a diode or open-drain OR into the divider midpoint); the exact circuit is **UNVERIFIED** and is a schematic task.
- **OV1 threshold:** the BOM states OV1 ≈ 13.7 V, the power tree §4.7 states about 14.5 V. The datasheet only fixes VREF (1.01–1.1 V rising, p. 8), so the trip point spread is set by VREF and the divider tolerance; the target value has to be made consistent between the two documents.
- **Supervisor accuracy:** OVx and PR1 accuracy < ±5 % (p. 1, §1).
- **Hot-plug:** USB-C is a cable input; the datasheet example shows > 30 V spikes without a TVS (p. 32). The BOM's TVS2200 on VBUS and TVS0500 on `HAT_5V` address this; their clamp versus the 24 V absolute maximum is power tree risk 5.
- **Current limit:** RILM must stay within 18–100 kΩ (p. 6); RILM < 1 kΩ is a defined fallback of 1.5–3.5 A (p. 8). The value for the 3.25 A `VBUS_CHG` limit in the power tree §3 is not chosen in the BOM; Equation 2 gives about 32.5 kΩ for 3.25 A typical (calculation).

## Sources

- TI, TPS2120 / TPS2121 datasheet, SLVSEA3F, revised August 2020, <https://www.ti.com/lit/ds/symlink/tps2121.pdf>, sha256 `b2f5950f596dc2c4ca33e4ebac27fd35e4dcc68ea63e173466123e1118e91a06` (manifest). Page numbers are PDF page numbers.
- OpenDAP board BOM v1 line 45 and power tree v0 §1, §3, §4.6, §4.7, §9 (T1 context).
