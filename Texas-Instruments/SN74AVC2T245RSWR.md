# SN74AVC2T245RSWR

- **Manufacturer:** Texas Instruments
- **Function:** 2-bit dual-supply bus transceiver, 1.2–3.6 V on each port, DIR per channel, common active-low OE, Ioff, VCC isolation
- **BOM v1 lines:** 95 (second source for the SN74AXC2T245RSWR, HAT audio translator for I2S-A MCLK and DOUT on the DAC clock; not fitted by default)
- **Package:** UQFN-10 (RSW, RSW0010A), 1.8 × 1.4 mm nominal, 0.4 mm pitch, 0.55 mm max height
- **Datasheet:** *SN74AVC2T245 Dual-Bit Dual-Supply Bus Transceiver with Configurable Level-Shifting / Voltage Translation and Tri-State Outputs*, SCES692E, June 2008, revised September 2024. Cited below as "SCES692E". File sha256 `2d473c07fce653298ed85fa2b948201ca6bd91616cd2b04eb486760c9de0eb3b` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The SN74AVC2T245 is a dual-bit noninverting bus transceiver with two configurable supply rails, VCCA and VCCB, each 1.2–3.6 V. The A port and the control pins (DIR1, DIR2, OE) are supplied by VCCA; the B port tracks VCCB (SCES692E, p. 1; p. 12, §7.1). Each channel has its own direction pin and one active-low OE disables both. I/Os are 4.6 V tolerant; Ioff and VCC isolation (either supply at GND) put both ports in high impedance (p. 1). Typical data rate is 500 Mb/s for 1.8 V to 3.3 V level-shifting (p. 1). Unlike the AXC part it has no internal pull-downs: input circuits are always active and must see a valid level (p. 1). In the T1 it is the BOM v1 line 95 second source for the SN74AXC2T245RSWR on the same land.

## Absolute maximum ratings

SCES692E, p. 4, §5.1.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VCCA, VCCB | −0.5 | 4.6 | V |
| VI, A port, B port, control inputs | −0.5 | 4.6 | V |
| VO, high-impedance or power-off state, A or B port | −0.5 | 4.6 | V |
| VO, high or low state, A port | −0.5 | VCCA + 0.5 | V |
| VO, high or low state, B port | −0.5 | VCCB + 0.5 | V |
| Input clamp current IIK (VI < 0) | −50 | — | mA |
| Output clamp current IOK (VO < 0) | −50 | — | mA |
| Continuous output current IO | — | ±50 | mA |
| Continuous current through VCCA, VCCB or GND | — | ±100 | mA |
| Junction temperature TJ | −40 | 150 | °C |
| Storage temperature Tstg | −65 | 150 | °C |

ESD (p. 4, §5.2): HBM 5000 V; CDM 1500 V.

## Recommended operating conditions

SCES692E, pp. 4–5, §5.3. VCCI is the supply of the input port, VCCO of the output port.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VCCA, VCCB | — | 1.2 | 3.6 | V |
| VIH, data inputs | VCCI 1.2–1.95 V | 0.65 × VCCI | — | V |
| VIH, data inputs | VCCI 2.7–3.6 V | 2 | — | V |
| VIL, data inputs | VCCI 1.2–1.95 V | — | 0.35 × VCCI | V |
| VIL, data inputs | VCCI 2.7–3.6 V | — | 0.8 | V |
| VIH, DIR (referenced to VCCA) | VCCA 1.2–1.95 V | 0.65 × VCCA | — | V |
| VIL, DIR (referenced to VCCA) | VCCA 1.2–1.95 V | — | 0.35 × VCCA | V |
| VI | — | 0 | 3.6 | V |
| VO, active state | — | 0 | VCCO | V |
| VO, 3-state | — | 0 | 3.6 | V |
| IOH / IOL | VCCO 1.65–1.95 V | — | −8 / 8 | mA |
| IOH / IOL | VCCO 3–3.6 V | — | −12 / 12 | mA |
| Input transition rise or fall rate Δt/Δv | — | — | 5 | ns/V |
| Operating free-air temperature TA | — | −40 | 85 | °C |

All unused data inputs must be held at VCCI or GND (p. 5, note 3).

Thermal, RSW (p. 5, §5.4): RθJA 227.4 °C/W, RθJC(top) 96.3 °C/W, RθJB 139.6 °C/W, ψJT 5.2 °C/W, ψJB 139.2 °C/W.

### Electrical characteristics (selected)

SCES692E, p. 6, §5.5; limits over −40 to 85 °C.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VOH | IOH = −100 µA, VCCA and VCCB 1.2–3.6 V | VCCO − 0.2 | — | V |
| VOH | IOH = −8 mA, VCC 1.65 V | 1.2 | — | V |
| VOH | IOH = −12 mA, VCC 3 V | 2.3 | — | V |
| VOL | IOL = 100 µA, VCCA and VCCB 1.2–3.6 V | — | 0.2 | V |
| VOL | IOL = 8 mA, VCC 1.65 V | — | 0.45 | V |
| VOL | IOL = 12 mA, VCC 3 V | — | 0.7 | V |
| II, control inputs | VI = VCCA or GND | — | ±1 | µA |
| Ioff, A or B port | one supply at 0 V, VI or VO 0–3.6 V | — | ±5 | µA |
| IOZ, A or B port | OE = VIH, VCCA = VCCB = 3.6 V | — | ±5 | µA |
| Ci, control inputs | 3.3 V supplies | 3.5 typ | 4.5 (25 °C) | pF |
| Cio, A or B port | 3.3 V supplies | 6 typ | 7 (25 °C) | pF |

## Power by mode

SCES692E, p. 6, §5.5 (VI = VCCI or GND, IO = 0, −40 to 85 °C) and p. 9, §5.11 (TA = 25 °C).

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Static, ICCA | VCCA and VCCB 1.2–3.6 V | — | 8 | µA |
| Static, ICCB | VCCA and VCCB 1.2–3.6 V | — | 8 | µA |
| Static, ICCA + ICCB | VCCA and VCCB 1.2–3.6 V | — | 16 | µA |
| Dynamic, CpdA, A to B, outputs enabled | VCCA = VCCB = 1.8 V, 10 MHz | 3 | — | pF |
| Dynamic, CpdB, A to B, outputs enabled | VCCA = VCCB = 1.8 V, 10 MHz | 13 | — | pF |
| Dynamic, CpdA, A to B, outputs enabled | VCCA = VCCB = 3.3 V, 10 MHz | 4 | — | pF |
| Dynamic, CpdB, A to B, outputs enabled | VCCA = VCCB = 3.3 V, 10 MHz | 16 | — | pF |

Cpd is given for equal supplies only; the value for VCCA = 1.8 V with VCCB = 3.3 V is not tabulated (**UNVERIFIED**).

## Pinout and package

SCES692E, p. 3, Figure 4-1 and Table 4-1.

| Pin | Name | Function |
|---|---|---|
| 1 | DIR2 | Direction for channel 2; connect to GND or VCCA |
| 2 | OE | Tri-state output enable, active low; high puts all outputs in 3-state; referenced to VCCA |
| 3 | GND | Ground |
| 4 | B2 | Channel 2, B side; level from VCCB |
| 5 | B1 | Channel 1, B side; level from VCCB |
| 6 | VCCB | Supply B |
| 7 | VCCA | Supply A |
| 8 | A1 | Channel 1, A side; level from VCCA |
| 9 | A2 | Channel 2, A side; level from VCCA |
| 10 | DIR1 | Direction for channel 1; connect to GND or VCCA |

Pin-by-pin comparison with the SN74AXC2T245 (SCES879A, p. 2, Table 4-1): all ten pins carry the same names and functions (1 DIR2, 2 OE, 3 GND, 4 B2, 5 B1, 6 VCCB, 7 VCCA, 8 A1, 9 A2, 10 DIR1), and both datasheets use the same outline, RSW0010A, drawing 4224897/A 03/2019 (SCES692E, pp. 22–24; SCES879A, pp. 29–31). The BOM's "same RSW pinout" claim is confirmed.

Orderable SN74AVC2T245RSWR (p. 18): active, 3000 per reel, NiPdAu or NiPdAuAg, MSL Level-1-260C-UNLIM, −40 to 85 °C, marking one of TQ7, TQO, TQR and others.

## Recommended footprint

Same RSW0010A example board layout as the SN74AXC2T245 (SCES692E, p. 23; stencil p. 24, 0.125 mm): 10 pads 0.2 mm wide (reference), pads 2–10 0.6 mm long, pad 1 0.7 mm long, 0.4 mm pitch, 1.6 mm between the centres of the top and bottom pad rows (reference); non-solder-mask-defined pads preferred, 0.05 mm maximum mask clearance. One footprint serves both parts.

## Application circuit and required passives

| Ref | Value | Note |
|---|---|---|
| Bypass, VCCA and VCCB | not given | "Bypass capacitors should be used on power supplies" (p. 15, §10.1); the SN74AXC2T245 value, 0.1 µF each, is the design choice (**UNVERIFIED** for this part) |
| OE pull-up to VCCA | value set by the driver's sink capability | Needed to ensure the high-impedance state during power-up and power-down (p. 1); the layout example keeps OE high until both supplies are up (p. 15, Figure 10-1). The typical application uses 1 kΩ (p. 13, Figure 8-1) |
| Data-line pulls | value not given | Inputs must not float; tie unused ports directly to ground (p. 13, §8.1, §8.2.1) |

## Interfaces and timing

Function table, each transceiver (p. 12, Table 7-1):

| OE | DIR | A port | B port | Operation |
|---|---|---|---|---|
| L | L | Enabled | Hi-Z | B data to A |
| L | H | Hi-Z | Enabled | A data to B |
| H | X | Hi-Z | Hi-Z | Isolation |

Switching, VCCA = 1.8 V ± 0.15 V, VCCB = 3.3 V ± 0.3 V, −40 to 85 °C (p. 8, §5.8):

| Parameter | Min | Max | Unit |
|---|---|---|---|
| tPLH, tPHL, A to B | 0.1 | 3.3 | ns |
| tPLH, tPHL, B to A | 0.1 | 3.7 | ns |
| tPZH, tPZL, OE to A | 0.3 | 4.6 | ns |
| tPZH, tPZL, OE to B | 0.2 | 6.7 | ns |
| tPHZ, tPLZ, OE to A | 0.8 | 6.5 | ns |
| tPHZ, tPLZ, OE to B | 0.1 | 6.7 | ns |

Typical data rate 500 Mb/s for 1.8 V to 3.3 V (p. 1). After a DIR change, the enable time is the disable time of the old output plus the propagation delay (p. 13, §8.1.1, Eq. 1–4).

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. The datasheet names no simulation model; whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **Drop-in on the land.** Pinout and outline match the SN74AXC2T245RSWR pin for pin (see Pinout and package), so line 95 keeps one footprint for both.
- **Differences that matter for the swap:**
  - No internal pull-downs: every input, including the B-side pins of an absent HAT, needs a defined level (p. 1; p. 13, §8.2.1). BOM v1 line 95 already asks for pulls on the HAT side; they must be fitted when this part is placed. With the AXC part fitted, external pull-ups would fight its 71 kΩ pull-downs and must be ≤ 7 kΩ (SCES879A, p. 19), so pull-downs are the value that suits both parts (**UNVERIFIED** as a schematic choice).
  - OE needs a pull-up to VCCA for a defined high-impedance state through power-up and power-down (p. 1).
  - Operating range −40 to 85 °C against −40 to 125 °C for the AXC part (p. 5; orderable addendum p. 18).
  - Input transition limit 5 ns/V against 10 ns/V (p. 5).
  - Supply minimum 1.2 V; both T1 supplies (1.8 V and 3.3 V) are inside it.
- **Control levels.** DIR and OE are referenced to VCCA = 1.8 V: VIH ≥ 1.17 V, VIL ≤ 0.63 V (p. 4–5).
- **Stock.** LCSC C128418: 171,893 (BOM v1 line 95, 2026-10-22).

## Sources

- TI, *SN74AVC2T245 Dual-Bit Dual-Supply Bus Transceiver with Configurable Level-Shifting / Voltage Translation and Tri-State Outputs*, SCES692E (September 2024): <https://www.ti.com/lit/ds/symlink/sn74avc2t245.pdf>
- TI, SN74AXC2T245, SCES879A (February 2024), for the pin and footprint comparison: <https://www.ti.com/lit/ds/symlink/sn74axc2t245.pdf>
- OpenDAP board BOM v1 (v1.1), line 95 and §9 D8 (`public/board/docs/specs/bom-v1.md`).
