# TVS2200DRVR

- **Manufacturer:** Texas Instruments
- **Function:** 22 V unidirectional flat-clamp surge protection device (TI Flat-Clamp family)
- **BOM v1 lines:** 64 (main USB-C VBUS TVS)
- **Package:** WSON-6 (DRV), 2.0 × 2.0 mm, exposed thermal pad
- **Datasheet:** TVS2200 22-V Flat-Clamp Surge Protection Device, SLVSED5C (December 2017, revised August 2023), sha256 `84c986c9cc4f…` in `manifest.toml`
- **Status:** Partly UNVERIFIED

## Summary

The TVS2200 is an active (feedback-controlled) clamp with 22 V stand-off that shunts up to 40 A of IEC 61000-4-5 8/20 µs surge current while holding the clamp near 28 V, with integrated IEC 61000-4-2 level 4 ESD protection (SLVSED5C §1, §3, p. 1). TI names USB Type-C VBUS as an application and shows it on a 20 V VBUS input (§9.2.1, p. 10). In the T1 it is the VBUS TVS of the main USB-C receptacle (BOM v1 line 64).

## Absolute maximum ratings

TA = 27 °C unless noted (SLVSED5C p. 4, §7.1).

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Surge current | IEC 61000-4-5 (8/20 µs) | — | 40 | A | p. 4, §7.1 |
| Surge power | IEC 61000-4-5 (8/20 µs) | — | 1120 | W | p. 4 |
| Surge current | IEC 61643-321 (10/1000 µs) | — | 5 | A | p. 4 |
| Surge power | IEC 61643-321 (10/1000 µs) | — | 145 | W | p. 4 |
| Forward surge current | IEC 61000-4-5 (8/20 µs) | — | 50 | A | p. 4 |
| Forward surge power | IEC 61000-4-5 (8/20 µs) | — | 80 | W | p. 4 |
| Forward surge current | IEC 61643-321 (10/1000 µs) | — | 23 | A | p. 4 |
| Forward surge power | IEC 61643-321 (10/1000 µs) | — | 60 | W | p. 4 |
| EFT | IEC 61000-4-4 | — | 80 | A | p. 4 |
| DC breakdown current, IBR | — | — | 18 | mA | p. 4 |
| DC forward current, IF | — | — | 500 | mA | p. 4 |
| Ambient operating temperature, TA | — | −40 | 125 | °C | p. 4 |
| Storage temperature, Tstg | — | −65 | 150 | °C | p. 4 |
| ESD, HBM | JS-001, all pins | — | ±2000 | V | p. 4, §7.2 |
| ESD, CDM | JESD22-C101, all pins | — | ±500 | V | p. 4, §7.2 |
| ESD, IEC 61000-4-2 contact | — | — | ±17 | kV | p. 4, §7.3 |
| ESD, IEC 61000-4-2 air gap | — | — | ±30 | kV | p. 4, §7.3 |

## Recommended operating conditions

| Parameter | Min | Nom | Max | Unit | Reference |
|---|---|---|---|---|---|
| Reverse stand-off voltage, VRWM | — | — | 22 | V | p. 4, §7.4 |
| Input voltage range for proper function | 0 | — | 22 | V | §9.3, p. 11 |

### Electrical characteristics

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| VRWM | — | −0.5 | — | 22 | V | p. 5, §7.6 |
| Leakage, ILEAK | VIN = VRWM, 27 °C | — | 3.5 | 62 | nA | p. 5 |
| Leakage, ILEAK | VIN = VRWM, 85 °C | — | 25 | 400 | nA | p. 5 |
| Leakage, ILEAK | VIN = VRWM, 105 °C | — | 80 | 1300 | nA | p. 5 |
| Forward voltage, VF | 1 mA, GND to IO | 0.25 | 0.5 | 0.65 | V | p. 5 |
| Breakdown voltage, VBR | 1 mA, IO to GND | 24.6 | 25.9 | 27.6 | V | p. 5 |
| Forward clamp, VFCLAMP | 40 A 8/20 µs, GND to IO, 27 °C | 1 | 2 | 5 | V | p. 5 |
| Clamp, VCLAMP | 24 A 8/20 µs, VIN = 0 V before surge, 27 °C | — | 27.2 | 27.7 | V | p. 5 |
| Clamp, VCLAMP | 40 A 8/20 µs, VIN = 0 V before surge, 27 °C | — | 27.6 | 28 | V | p. 5 |
| Clamp, VCLAMP | 35 A 8/20 µs, VIN = VRWM before surge, 125 °C | — | 27.8 | 28.35 | V | p. 5 |
| Dynamic resistance, RDYN | 8/20 µs, 27 °C | — | 30 | — | mΩ | p. 5 |
| Input capacitance, CIN | VIN = VRWM, 1 MHz | — | 105 | — | pF | p. 5 |
| Maximum input slew rate, SR | 0 to VRWM, IPK = 1 mA, 27 °C | — | 2.5 | — | V/µs | p. 5 |
| Maximum input slew rate, SR | same, 105 °C | — | 0.7 | — | V/µs | p. 5 |

Thermal (DRV): RθJA 70.4 °C/W, RθJB 40 °C/W, RθJC(bot) 11 °C/W (p. 5, §7.5).

## Power by mode

Not applicable: no supply pin (§9.3, p. 11). Standing loss is the leakage at the rail voltage (3.5 nA typical at 22 V, 27 °C; p. 5).

## Pinout and package

WSON-6 (DRV) (Figure 6-1 and Table 6-1, p. 3):

| Pin | Name | Type | Description |
|---|---|---|---|
| 1, 2, 3 | GND | Ground | Ground |
| 4, 5, 6 | IN | I | ESD- and surge-protected channel |
| 7 (exposed pad) | GND | Ground | Ground |

Outline DRV0006A (drawing 4222173/C 11/2025, PDF p. 18): body 1.9–2.1 × 1.9–2.1 mm, 0.7–0.8 mm height, 0.65 mm pitch, exposed pad 1.0 ± 0.1 × 1.6 ± 0.1 mm, terminals 0.25–0.35 mm wide and 0.2–0.3 mm long. The thermal pad must be soldered (note 3). NiPdAu finish, MSL Level-1-260C-UNLIM, reel of 3000, marking 1HVH (package option addendum, p. 14).

## Recommended footprint

DRV0006A example board layout (PDF p. 19, drawing 4222173/C, scale 25:1):

- Six pads 0.45 × 0.3 mm (reference), 0.65 mm pitch, pad column centre-to-centre 1.95 mm (reference).
- Thermal pad 1.0 × 1.6 mm (reference) with optional Ø 0.2 mm vias at 1.1 mm spacing.
- Non-solder-mask-defined pads preferred, 0.07 mm maximum mask clearance.
- Stencil: example on PDF p. 20.

## Application circuit and required passives

No passives. IN pins 4–6 tie to the protected VBUS net; GND pins 1–3 and the exposed pad tie to ground (Figure 9-1, p. 10). Two parts in series, reversed, give bidirectional ±22 V operation (§9.2.4, p. 11; not characterized for the TVS2200 itself).

## Interfaces and timing

Not applicable (no logic interface). Input slew rate above 2.5 V/µs (27 °C) or 0.7 V/µs (125 °C) makes the device conduct for a few microseconds; regular fast swings can overheat it (§8.5.3, p. 9).

## Linux driver

None (passive protection part).

## Simulation models

None listed in `manifest.toml`. Whether TI publishes a SPICE model for this device is **UNVERIFIED**.

## Design notes for the T1

- Stand-off 22 V covers 20 V USB PD VBUS. On a surge the downstream node sees up to 28 V at 40 A (27 °C) or 28.35 V at 35 A (125 °C) (p. 5). Every part on unprotected VBUS (CC/PD controller, charger input, power mux, eFuse) must tolerate that clamp; this is the clamp-coordination risk in BOM v1 line 64 and power tree §4.7.
- VBUS hot-plug edges can exceed 2.5 V/µs. The datasheet says faster slew only makes the device conduct briefly and is harmless unless repeated regularly (§8.5.3, p. 9); behaviour on a real 20 V hot plug in the T1 is **UNVERIFIED** until measured.
- 105 pF input capacitance (p. 5) adds to the VBUS capacitance seen by a source; it is small against the USB bulk capacitance.
- Place at the receptacle with short, wide connections to the ground plane; keep unprotected traces away from the protected section (§9.4.1, p. 11; Figure 9-3, p. 12).
- Second source in the BOM (SMBJ24A) is a conventional TVS with a softer clamp (BOM v1 line 64).

## Sources

- TI, *TVS2200 22-V Flat-Clamp Surge Protection Device*, SLVSED5C, revised August 2023, <https://www.ti.com/lit/ds/symlink/tvs2200.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 64
