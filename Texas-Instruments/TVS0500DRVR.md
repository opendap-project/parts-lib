# TVS0500DRVR

- **Manufacturer:** Texas Instruments
- **Function:** 5 V unidirectional flat-clamp surge protection device (TI Flat-Clamp family)
- **Package:** WSON-6 (DRV), 2.0 × 2.0 mm, exposed thermal pad
- **Datasheet:** TVS0500 5-V Flat-Clamp Surge Protection Device, SLVSED2C (December 2017, revised November 2019), sha256 `ac7a4dc56da9…` in `manifest.toml`
- **BOM v1 line:** 65

## Summary

The TVS0500 is an active (feedback-controlled) clamp with 5 V stand-off that shunts up to 43 A of IEC 61000-4-5 8/20 µs surge current with a 9.2 V typical clamp, and integrates IEC 61000-4-2 level 4 ESD protection (SLVSED2C §1, §3, p. 1). In the T1 two parts protect the HAT 5 V and 3.3 V rails at the HAT flat-cable connector (BOM v1 line 65).

## Absolute maximum ratings

TA = 27 °C unless noted (SLVSED2C p. 5, §7.1).

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Surge current | IEC 61000-4-5 (8/20 µs) | — | 43 | A | p. 5, §7.1 |
| Surge power | IEC 61000-4-5 (8/20 µs) | — | 400 | W | p. 5 |
| Surge current | IEC 61643-321 (10/1000 µs) | — | 20 | A | p. 5 |
| Surge power | IEC 61643-321 (10/1000 µs) | — | 180 | W | p. 5 |
| Forward surge current | IEC 61000-4-5 (8/20 µs) | — | 50 | A | p. 5 |
| Forward surge power | IEC 61000-4-5 (8/20 µs) | — | 80 | W | p. 5 |
| Forward surge current | IEC 61643-321 (10/1000 µs) | — | 23 | A | p. 5 |
| Forward surge power | IEC 61643-321 (10/1000 µs) | — | 60 | W | p. 5 |
| EFT | IEC 61000-4-4 | — | 80 | A | p. 5 |
| DC breakdown current, IBR | — | — | 50 | mA | p. 5 |
| DC forward current, IF | — | — | 500 | mA | p. 5 |
| Ambient operating temperature, TA | — | −40 | 125 | °C | p. 5 |
| Storage temperature, Tstg | — | −65 | 150 | °C | p. 5 |
| ESD, HBM | JS-001, all pins | — | ±2000 | V | p. 5, §7.2 |
| ESD, CDM | JESD22-C101, all pins | — | ±500 | V | p. 5, §7.2 |
| ESD, IEC 61000-4-2 contact | — | — | ±24 | kV | p. 5, §7.3 |
| ESD, IEC 61000-4-2 air gap | — | — | ±30 | kV | p. 5, §7.3 |

## Recommended operating conditions

| Parameter | Min | Nom | Max | Unit | Reference |
|---|---|---|---|---|---|
| Reverse stand-off voltage, VRWM | — | — | 5 | V | p. 5, §7.4 |
| Input voltage range for proper function | 0 | — | 5 | V | §10, p. 12 |

### Electrical characteristics

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| Leakage, ILEAK | VIN = VRWM, 27 °C | — | 0.07 | 5.5 | nA | p. 6, §7.6 |
| Leakage, ILEAK | VIN = VRWM, 85 °C | — | 6.5 | 220 | nA | p. 6 |
| Leakage, ILEAK | VIN = VRWM, 105 °C | — | 38 | 755 | nA | p. 6 |
| Forward voltage, VF | 1 mA, GND to IO | 0.25 | 0.5 | 0.65 | V | p. 6 |
| Breakdown voltage, VBR | 1 mA, IO to GND | 7.5 | 7.9 | 8.4 | V | p. 6 |
| Forward clamp, VFCLAMP | 35 A 8/20 µs, GND to IO, 27 °C | — | 2 | 5 | V | p. 6 |
| Clamp, VCLAMP | 24 A 8/20 µs, VIN = 0 V before surge, 27 °C | — | 8.6 | 8.8 | V | p. 6 |
| Clamp, VCLAMP | 43 A 8/20 µs, VIN = 0 V before surge, 27 °C | — | 9.2 | 9.5 | V | p. 6 |
| Clamp, VCLAMP | 35 A 8/20 µs, VIN = VRWM before surge, 125 °C | — | 9.2 | 9.5 | V | p. 6 |
| Dynamic resistance, RDYN | 8/20 µs, 27 °C | — | 30 | 50 | mΩ | p. 6 |
| Input capacitance, CIN | VIN = 5 V, 1 MHz | — | 155 | — | pF | p. 6 |
| Maximum input slew rate, SR | 0 to VRWM, IPEAK = 1 mA, 27 °C | — | 2.5 | — | V/µs | p. 6 |
| Maximum input slew rate, SR | same, 105 °C | — | 0.7 | — | V/µs | p. 6 |

Thermal (DRV): RθJA 70.4 °C/W, RθJB 40 °C/W, RθJC(bot) 11 °C/W (pp. 5–6, §7.5).

## Power by mode

Not applicable: no supply pin (§10, p. 12). Standing loss is the leakage at the rail voltage; TI quotes about 70 pA at 5 V, under 1 nW (§9.2.2, p. 11).

## Pinout and package

WSON-6 (DRV), top view (Pin Configuration and Functions, p. 4):

| Pin | Name | Type | Description |
|---|---|---|---|
| 1, 2, 3 | GND | Ground | Ground |
| 4, 5, 6 | IN | I | ESD- and surge-protected channel |
| Exposed pad | GND | Ground | Ground |

Outline DRV0006A (drawing 4222173/C 11/2025, PDF p. 19, same drawing as the TVS2200): body 1.9–2.1 × 1.9–2.1 mm, 0.7–0.8 mm height, 0.65 mm pitch, exposed pad 1.0 ± 0.1 × 1.6 ± 0.1 mm. NiPdAu finish, MSL Level-1-260C-UNLIM, reel of 3000, marking 1HRH (package option addendum, p. 15).

## Recommended footprint / land pattern

DRV0006A example board layout (drawing 4222173/C, PDF p. 20): six pads 0.45 × 0.3 mm (reference) at 0.65 mm pitch, pad column centre-to-centre 1.95 mm, thermal pad 1.0 × 1.6 mm with optional Ø 0.2 mm vias, non-solder-mask-defined pads preferred with 0.07 mm maximum clearance. Stencil on PDF p. 21. One shared KiCad footprint serves TVS0500 and TVS2200.

## Application circuit and required passives

No passives. IN pins 4–6 to the protected rail, GND pins 1–3 and the pad to ground (Figure 10, p. 11). Two parts in series, reversed, give bidirectional ±5 V operation (§9.2.3, p. 12; not characterized for the TVS0500 itself).

## Interfaces and timing

Not applicable (no logic interface). Input slew rate above 2.5 V/µs (27 °C) or 0.7 V/µs (125 °C) makes the device conduct for a few microseconds; regular fast swings can overheat it (§8.5.3, p. 10).

## Linux driver

None (passive protection part).

## Simulation models available

None listed in `manifest.toml`. Whether TI publishes a SPICE model for this device is **UNVERIFIED**.

## Design notes for the T1

- VRWM is exactly 5 V and the recommended input range is 0–5 V (p. 5; §10). If the HAT 5 V rail is regulated above 5.0 V or carries tolerance above it, the TVS0500 operates beyond its stand-off. The HAT 5 V setpoint of the TPS61088 boost (BOM v1 line 91) against this limit is **UNVERIFIED**; check it before freeze. On the 3.3 V rail there is ample margin.
- Clamp is 9.2–9.5 V at 43 A (p. 6): downstream parts on the HAT rails (eFuse outputs, load switches) must tolerate that.
- Rail turn-on edges faster than 2.5 V/µs make the device conduct briefly (§8.5.3). The eFuse (TPS259470, BOM v1 line 44) soft-start slew is expected to be slower, but this is **UNVERIFIED** here.
- 155 pF per rail (p. 6) is negligible against rail decoupling.
- Place at the HAT flat-cable connector with short ground connections; keep unprotected traces away from the protected section (§11.1, p. 13; Figure 11, p. 13).

## Sources

- TI, *TVS0500 5-V Flat-Clamp Surge Protection Device*, SLVSED2C, revised November 2019, <https://www.ti.com/lit/ds/symlink/tvs0500.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 44, 65, 91
