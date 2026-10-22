# OPA1622IDRCR

- **Manufacturer:** Texas Instruments
- **Function:** Dual bipolar-input audio operational amplifier with a high-current output stage and an enable pin
- **BOM v1 lines:** 19 (Audio, headphone drivers), quantity 6 (v1.3: 4 → 6, ADR 0012); its difference-amplifier resistors, capacitors and ballast resistors are on lines 37, 107 and 108
- **Package:** VSON-10 (DRC0010J), 3 mm × 3 mm, tape and reel of 3000, NiPdAu, MSL 1 at 260 °C, marking O1622 (SBOS727B, package option addendum, PDF p. 29)
- **Datasheet:** OPA1622 "SoundPlus High-Fidelity, Bipolar-Input, Audio Operational Amplifier", SBOS727B, November 2015, revised May 2016 (manifest sha256 `505556d1…ac9824`, verified against the cached copy)
- **Status:** Partly UNVERIFIED

## Summary

The OPA1622 is a dual bipolar-input audio operational amplifier with a high-current output stage (+145/−130 mA short-circuit), 2.8 nV/√Hz input noise at 1 kHz, an enable pin referenced to a dedicated ground pin, and a low-power shutdown mode of 5 µA per channel (SBOS727B, pp. 1, 5–6). In the T1 it is the headphone driver after the CS43198 DACs: six packages, each running both halves in parallel, four for the 4.4 mm balanced output (one per leg: L+, L−, R+, R−) and two for the 3.5 mm output (one per channel), each enabled separately for power gating. BOM line 19 (v1.3, ADR 0012).

## Absolute maximum ratings

SBOS727B, §6.1, p. 4.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| Supply voltage VS = (V+) − (V−) | — | 40 | V |
| Input voltage (signal inputs, enable, ground) | (V−) − 0.5 | (V+) + 0.5 | V |
| Input differential voltage | — | ±0.5 | V |
| Input current, all pins except supplies | — | ±10 | mA |
| Output short-circuit (to VS/2, one amplifier per package) | Continuous | — | — |
| Operating temperature TA | −55 | 125 | °C |
| Junction temperature TJ | — | 200 | °C |
| Storage temperature Tstg | −65 | 150 | °C |

ESD: HBM ±4000 V, CDM ±1500 V (SBOS727B, §6.2, p. 4).

## Recommended operating conditions

SBOS727B, §6.3, p. 4.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| Supply voltage, single supply | 4 | 36 | V |
| Supply voltage, dual supply | ±2 | ±18 | V |
| Specified temperature | −40 | 125 | °C |

Supplies need not be symmetrical; the common-mode voltage must stay within (V−) + 1.5 V to (V+) − 1 V (SBOS727B, §9, p. 26; §6.5, p. 5).

Selected electrical characteristics, TA = 25 °C, VS = ±2 V to ±18 V, RL = 1 kΩ unless noted (SBOS727B, §6.5, pp. 5–6):

| Parameter | Condition | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| THD+N | G = 1, 1 kHz, 10 mW, RL = 32 Ω, 80 kHz BW | — | −116 | — | dB |
| THD+N | G = 1, 1 kHz, 10 mW, RL = 16 Ω, 80 kHz BW | — | −113 | — | dB |
| THD+N | G = 1, 1 kHz, 3.5 Vrms, RL = 600 Ω | — | −132 | — | dB |
| Input voltage noise density | 1 kHz | — | 2.8 | — | nV/√Hz |
| Input voltage noise density | 10 Hz | — | 10 | — | nV/√Hz |
| Input voltage noise | 20 Hz–20 kHz | — | 2.1 | — | µVpp |
| Input current noise density | 1 kHz | — | 0.8 | — | pA/√Hz |
| Input offset voltage | 25 °C | — | ±100 | ±500 | µV |
| Input bias current | 25 °C | — | 1.2 | 2.0 | µA |
| Gain-bandwidth product | G = 1000 / G = 1 | — | 32 / 8 | — | MHz |
| Slew rate | G = −1 | — | 10 | — | V/µs |
| Channel separation | 1 kHz | — | 140 | — | dB |
| CMRR | −40 to 125 °C | 110 | 127 | — | dB |
| PSRR | — | — | 0.1 | 3 | µV/V |
| Output swing from rail | RL = 600 Ω | — | 900 | — | mV |
| Short-circuit current | VS = ±18 V | — | +145 / −130 | — | mA |
| Open-loop gain | RL = 32 Ω, VS = ±5 V | 114 | 120 | — | dB |

## Power by mode

SBOS727B, §6.5, p. 6.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Enabled, quiescent, per channel | VEN = 2.0 V, IOUT = 0, 25 °C | 2.6 | 3.3 | mA |
| Enabled, quiescent, per channel | −40 to 125 °C | — | 4.2 | mA |
| Shutdown, per channel | VEN = 0 V, IOUT = 0 | 5 | 10 | µA |

Thermal (DRC, JEDEC): RθJA 47.6 °C/W, RθJB 22.0 °C/W, RθJC(bot) 4.1 °C/W (SBOS727B, §6.4, p. 4). Thermal shutdown at TJ above 175 °C, re-enable below about 160 °C (§7.3.2, p. 15).

## Pinout and package

SBOS727B, §5, p. 3.

| Pin | Name | Function |
|---|---|---|
| 1 | +IN A | Non-inverting input A |
| 2 | V+ | Positive supply |
| 3 | GND | Ground reference for EN and internal compensation |
| 4 | V− | Negative supply |
| 5 | +IN B | Non-inverting input B |
| 6 | −IN B | Inverting input B |
| 7 | OUT B | Output B |
| 8 | EN | Shutdown (low) / enable (high) |
| 9 | OUT A | Output A |
| 10 | −IN A | Inverting input A |
| Pad (11) | Thermal pad | Connect to V− |

Package DRC0010J: body 2.9–3.1 mm × 2.9–3.1 mm, height 0.8–1.0 mm, pitch 0.5 mm, lead width 0.18–0.30 mm, exposed pad 1.65 ± 0.1 mm × 2.4 ± 0.1 mm (SBOS727B, package outline, PDF p. 34).

## Recommended footprint

TI example board layout for DRC0010J, drawing 4218878/B (SBOS727B, PDF p. 35):

- 10 pads 0.6 mm × 0.24 mm at 0.5 mm pitch, pad rows 2.8 mm apart (outer extents).
- Thermal pad 11: 1.65 mm × 2.4 mm, with 0.25 mm-wide tabs extending to 3.4 mm overall; optional Ø0.2 mm vias, filled, plugged or tented if under paste.
- Non-solder-mask-defined pads preferred, mask opening 0.07 mm maximum all around.
- Stencil: 0.125 mm thick, 80 % printed coverage on the exposed pad (SBOS727B, PDF p. 36; aperture details in the drawing).

The thermal pad must be soldered (SBOS727B, PDF p. 34 note 3) and connected to a copper pour at V−, extended with vias to a larger plane (§7.3.1, p. 15; §10.1, p. 26).

## Application circuit and required passives

- **Bypass:** low-ESR 0.1 µF ceramic from each supply pin to ground, as close as possible (SBOS727B, §10.1, p. 26).
- **Difference amplifier for a voltage-output DAC** (SBOS727B, Figure 52, p. 22; §8.2, pp. 22–25): R1 = R3 = 499 Ω, R2 = R4 = 768 Ω, C1 = C2 = 470 pF across R2/R4; gain VOUT = VDAC · R2 / (R1 + ROUT) (Equation 5, p. 23); C1/C2 pole kept ≥ 416.6 kHz for < 0.01 dB deviation at 20 kHz (Equations 9–11, p. 24). Design targets: ±5 V supplies, 150 mW into 32 Ω, THD+N < −115 dB (§8.2.1, p. 22). Built with 0.1 % thin-film 0603 resistors and film capacitors (§8.2.3, p. 24).
- **Measured maximum output before clipping (±5 V, Figure 52 circuit):** 16 Ω 95 mW at −114.2 dB; 32 Ω 150 mW at −118.7 dB; 600 Ω 11.3 mW at −119.4 dB (SBOS727B, Table 2, p. 24).
- **EN hold-off divider** when EN is not driven by a GPIO: 22.1 kΩ from VCC and 10.7 kΩ to ground (SBOS727B, Figure 48, p. 18).
- **Input current limiting:** in low-gain stages with fast input edges, limit input current to ≤ 10 mA with RI or RF (§7.3.6, p. 17).
- **Capacitive load:** headphone loads up to 400 pF are expected (§8.2.2, p. 22); phase margin vs. load in Figure 24 (p. 10).

## Interfaces and timing

- **EN:** shutdown at VEN ≤ 0.78 V, enabled at VEN ≥ 0.82 V, referenced to the GND pin (SBOS727B, §7.3.3, p. 16). Over −40 to 125 °C the thresholds are 0.95 V (high) and 0.65 V (low) (§6.5, p. 6). EN current IEN ≈ (VEN − 0.7 V) / 700 kΩ (Equation 4, p. 16); 1.5 µA at VEN = 1.8 V (§6.5, p. 6). EN must not float or be left high-impedance (§7.3.3, p. 16). A 1.8 V GPIO meets the high threshold.
- **Shutdown output:** the output is not high-impedance in shutdown; driving the output can parasitically power the output stage (§7.4.1, p. 18).
- **Enable transitions:** brief output transients on the µs scale (Figures 46–47, p. 18).

## Linux driver

None. The amplifier has no control interface; EN lines are GPIOs (BOM v1 line 19, driver path "none").

## Simulation models

- The datasheet points to TINA-TI and its macro-model library (SBOS727B, §11.1.1.1, p. 27). The availability of an OPA1622-specific PSpice or TINA-TI macromodel on ti.com: **UNVERIFIED**.
- Related reference design: TIDUAW1, "Headphone Amplifier for Voltage-Output Audio DACs" (§11.2.1, p. 27).
- No model is listed in `manifest.toml` for this part.

## Design notes for the T1

- Supplies (v1.3): the T1 runs the OPA1622 from ±6.04 V (LT3045 HPA_P6V0 and LT3094 HPA_N6V0, BOM lines 25–26), made from the ±7.0 V TPS65131 pre-rails (line 22). This is inside the ±2 V to ±18 V dual-supply range (§6.3); the datasheet application uses ±5 V (§8.2.1); output swing against current at ±6 V is **UNVERIFIED** (power tree v0 §4.1).
- Topology (v1.3, ADR 0012): both halves of every package in parallel, each half its own difference amplifier (R1 = R3 = 1.00 kΩ, R2 = R4 = 1.62 kΩ, 100 pF, gain 1.62; BOM lines 37, 108) driving the output through a 1.0 Ω ballast resistor outside the loop (line 107). Paralleling halves is not described in SBOS727B; current sharing and stability with the ballast resistors are **UNVERIFIED** until simulated and measured (BOM line 19).
- Enable per output (v1.3): 8 halves enabled for balanced, 4 for SE. A package in shutdown does not present a high-impedance output, and signals applied to it can parasitically power the output stage (§7.4.1, p. 17); a whole package is therefore the smallest unit that can be disabled (power tree v0 §4.1).
- Pop control: ramp V+ and V− symmetrically and hold EN low while the supplies ramp (§7.4.2, p. 18). v1.3: the LT3045 and LT3094 ramp on equal RSET × CSET soft-starts, about 65 ms (power tree v0 §4.2, §6.2). BOM line 100 reserves a DNP mute shunt in case measurements show pops.
- Thermal pad and its pour go to V− (−6 V), not to ground (§10.1).
- GND pin: connect to the low-noise analog reference (§7.3.4, p. 16; §10.1).
- Feedback resistors close to the inverting input, short input traces (§10.1, Figure 60).
- Headphone ESD (TPD1E10B06, BOM line 36) sits after the feedback node per the BOM note.
- Thermal (est., power tree v0 §4.1): about 0.5 W per package at the balanced 32 Ω full-scale sine, +24 °C at θJA 47.6 °C/W (§6.4).

## Sources

- Texas Instruments, OPA1622 data sheet, SBOS727B, May 2016, <https://www.ti.com/lit/ds/symlink/opa1622.pdf>, sha256 `505556d18113e86aed84f20c1dbcfc6b4ad66ccdc5202998bd883f7a7eac9824`.
- OpenDAP board BOM v1 (v1.3), lines 19, 22, 25, 26, 36, 37, 100, 107, 108; power tree v0 §4.1, §4.2, §6.2 (`public/board/docs/specs/`).
