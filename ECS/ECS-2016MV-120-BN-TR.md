# ECS-2016MV-120-BN-TR

- **Manufacturer:** ECS Inc.
- **Function:** 12 MHz HCMOS crystal oscillator (XO), 1.6–3.6 V supply, tri-state output
- **BOM v1 lines:** 14 (RP2350 12 MHz clock into XIN, qty 1; BOM v1.1, replaces the ABM8-272-T3 crystal)
- **Package:** 4-pad ceramic SMD, 2.0 × 1.6 × 0.85 mm max
- **Datasheet:** *ECS-2016MV SMD MultiVolt Crystal Oscillator*, Rev. 2025 (2 pages). Cited below as "ECS-2016MV". File sha256 `f179ffbc8a8257a363abd72fb03ddc445cfae44fed3edb7e32cd938101c61872` (matches the BOM v1.1 Datasheets table).
- **Status:** Partly UNVERIFIED

## Summary

The ECS-2016MV is a miniature SMD HCMOS oscillator for 1.6–3.6 V in a 2.0 × 1.6 × 0.85 mm ceramic package (ECS-2016MV, p. 1). Part number decoded with the part numbering guide (p. 1) and the developed-frequency list (p. 2):

| Field | Value | Meaning |
|---|---|---|
| ECS | ECS | Manufacturer prefix |
| 2016MV | series | 2.0 × 1.6 mm MultiVolt oscillator |
| 120 | frequency code | 12.000 MHz (developed frequency, p. 2) |
| B | stability | ±50 ppm |
| N | temperature range | −40 to +85 °C |
| -TR | packaging | 1K per reel (-TR3 = 3K) |

Frequency stability includes initial tolerance, temperature, supply voltage, load change, reflow shift and aging (p. 1, note). In the T1 it runs from RP_IOVDD_1V8 (1.8 V) and drives the RP2354A XIN pin with a square wave; XOUT is left open and the tri-state pin is left open, so the output is always active (BOM v1 line 14; power tree v0 §3).

## Absolute maximum ratings

Not given in the datasheet. Supply above 3.6 V is outside the specified range (p. 1). Storage −55 to +125 °C (p. 1). Reflow: peak 260 ± 5 °C for 10 ± 5 s, 2 cycles max (p. 2).

## Recommended operating conditions

ECS-2016MV, p. 1, Operating Conditions / Electrical Characteristics.

| Parameter | Condition | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| Frequency range (series) | — | 1.500 | | 54.000 | MHz |
| Frequency stability | B option | | | ±50 | ppm |
| Supply voltage | — | 1.6 | | 3.6 | V |
| Output load | CMOS | | | 15 | pF |
| Operating temperature | N option (part numbering guide) | −40 | | +85 | °C |
| Storage temperature | — | −55 | | +125 | °C |

The table's operating temperature row (−40 to +105 °C) is for the P option and its ±30 ppm stability row is for the GP option; the N and B values above come from the part numbering guide (p. 1).

## Power by mode

Current consumption, mA max (p. 1, table):

| Supply | up to ~19 MHz | ~39.9 MHz | ~50 MHz | ~60 MHz |
|---|---|---|---|---|
| 1.8 V | 2.5 | 3.0 | 3.5 | 4.0 |
| 2.5 V | 4.5 | 5.5 | 6.5 | 7.0 |
| 3.3 V | 6.0 | 7.0 | 8.0 | 8.5 |

- T1 operating point (12 MHz, 1.8 V): 2.5 mA max, matching power tree v0 §3 (RP_IOVDD_1V8: "12 MHz XO, ≤ 2.5 mA at 1.8 V").
- Standby (output in high impedance): 10 µA max (p. 1). Not used in the T1 (tri-state pin open).
- The load conditions of the current table are not stated (**UNVERIFIED**).

## Pinout and package

Pad connections (p. 1):

| Pad | Function |
|---|---|
| 1 | Tri-state |
| 2 | GND |
| 3 | Output |
| 4 | Vdd |

Figure 1 (p. 1): body 2.0 ± 0.1 × 1.6 ± 0.1 mm, height 0.85 mm max; top view with the pin-1 dot at the lower left, pads numbered #1 lower left, #2 lower right, #3 upper right, #4 upper left. The bottom view gives 0.575 ± 0.1, 0.7 ± 0.1 and 0.1 mm horizontally and 0.475 ± 0.1, 0.5 ± 0.1, 0.475 ± 0.1 mm vertically; which feature each dimension references is read from the drawing only (**UNVERIFIED** until checked against the PDF when drawing the footprint).

Solder profile (p. 2): MSL 1, lead finish Au, peak 260 ± 5 °C, 10 ± 5 s max, 2 cycles max.

## Recommended footprint

Figure 2, suggested land pattern (p. 1): four pads in a 2 × 2 grid. Horizontal dimensions 0.775 / 0.5 / 0.775 mm, vertical 0.675 / 0.3 / 0.675 mm, read as pads 0.775 × 0.675 mm separated by a 0.5 mm gap horizontally and a 0.3 mm gap vertically (overall 2.05 × 1.65 mm). Mask and paste rules are not given (**UNVERIFIED**).

## Application circuit and required passives

- The datasheet gives no application circuit or bypass value.
- BOM v1 §5 places 100 nF on the 12 MHz XO supply, with no crystal load capacitors or XOUT resistor (design choice, not from this datasheet).
- Tri-state function (p. 1): pin 1 ≥ 0.7 × Vdd or not connected → output active; pin 1 ≤ 0.3 × Vdd → output high impedance. Leaving pin 1 open keeps the output on.

## Interfaces and timing

ECS-2016MV, p. 1.

| Parameter | Condition | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| Output level | — | VOH ≥ 90 % Vdd | | VOL ≤ 10 % Vdd | V |
| Rise and fall time | 10–90 % Vdd | | | 6.5 | ns |
| Duty cycle | at ½ Vdd | 45 | | 55 | % |
| Start-up time | to 90 % Vdd | | | 5 | ms |
| Phase jitter | 12 kHz–5 MHz | | | 1 | ps |

At Vdd = 1.8 V the output swings to ≥ 1.62 V and ≤ 0.18 V. The RP2354A XIN pin accepts a 1–50 MHz input (RP2350 datasheet Table 1686, transcribed on the [RP2354A](../Raspberry-Pi/RP2354A.md) sheet; BOM v1 line 14). The XIN input thresholds at IOVDD = 1.8 V are not checked in this sheet (**UNVERIFIED**).

## Linux driver

None. The oscillator serves the RP2354A coprocessor only (BOM v1 line 14: driver path *none*).

## Simulation models

None listed in `manifest.toml`. ECS model availability is **UNVERIFIED**.

## Design notes for the T1

- **Why an oscillator:** the Raspberry Pi crystal circuit is tuned for IOVDD = 3.3 V only; with IOVDD at 1.8 V the T1 drives XIN from this XO instead (BOM v1 line 14, §9 D6).
- **Supply:** RP_IOVDD_1V8 (1.8 V) is inside the 1.6–3.6 V range. The XO is gated with the RP2354A (`RP_PWR_EN`), so the 5 ms max start-up time applies at every RP2354A power-up; firmware and boot timing must allow it (**UNVERIFIED** against the RP2350 oscillator start-up handling).
- **Accuracy:** ±50 ppm over −40 to +85 °C including aging (p. 1). Whether this meets every RP2354A use of the 12 MHz reference (USB, UART timing) is **UNVERIFIED** here.
- **Ordering:** the BOM quotes stock for both -TR (1K reel) and -TR3 (3K reel); the electrical part is the same (p. 1). LCSC stock is 7 (BOM v1 §8 risk 7).
- The second source in the BOM is the ABM8-272-T3 crystal with a re-tuned XOUT resistor, after qualification over temperature (BOM v1 line 14).

## Sources

- ECS Inc., *ECS-2016MV SMD MultiVolt Crystal Oscillator*, Rev. 2025: <https://ecsxtal.com/store/pdf/ECS-2016MV.pdf>
- OpenDAP board BOM v1.1, line 14, §4.3, §5, §8, §9 D6; power tree v0 §2, §3 (`public/board/docs/specs/`).
