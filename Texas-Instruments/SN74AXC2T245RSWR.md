# SN74AXC2T245RSWR

- **Manufacturer:** Texas Instruments
- **Function:** 2-bit dual-supply bus transceiver, 0.65–3.6 V on each port, DIR per channel, common active-low OE, Ioff, VCC isolation
- **BOM v1 lines:** 95 (HAT audio translator for I2S-A MCLK and DOUT on the DAC clock, VCCIO6 1.8 V ↔ HAT 3.3 V, qty 1; replaces SN74AXC2T45DCUR in BOM v1.1)
- **Package:** UQFN-10 (RSW, RSW0010A), 1.8 × 1.4 mm nominal, 0.4 mm pitch, 0.55 mm max height
- **Datasheet:** *SN74AXC2T245 2-Bit Dual-Supply Bus Transceiver with Configurable Voltage Translation and Tri-State Outputs*, SCES879A, May 2020, revised February 2024. Cited below as "SCES879A". File sha256 `fd6cf4a6e830e80e76a2cbca4351f067dae9f8e3915d5086104a70e2d72e5d4f` (matches the BOM v1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The SN74AXC2T245 is a two-bit noninverting bus transceiver with two independently configurable supply rails, VCCA and VCCB, each 0.65–3.6 V. The A port and the control inputs (DIR1, DIR2, OE) track VCCA; the B port tracks VCCB (SCES879A, p. 1, p. 18 §7.1). Each channel has its own direction pin; one active-low OE puts both channels in the high-impedance state (p. 2, Table 4-1; p. 20, Table 7-1). It supports up to 380 Mb/s from 1.8 V to 3.3 V, Ioff partial power-down, VCC isolation below 100 mV and glitch-free supply sequencing (p. 1). The data I/Os carry 71 kΩ typical internal pull-downs (p. 19, §7.3.9). In the T1 it buffers the two I2S-A lines that run on the DAC clock domain, MCLK and DOUT, between the 1.8 V VCCIO6 bank (A side) and the 3.3 V HAT branch (B side); only the HAT branch is buffered (BOM v1 line 95).

## Absolute maximum ratings

SCES879A, p. 3, §5.1.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VCCA, VCCB | −0.5 | 4.2 | V |
| VI, A port, B port, control inputs | −0.5 | 4.2 | V |
| VO, high-impedance or power-off state, A or B port | −0.5 | 4.2 | V |
| VO, high or low state, A port | −0.5 | VCCA + 0.2 | V |
| VO, high or low state, B port | −0.5 | VCCB + 0.2 | V |
| Input clamp current IIK (VI < 0) | −50 | — | mA |
| Output clamp current IOK (VO < 0) | −50 | — | mA |
| Continuous output current IO | −50 | 50 | mA |
| Continuous current through VCC or GND | −100 | 100 | mA |
| Junction temperature TJ | — | 150 | °C |
| Storage temperature Tstg | −65 | 150 | °C |

The output positive-voltage rating may be exceeded up to 4.2 V if the output current rating is observed (p. 3, note 3).

ESD (p. 3, §5.2): HBM ±8000 V; CDM ±1000 V.

## Recommended operating conditions

SCES879A, p. 4, §5.4. VCCI is the supply of the input port, VCCO of the output port.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VCCA, VCCB | — | 0.65 | 3.6 | V |
| VIH, data inputs | VCCI 1.1–1.95 V | 0.65 × VCCI | — | V |
| VIH, data inputs | VCCI 3–3.6 V | 2 | — | V |
| VIL, data inputs | VCCI 1.1–1.95 V | — | 0.35 × VCCI | V |
| VIL, data inputs | VCCI 3–3.6 V | — | 0.8 | V |
| VIH, control inputs (DIRx, OE), referenced to VCCA | VCCA 1.1–1.95 V | 0.65 × VCCA | — | V |
| VIL, control inputs (DIRx, OE), referenced to VCCA | VCCA 1.1–1.95 V | — | 0.35 × VCCA | V |
| VI | — | 0 | 3.6 | V |
| VO, active state | — | 0 | VCCO | V |
| VO, tri-state | — | 0 | 3.6 | V |
| Input transition rate Δt/Δv | — | — | 10 | ns/V |
| Operating free-air temperature TA | — | −40 | 125 | °C |

All unused inputs must be held at VCC or GND (p. 4, note 3).

Thermal, RSW (p. 3, §5.3): RθJA 209.0 °C/W, RθJC(top) 129.1 °C/W, RθJB 122.9 °C/W, ψJT 18.4 °C/W, ψJB 122.5 °C/W.

### Electrical characteristics (selected)

SCES879A, p. 5, §5.5; −40 to 85 °C unless noted.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VOH | IOH = −100 µA, VCCA and VCCB 0.7–3.6 V | VCCO − 0.1 | — | V |
| VOH | IOH = −8 mA, VCC 1.65 V | 1.2 | — | V |
| VOH | IOH = −12 mA, VCC 3 V | 2.3 | — | V |
| VOL | IOL = 100 µA, VCCA and VCCB 0.7–3.6 V | — | 0.1 | V |
| VOL | IOL = 8 mA, VCC 1.65 V | — | 0.45 | V |
| VOL | IOL = 12 mA, VCC 3 V | — | 0.7 | V |
| II, control inputs | VI = VCCA or GND | −0.5 | 0.5 | µA |
| II, data inputs | VI = VCCI or GND | −4 | 4 | µA |
| Ioff, A or B port | one supply at 0 V, VI or VO 0–3.6 V | −4 | 4 | µA |
| IOZ, A or B port | OE = VIH, VCCA = VCCB = 3.6 V | −4 | 4 | µA |
| Ci, control inputs | VI = 3.3 V or GND, 3.3 V supplies | 3.0 typ | — | pF |
| Cio, data I/O | 3.3 V supplies | 5.1 typ | — | pF |

At −40 to 125 °C the data-input, Ioff and IOZ limits widen to ±8 µA and the control-input leakage to ±1 µA (p. 5).

## Power by mode

SCES879A, p. 5, §5.5 (VI = VCCI or GND, IO = 0) and p. 14, §5.14.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Static, ICCA | VCCA and VCCB 0.65–3.6 V, −40 to 85 °C | — | 10 | µA |
| Static, ICCB | VCCA and VCCB 0.65–3.6 V, −40 to 85 °C | — | 10 | µA |
| Static, ICCA + ICCB | −40 to 85 °C | — | 16 | µA |
| Static, ICCA + ICCB | −40 to 125 °C | — | 23 | µA |
| One supply off | VCCA = 0 V, VCCB = 3.6 V: ICCB | — | 5 | µA |
| Dynamic, CpdA, A to B, outputs enabled | VCCA = VCCB = 1.8 V, 1 MHz, 25 °C | 2.1 | — | pF |
| Dynamic, CpdA, B to A, outputs enabled | VCCA = VCCB = 1.8 V, 1 MHz, 25 °C | 12.5 | — | pF |

Cpd is given only for equal supplies (p. 14–15); the value for VCCA = 1.8 V with VCCB = 3.3 V is not tabulated (**UNVERIFIED**).

## Pinout and package

SCES879A, p. 2, Figure 4-1 and Table 4-1.

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | DIR2 | I | Direction for channel A2/B2; connect to GND or VCCA |
| 2 | OE | I | Tri-state output enable, active low; high puts all outputs in tri-state; referenced to VCCA |
| 3 | GND | G | Ground |
| 4 | B2 | I/O | Channel 2, B side; level from VCCB |
| 5 | B1 | I/O | Channel 1, B side; level from VCCB |
| 6 | VCCB | P | Supply B |
| 7 | VCCA | P | Supply A |
| 8 | A1 | I/O | Channel 1, A side; level from VCCA |
| 9 | A2 | I/O | Channel 2, A side; level from VCCA |
| 10 | DIR1 | I | Direction for channel A1/B1; connect to GND or VCCA |

Outline RSW0010A (drawing 4224897/A 03/2019, p. 29): body 1.35–1.45 × 1.75–1.85 mm, height 0.45–0.55 mm, standoff 0.00–0.05 mm; 0.4 mm pitch; terminals 0.15–0.25 mm wide, 0.35–0.45 mm long; JEDEC MO-288 variation UDEE except minimum height. No exposed pad is drawn. Orderable SN74AXC2T245RSWR: active, 3000 per reel, NiPdAu, MSL Level-1-260C-UNLIM, −40 to 125 °C, marking 1HN (p. 25).

## Recommended footprint

RSW0010A example board layout (p. 30) and stencil (p. 31, 0.125 mm thick):

- 10 pads, 0.2 mm wide (reference); pads 2–10 are 0.6 mm long, pad 1 is 0.7 mm long; 0.4 mm pitch; 1.6 mm between the centres of the top and bottom pad rows (reference); R0.05 corners.
- Non-solder-mask-defined pads preferred, 0.05 mm maximum mask clearance all around.
- Stencil apertures equal to the pads.

Take the land from the drawing, not from these notes, when building the footprint.

## Application circuit and required passives

| Ref | Value | Note |
|---|---|---|
| CVCCA | 0.1 µF | Close to VCCA; 1 µF in parallel improves transient performance (p. 23, §8.4.1) |
| CVCCB | 0.1 µF | Close to VCCB (p. 23, §8.4.1) |
| OE pull-up | value not given | The typical application (p. 21, Figure 8-1) shows pull-ups that keep the device disabled during power-up; OE may instead be tied to GND to keep it enabled |

- Apply the ground reference first; no supply ramp order or rate is required (p. 23, §8.3).
- Inputs need fast edges per Δt/Δv; a slow or noisy input needs a Schmitt-trigger buffer first (p. 18, §7.3.1).
- External pull-ups on data I/Os must be ≤ 7 kΩ to overcome the 71 kΩ internal pull-down (p. 19, §7.3.9).

## Interfaces and timing

Function table, each transceiver (p. 20, Table 7-1):

| OE | DIRx | A port | B port | Operation |
|---|---|---|---|---|
| L | L | Output | Input (Hi-Z) | B data to A bus |
| L | H | Input (Hi-Z) | Output | A data to B bus |
| H | X | Input (Hi-Z) | Input (Hi-Z) | Isolation |

Input circuits of the data I/Os are always active; pins configured as inputs must not float (p. 20, notes 1–2).

Switching, VCCA = 1.8 V ± 0.15 V, VCCB = 3.3 V ± 0.3 V (p. 11, §5.11):

| Parameter | −40 to 85 °C | −40 to 125 °C | Unit |
|---|---|---|---|
| tpd, A to B | 0.5–5 | 0.5–5 | ns |
| tpd, B to A | 0.5–4 | 0.5–5 | ns |
| tdis, OE to A | 0.5–15 | 0.5–16 | ns |
| tdis, OE to B | 0.5–12 | 0.5–13 | ns |
| ten, OE to A | 0.5–14 | 0.5–15 | ns |
| ten, OE to B | 0.5–11 | 0.5–12 | ns |

Data rate up to 380 Mb/s when translating from 1.8 V to 3.3 V (p. 19, §7.3.10).

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. The datasheet names no simulation model (p. 24, §9); whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **Supplies.** VCCA on the VCCIO6 1.8 V domain, VCCB on the HAT 3.3 V side (BOM v1 line 95). DIR1, DIR2 and OE are referenced to VCCA, so 1.8 V GPIOs drive them directly: VIH ≥ 0.65 × VCCA ≈ 1.17 V, VIL ≤ 0.35 × VCCA ≈ 0.63 V (p. 4).
- **Absent HAT.** OE high isolates both ports (Table 7-1). If the HAT supply is below 100 mV, VCC isolation puts both ports in high impedance, and Ioff bounds the leakage to ±4 µA per pin (pp. 5, 18). This is the property the SN74AXC2T45 lacked (BOM v1 §9 D8). The default state of OE at power-up (pull-up to VCCA or a GPIO default) is a schematic decision; the datasheet example uses a pull-up (p. 21).
- **Internal pull-downs.** The 71 kΩ pull-downs hold every data I/O low when undriven, including the B-side pins of an absent HAT, so floating inputs are not a concern on this part (p. 19, §7.3.9). They are a static load on any driver holding a line high: about 3.3 V / 71 kΩ ≈ 46 µA per B-side line held high (typical value; minimum resistance not given, **UNVERIFIED**).
- **Direction.** Which of MCLK and DOUT is A to B and which is B to A follows the pin plan §5.1; whether DIR1 and DIR2 are strapped or GPIO-driven is not fixed in the BOM (**UNVERIFIED**). A strap to VCCA or GND is allowed (p. 2, Table 4-1).
- **Speed.** At 1.8 → 3.3 V the propagation delay is at most 5 ns and the rated data rate is 380 Mb/s (pp. 11, 19). The edge and duty-cycle quality of a translated audio master clock is not specified in the datasheet; any jitter added on the HAT MCLK path is **UNVERIFIED** and belongs to the HAT branch only (the on-board DAC clock nets are not translated, BOM v1 line 95).
- **Stock.** BOM v1 line 95 flags thin LCSC stock (596); the second source is the [SN74AVC2T245RSWR](SN74AVC2T245RSWR.md) on the same land.

## Sources

- TI, *SN74AXC2T245 2-Bit Dual-Supply Bus Transceiver with Configurable Voltage Translation and Tri-State Outputs*, SCES879A (February 2024): <https://www.ti.com/lit/ds/symlink/sn74axc2t245.pdf>
- OpenDAP board BOM v1 (v1.1), line 95 and §9 D8 (`public/board/docs/specs/bom-v1.md`).
