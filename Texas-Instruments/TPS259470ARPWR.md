# Texas Instruments TPS259470ARPWR

- **Function:** 2.7–23 V, 5.5 A eFuse with true reverse-current blocking, adjustable OVLO, active current limit, auto-retry
- **T1 use:** board BOM v1 line 44 (Power), ×3: #A `HAT_5V` out, #B `HAT_3V3` out, #C USB-C VBUS out; status Proposed
- **Datasheet:** TPS25947xx 2.7V to 23V, 5.5A, 28mΩ True Reverse Current Blocking eFuse with Input Reverse Polarity Protection, SLVSFC9C (October 2020, revised May 2026), <https://www.ti.com/lit/ds/symlink/tps25947.pdf>
- **Package:** VQFN-HR 10-pin, 2 mm × 2 mm, 0.45 mm pitch (RPW, drawing RPW0010A)

## Summary

The TPS25947xx is an eFuse with integrated back-to-back FETs (28.3 mΩ typical), input reverse-polarity protection, ideal-diode reverse-current blocking, adjustable current limit (0.5–6 A) with an analog load-current monitor on the same ILM pin, adjustable slew rate, and adjustable undervoltage lockout (SLVSFC9C p. 1, §1, §3). In the variant code, "0" selects adjustable OVLO with AUXOFF and FLT outputs and active current limiting; "A" selects auto-retry after a fault (p. 4, §4 Device Comparison Table). The T1 uses three, each fed from a dedicated source and each with a hardware current ceiling: #A from the TPS61088 5.1 V boost to `HAT_5V` (ILIM 1.5 A), #B from a TLV62569 to `HAT_3V3` (ILIM 1.0 A), #C from the TPS61088 to the USB-C VBUS source path (ILIM 1.5 A). ILM is read by the SoC SARADC as a current monitor (BOM v1 line 44, power tree §4.6).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| VIN (IN), −40 °C ≤ TJ ≤ 125 °C | max(−15, VOUT − 21) | 28 | V | SLVSFC9C p. 7, §6.1 |
| VIN (IN), −10 °C ≤ TJ ≤ 125 °C | max(−15, VOUT − 22) | 28 | V | p. 7, §6.1 |
| Input rising slew rate | — | 100 | V/µs | p. 7, §6.1 |
| Input falling slew rate | — | 10 | V/µs | p. 7, §6.1 |
| VOUT, −40 °C ≤ TJ ≤ 125 °C | −0.3 | min(28, VIN + 21) | V | p. 7, §6.1 |
| VOUT, minimum pulse (< 1 µs) | −0.8 | — | V | p. 7, §6.1 |
| EN/UVLO, OVLO, AUXOFF, FLT | −0.3 | 6.5 | V | p. 7, §6.1 |
| dVdt, ITIMER, ILM | internally limited | — | — | p. 7, §6.1 |
| Continuous switch current | internally limited | — | — | p. 7, §6.1 |
| Lead temperature | — | 300 | °C | p. 7, §6.1 |
| Storage temperature | −65 | 150 | °C | p. 7, §6.1 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 7, §6.2 |
| ESD, CDM (JS-002) | — | ±500 | V | p. 7, §6.2 |

Pins pulled up to VIN: use ≥ 350 kΩ to limit current under reverse polarity (p. 7, §6.1 note 2).

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Input voltage VIN | 2.7 | — | 23 | V | SLVSFC9C p. 8, §6.3 |
| Output voltage VOUT | — | — | min(23, VIN + 20) | V | p. 8, §6.3 |
| EN/UVLO voltage | — | — | 5 | V | p. 8, §6.3 |
| OVLO pin voltage (TPS259470x) | 0.5 | — | 1.5 | V | p. 8, §6.3 |
| FLT, AUXOFF pin voltage | — | — | 5 | V | p. 8, §6.3 |
| dVdt capacitor voltage rating | VIN + 5 | — | — | V | p. 8, §6.3 |
| ITIMER capacitor voltage rating | 4 | — | — | V | p. 8, §6.3 |
| RILM | 549 | — | 6650 | Ω | p. 8, §6.3 |
| Continuous switch current, TJ ≤ 125 °C | — | — | 5.5 | A | p. 8, §6.3 |
| Junction temperature TJ | −40 | — | 125 | °C | p. 8, §6.3 |
| IN UVP rising / falling | 2.44 / 2.35 | 2.53 / 2.42 | 2.64 / 2.55 | V | p. 8, §6.5 |
| RON, VIN = 12 V, 3 A, TJ = 25 °C | — | 28.2 | — | mΩ | p. 9, §6.5 |
| RON, 2.7–23 V, 3 A, −40 to 125 °C | — | — | 45 | mΩ | p. 9, §6.5 |
| UVLO rising threshold (EN/UVLO) | 1.183 | 1.20 | 1.223 | V | p. 9, §6.5 |
| UVLO falling threshold | 1.076 | 1.09 | 1.116 | V | p. 9, §6.5 |
| EN/UVLO shutdown threshold VSD(F) | 0.45 | — | 0.74 | V | p. 9, §6.5 |
| OVLO rising / falling threshold | 1.183 / 1.076 | 1.20 / 1.09 | 1.223 / 1.116 | V | p. 9, §6.5 |
| ILIM, RILM = 3.32 kΩ | 0.850 | 1.007 | 1.150 | A | p. 9, §6.5 |
| ILIM, RILM = 1.65 kΩ | 1.800 | 2.028 | 2.200 | A | p. 9, §6.5 |
| Scalable fast-trip ratio ISC : ILIM | — | 201 | — | % | p. 10, §6.5 |
| Fixed fast-trip threshold IFT | — | 22.2 | — | A | p. 10, §6.5 |
| IMON gain GIMON (IOUT 0.5–5.5 A, IOUT < ILIM) | 165 | 182 | 200 | µA/A | p. 10, §6.5 |
| Thermal shutdown rising / hysteresis | — | 154 / 10 | — | °C | p. 10, §6.5 |
| dVdt charging current | 0.81 | 2.21 | 3.82 | µA | p. 11, §6.5 |

Thermal (RPW, p. 8, §6.4): RθJA 41.7 °C/W on a custom 4-layer board with 8 thermal vias, 74.5 °C/W on JEDEC 2s2p with no vias; ψJB 20 / 27.6 °C/W.

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| On (TPS259470x) | VIN = 12 V, OUT open | 428 | 610 | µA | SLVSFC9C p. 9, §6.5 IQ(ON) |
| On, reverse-current blocking | VOUT = VIN + 1 V | 193 | — | µA | p. 9, §6.5 |
| Disabled | VSD(F) < VEN < VUVLO(F) | 73 | 130 | µA | p. 9, §6.5 IQ(OFF) |
| Shutdown | VEN < VSD(F) | 4.4 | 28.7 | µA | p. 9, §6.5 ISD |
| OVLO off state | VOUT = VIN + 1 V | 190 | 267 | µA | p. 9, §6.5 |
| OUT leakage, unpowered | VOUT = 12 V, VIN = 0 V | 4.86 | — | µA | p. 10, §6.5 |
| Conduction loss | I² × RON | — | — | — | p. 9, §6.5 (RON) |

## Pinout and package

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | EN/UVLO | Analog in | Active-high enable; divider from supply sets UVLO. Do not leave floating |
| 2 | OVLO | Analog in | Divider sets the overvoltage lockout; also usable as an active-low enable. Do not leave floating |
| 3 | AUXOFF | Digital out (open drain) | High when the input is valid and inrush is complete (priority MUX control) |
| 4 | FLT | Digital out (open drain) | Active-low fault indication |
| 5 | IN | Power | Power input |
| 6 | OUT | Power | Power output |
| 7 | DVDT | Analog out | Capacitor to GND sets output turn-on slew rate; open for fastest |
| 8 | GND | Ground | Device ground |
| 9 | ILM | Analog out | Resistor to GND sets ILIM; pin voltage is the load-current monitor. Do not leave floating |
| 10 | ITIMER | Analog out | Capacitor to GND sets the overcurrent blanking interval; open for fastest response |

Source: SLVSFC9C p. 5–6, Figure 5-1, Table 5-1. Device marking 2A9H, MSL 2 at 260 °C, 3000 per reel (p. 68, Package Option Addendum).

## Recommended footprint / land pattern

- Package outline, example board layout and stencil: drawing RPW0010A (4225183/A), SLVSFC9C p. 72–74. Stencil example based on 0.100 mm thickness (p. 74). The pad dimensions in the extracted text are not reliably attributable to individual pads; draw the footprint from the drawing itself (**UNVERIFIED** until the KiCad footprint is checked against p. 73).
- IN and OUT are the heat-sinking pins: connect them to as much copper as possible on top and bottom layers with thermal vias; vias under IN and OUT also equalise current and improve RON and current-sense accuracy (p. 63, §8.4.1).
- Layout examples: single device, Figure 8-22 (p. 63); two devices in PowerMUX, Figure 8-23 (p. 64).

## Application circuit and required passives

| Item | Value / rule | Source |
|---|---|---|
| CIN | ≥ 0.1 µF ceramic, close to IN and GND; 1 µF low-value ceramic suggested to damp transients, rated ≥ 2 × VIN | SLVSFC9C p. 60–62, §8.3, §8.4.1 |
| COUT | ≥ 1 µF low-ESR ceramic close to OUT | p. 61, §8.3.1; p. 63, §8.4.1 |
| RILM | RILM (Ω) = 3334 / ILIM (A), 549–6650 Ω; ≥ 750 Ω for UL 2367 recognition | p. 32, §7.3.5.3, Equation 7; p. 1, §1 |
| CdVdt | CdVdt (pF) = 2000 / SR (V/ms); open = fastest; add 100 Ω in series above 10 nF | p. 29–30, §7.3.5.1, Equations 3–4 |
| CITIMER | tITIMER (ms) = ΔVITIMER (V) × CITIMER (nF) / IITIMER (µA); open = fastest | p. 32, Equation 8 |
| UVLO divider | VIN(UV) = VUVLO(R) × (R1 + R2) / R2 | p. 26, Equation 1 |
| OVLO divider | VIN(OV) = VOV(R) × (R1 + R2) / R2 | p. 27, Equation 2 |
| Output Schottky to GND | optional, absorbs negative spikes from inductive loads | p. 60, §8.3.1 |
| TVS OUT-to-IN | recommended where a powered USB-C cable can drive OUT above the OUT-to-IN rating | p. 61, §8.3.1 |
| Input TVS | optional, keeps transients within absolute maximum | p. 61, §8.3.1 |

Measured turn-on slew rate (RL = 100 Ω, COUT = 1 µF, TJ = 25 °C, p. 11, §6.7):

| VIN | CdVdt open | CdVdt = 1800 pF | CdVdt = 3300 pF | Unit |
|---|---|---|---|---|
| 2.7 V | 12.14 | 0.87 | 0.5 | V/ms |
| 12 V | 28.1 | 1.09 | 0.61 | V/ms |
| 23 V | 44.78 | 1.25 | 0.71 | V/ms |

## Interfaces and timing

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| OVLO response, VOVLO > VOV(R) to VOUT falling | — | 1.2 | — | µs | SLVSFC9C p. 11, §6.6 |
| OVLO fast recovery (TPS259470x) | — | 90 | — | µs | p. 11, §6.6 |
| Current-limit response, settle within 5 % of ILIM | — | 400 | — | µs | p. 11, §6.6 |
| Scalable fast-trip response (IOUT > 3 × ILIM) | — | 500 | — | ns | p. 11, §6.6 |
| Fixed fast-trip response (IOUT > IFT) | — | 500 | — | ns | p. 11, §6.6 |
| Auto-retry interval after fault (A variants) | — | 110 | — | ms | p. 11, §6.6 |
| Reverse-current blocking response | — | 1 | — | µs | p. 11, §6.6 |
| Reverse-current blocking recovery | — | 50 | — | µs | p. 11, §6.6 |
| ITIMER discharge current (IOUT > ILIM) | 1.2 | 1.8 | 2.5 | µA | p. 10, §6.5 |
| ITIMER discharge threshold ΔVITIMER | 1.286 | 1.51 | 1.741 | V | p. 10, §6.5 |
| Reverse blocking entry, VIN − VOUT | −36.45 | −29.3 | −22.3 | mV | p. 10, §6.5 |
| FLT leakage | −1 | — | 1 | µA | p. 10, §6.5 |

- **Fault behaviour (TPS259470A):** persistent overcurrent → active current limit, FLT low after tITIMER, then thermal shutdown if the fault stays; auto-retry after tRST. Overtemperature latches the fault internally and asserts FLT; reverse current (VOUT − VIN > VREVTH) also pulls FLT low. Latched faults clear by cycling VIN or pulling EN/UVLO below VSD(F) (p. 37–38, Table 7-2, Table 7-3).
- **Load-current monitor:** IOUT = VILM / (RILM × GIMON) (p. 34, §7.3.6, Equation 9). Parasitic capacitance on ILM must stay below 50 pF for stable operation (p. 35 note; p. 43 note; p. 63).

## Linux driver

None. The device has no digital bus. In the device tree each output is a `regulator-fixed` node with an enable GPIO (`HAT5V_EN`, `HAT3V3_EN`, `USB_SRC_ON`, power tree §5); ILM is read through the RK3566 SARADC (`iio-channels`). This mapping is OpenDAP's design, not a datasheet statement. FLT can be routed to a GPIO interrupt; which kernel consumer reports it is **UNVERIFIED**.

## Simulation models available

No model is listed in `manifest.toml`. The datasheet points to a spreadsheet design tool, "TPS25947xx Design Calculator", in the product folder (p. 42, §8.1). A PSpice or SIMPLIS transient model is **UNVERIFIED**.

## Design notes for the T1

- **ILIM resistors (power tree §4.6):** with Equation 7, 2.21 kΩ gives 1.509 A and 3.32 kΩ gives 1.004 A. The power tree uses 3350 Ω·A, the datasheet 3334 Ω·A; the difference is about 0.5 % and does not change the E96 picks. The tabulated spread at 3.32 kΩ is 0.850–1.150 A (p. 9), i.e. ±15 % at 1 A; the ±10 % accuracy claim applies only above 1 A (p. 1).
- **Inrush (power tree §4.6):** the power tree's slew rates for 1.8 nF (0.87 V/ms at 2.7 V, 1.09 V/ms at 12 V) match §6.7. At 5 V, Equation 4 gives 1.11 V/ms; the 0.92 V/ms interpolation in the power tree is an estimate.
- **IMON range:** VILM = IOUT × GIMON × RILM. At ILIM this is about 3334 × 182 µA/A ≈ 0.61 V for any RILM, i.e. the monitor full scale is about 0.6 V regardless of the limit. With the RK3566 SARADC (1.8 V reference, **UNVERIFIED**), about one third of the ADC range is used. The 50 pF limit on ILM rules out a large filter capacitor; whether the SARADC sampling input needs a series resistor to meet it is **UNVERIFIED**.
- **Enable from 1.8 V logic:** the EN/UVLO rising threshold is 1.223 V maximum and the shutdown threshold 0.45 V minimum (p. 9), so a 1.8 V GPIO enables and fully shuts down the device. Drive EN low (not only below UVLO) to reach the 4.4 µA shutdown state.
- **OVLO pin:** must not float (p. 5). If OVLO is not used on #A/#B/#C, tie it to GND (the Electrical Characteristics test condition is VOVLO = 0 V, p. 8). For #C, an OVLO divider would add protection against a source on the USB-C connector; this is an option, not a BOM decision.
- **Reverse blocking:** OUT is blocked from IN at all times (p. 35, §7.3.7). A powerbank HAT driving `HAT_5V` while #A is off, or a USB-C source driving VBUS while #C is off, does not back-feed the TPS61088. Reverse current asserts FLT (p. 38, Table 7-3), so software must not read FLT as an overload while an external source is present.
- **USB-C path (#C):** the datasheet recommends a TVS from OUT to IN when a powered cable can drive OUT (p. 61). The BOM does not list one; to check against the TVS2200 placement.
- **Thermal:** at 1.5 A, conduction loss is 1.5² × 45 mΩ = 0.10 W worst case (RON max, p. 9), 64 mW typical.

## Sources

- TI, TPS25947xx datasheet, SLVSFC9C, revised May 2026, <https://www.ti.com/lit/ds/symlink/tps25947.pdf>, sha256 `8f96de389903091650d4f462dcfad3210071c3ae7093623a7978f34baf8a65b4` (manifest). Page numbers are PDF page numbers.
- OpenDAP board BOM v1 line 44 and power tree v0 §3, §4.6, §5 (T1 context).
