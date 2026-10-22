# TPS22919DCKR

- **Manufacturer:** Texas Instruments
- **Function:** 5.5 V, 1.5 A, 90 mΩ load switch with controlled rise time, short-circuit protection and adjustable quick output discharge
- **BOM v1 lines:** 50 (Power), ×7: DAC_VP, DAC_DIG_1V8, FP_1V8, FP_3V3, MIC_1V8, RP_3V3, RP_IOVDD_1V8; status Proposed
- **Package:** SC-70 6-pin (DCK, drawing DCK0006A), 2.1 × 2.0 mm nominal
- **Datasheet:** TPS22919 5.5 V, 1.5 A, 90-mΩ Self-Protected Load Switch with Controlled Rise Time, SLVSEN5B (October 2018, revised May 2019), <https://www.ti.com/lit/ds/symlink/tps22919.pdf>
- **Status:** Partly UNVERIFIED

## Summary

The TPS22919 is a single N-channel load switch for 1.6–5.5 V rails, 1.5 A continuous, with a fixed slow turn-on slew, output short-circuit current limiting, thermal shutdown, a smart pull-down on ON and a QOD pin that sets the output discharge (SLVSEN5B p. 1, §1 and §3). The T1 uses seven of them (BOM line 50) to power-gate blocks that have no enable of their own: the CS43198 VP and digital rails, the faceplate 1.8 V and 3.3 V rails, the microphones, and the RP2354A supply and IO rails (power tree §5). Enables come from SoC GPIOs or the TCA6416A expander.

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| VIN | −0.3 | 6 | V | SLVSEN5B p. 4, §6.1 |
| VOUT | −0.3 | 6 | V | p. 4, §6.1 |
| VON | −0.3 | 6 | V | p. 4, §6.1 |
| VQOD | −0.3 | 6 | V | p. 4, §6.1 |
| Continuous current IMAX | — | 1.5 | A | p. 4, §6.1 |
| Pulsed current (2 ms, 2 % duty) | — | 2.5 | A | p. 4, §6.1 |
| Junction temperature | internally limited | — | °C | p. 4, §6.1 |
| Storage temperature | −65 | 150 | °C | p. 4, §6.1 |
| Lead temperature (10 s soldering) | — | 300 | °C | p. 4, §6.1 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 4, §6.2 |
| ESD, CDM (JESD22-C101) | — | ±1000 | V | p. 4, §6.2 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Input voltage VIN | 1.6 | — | 5.5 | V | SLVSEN5B p. 4, §6.3 |
| Output voltage VOUT | 0 | — | 5.5 | V | p. 4, §6.3 |
| ON high level VIH | 1 | — | 5.5 | V | p. 4, §6.3 |
| ON low level VIL | 0 | — | 0.35 | V | p. 4, §6.3 |
| Ambient temperature TA | −40 | — | 105 | °C | p. 4, §6.3 |
| RON, VIN = 5 V, 25 °C (−40…125 °C max) | — | 89 | 125 (200) | mΩ | p. 5, §6.5 |
| RON, VIN = 3.6 V, 25 °C (−40…125 °C max) | — | 90 | 150 (250) | mΩ | p. 5, §6.5 |
| RON, VIN = 1.8 V, 25 °C (−40…125 °C max) | — | 105 | 300 (500) | mΩ | p. 5, §6.5 |
| Short-circuit limit, VOUT ≤ VIN − 1.5 V | — | 3 | — | A | p. 5, §6.5 |
| Short-circuit limit, VOUT ≤ VSC (hard short) | 30 | 500 | 900 | mA | p. 5, §6.5 |
| Hard-short threshold VSC (VIN − VOUT) | 0.3 | 0.36 | 0.46 | V | p. 5, §6.5 |
| Short response time tSC | — | 2 | — | µs | p. 5, §6.5 |
| Thermal shutdown, rising / falling | — | 180 / 145 | — | °C | p. 5, §6.5 |

Thermal (DCK, p. 4, §6.4): RθJA 210.7 °C/W, RθJC(top) 142.0 °C/W, RθJB 69.0 °C/W, ΨJB 68.8 °C/W. The orderable TPS22919DCKR is listed for −40 to 105 °C (p. 20, Package Option Addendum; the `.A` suffix is listed to 125 °C).

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Off (shutdown) | VON ≤ VIL, VOUT = GND, 25 °C | 2 | 20 | nA | SLVSEN5B p. 5, §6.5 |
| Off (shutdown) | −40…125 °C | — | 800 | nA | p. 5, §6.5 |
| On (quiescent) | VON ≥ VIH, VOUT open, 25 °C | 8 | 15 | µA | p. 5, §6.5 |
| On (quiescent) | −40…125 °C | — | 20 | µA | p. 5, §6.5 |
| ON pin leakage | VON ≥ VIH | — | 100 | nA | p. 5, §6.5 |

Conduction loss is I² × RON (for example 1.5 A at 90 mΩ = 0.20 W; calculation).

## Pinout and package

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | IN | I | Switch input |
| 2 | GND | — | Ground |
| 3 | ON | I | Active-high control; do not leave floating |
| 4 | NC | — | No connect; leave floating |
| 5 | QOD | O | Quick output discharge: tie to VOUT (internal 24 Ω), through RQOD to VOUT, or leave open to disable |
| 6 | VOUT | O | Switch output |

Source: SLVSEN5B p. 3, §5. Marking 1CS, MSL 1 at 260 °C, Sn finish (p. 20). SOT/SC-70, 1.1 mm maximum height (p. 24, DCK0006A). Tape 8 mm, 4 mm pitch, pin 1 in Q3, 3000 per reel (p. 22).

## Recommended footprint

TI example board layout DCK0006A (SLVSEN5B p. 25): six pads 0.9 × 0.4 mm, pitch 0.65 mm, 2.2 mm between pad-row centres, corner radius 0.05 mm. The example stencil (p. 26) keeps the same 0.9 × 0.4 mm openings for a 0.125 mm stencil. Layout example: Figure 32 (p. 18).

## Application circuit and required passives

- Input capacitor: 1 µF is sufficient in most cases; more bulk if the source is slow (SLVSEN5B p. 17, §10).
- Output: no capacitor required by the device; the load capacitance sets inrush. Inrush ≈ slew rate × CL (p. 16, §9.2.2.1, Equation 3). With the typical slew of 2.7 mV/µs at 3.6 V (p. 5, §6.6), 10 µF draws about 27 mA (calculation).
- QOD: tie QOD to VOUT for the fastest discharge, or add RQOD in series; fall time tFALL = 2.2 × (RDIS ∥ RL) × CL with RDIS = 24 Ω + RQOD (p. 14, §8.3.3, Equations 1–2). Example: CL = 10 µF, QOD shorted, 0.4 ms (p. 6, §6.6).
- No other external parts are needed (p. 12, §8.1).

## Interfaces and timing

| Parameter | Conditions | Typ | Unit | Source |
|---|---|---|---|---|
| Turn-on time tON | VIN = 5.0 / 3.6 / 1.8 V, CL = 0.1 µF, RL = 100 Ω | 1950 / 1750 / 1500 | µs | SLVSEN5B p. 5, §6.6 |
| Output rise time tR | VIN = 5.0 / 3.6 / 1.8 V | 1280 / 1100 / 750 | µs | p. 5, §6.6 |
| Turn-on slew rate | VIN = 5.0 / 3.6 / 1.8 V | 3.2 / 2.7 / 1.8 | mV/µs | p. 5, §6.6 |
| Turn-off time tOFF | VIN = 1.8–5.0 V | 6 | µs | p. 5, §6.6 |
| Fall time | CL = 10 µF, QOD shorted, RL open | 0.4 | ms | p. 6, §6.6 |

ON logic: VIH ≥ 1 V, VIL ≤ 0.35 V (p. 4), so 1.8 V and 3.3 V GPIOs drive it directly. While ON is below VIL a 530 kΩ smart pull-down holds it low; it disconnects once ON is driven above VIH (p. 13, §8.3.1, Table 1).

## Linux driver

None for the device. Each switched rail is a `regulator-fixed` node with `gpio` (or a TCA6416A line) and `enable-active-high`; `startup-delay-us` should cover tON (about 2 ms at 5 V). The DT modelling is OpenDAP's design, not a datasheet statement.

## Simulation models

No model is listed in `manifest.toml`. A TI PSpice or TINA model is **UNVERIFIED** (not checked).

## Design notes for the T1

- **1.8 V rails (DAC_DIG_1V8, FP_1V8, MIC_1V8, RP_IOVDD_1V8):** VIN = 1.8 V is inside the 1.6 V minimum, but RON rises to 105 mΩ typ / 300 mΩ max at 25 °C and 500 mΩ max at 125 °C (p. 5). At 13 mA (DAC_DIG_1V8, power tree §3) the drop is under 7 mV even at 500 mΩ (calculation).
- **DAC_VP from VSYS (3.5–4.4 V):** inside the 5.5 V operating limit. VP must be first on and last off for the CS43198 (power tree §6.2); the 1.5–2 ms tON delays VP, so the sequence must wait for it before enabling the other DAC rails.
- **Default off:** the smart pull-down keeps ON low only while ON is below VIL and is weak (530 kΩ). Keep an external pull-down on each enable net so the default state in power tree §5 holds when the driving GPIO or expander is in reset.
- **QOD:** power tree §5 assumes QOD active on every switch; tie QOD to VOUT (or through RQOD) in the schematic, otherwise the output floats when off (p. 14, Table 2).
- **Back-powering:** the datasheet does not state reverse-current blocking. Any rail fed back through IO pins of a powered-off block (I2S into the DAC, faceplate IO) must be parked low before the switch opens, as power tree §5 already requires. Reverse-current behaviour is **UNVERIFIED**.
- **Temperature grade:** TPS22919DCKR is listed at −40 to 105 °C operating (p. 20); the T1 internal temperature has not been modelled (power tree risk 10).

## Sources

- TI, TPS22919 datasheet, SLVSEN5B, revised May 2019 (package addendum dated 10 November 2025, packing data 3 July 2026), <https://www.ti.com/lit/ds/symlink/tps22919.pdf>, sha256 `743c59b01fb0891d2d0f1faba779161cd2d2b6c18edf68e6d5b3279016240c84` (manifest). Page numbers are PDF page numbers.
- OpenDAP board BOM v1 line 50 and power tree v0 §3, §5, §6 (T1 context).
