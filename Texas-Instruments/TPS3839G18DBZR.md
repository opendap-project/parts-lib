# TPS3839G18DBZR

- **Manufacturer:** Texas Instruments
- **Function:** Ultralow-power supply voltage supervisor, 1.67 V threshold, push-pull active-low RESET, 200 ms typical reset delay
- **BOM v1 lines:** 97 (MaskROM combo power-on window supervisor)
- **Package:** SOT-23-3 (DBZ)
- **Datasheet:** TPS3831, TPS3839, SBVS193D (June 2012, revised July 2015), sha256 `a18940237afc…` in `manifest.toml`
- **Status:** Partly UNVERIFIED

## Summary

The TPS3839 monitors its own supply pin VDD and holds an active-low push-pull RESET output low while VDD is below the threshold, and for the reset delay td (200 ms typical) after VDD rises above the threshold plus hysteresis. Supply current is 150 nA typical (SBVS193D §1, §3, §8.1, pp. 1, 11). The G18 option has a 1.67 V nominal falling threshold (§5, p. 4). In the T1 it senses VCCIO2 (vcc_1v8) and provides the WINDOW_N input of the MaskROM combo circuit: its output stays low during the reset delay after the rail rises, which defines the power-on window in which Power + Vol− can force MaskROM mode (BOM v1 line 97, ADR 0009).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Reference |
|---|---|---|---|---|
| Voltage, VDD and RESET | −0.3 | 7 | V | SBVS193D p. 6, §7.1 |
| Current, RESET pin | −10 | 10 | mA | p. 6 |
| Operating ambient temperature, TA | −40 | 85 | °C | p. 6 |
| Storage temperature | −65 | 150 | °C | p. 6 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 6, §7.2 |
| ESD, CDM (JESD22-C101) | — | ±500 | V | p. 6, §7.2 |

## Recommended operating conditions

| Parameter | Min | Max | Unit | Reference |
|---|---|---|---|---|
| Input supply voltage, VDD | 0.9 | 6.5 | V | p. 6, §7.3 |
| RESET pin voltage | 0 | 6.5 | V | p. 6 |
| RESET pin current | 0 | 8 | mA | p. 6 |

### Electrical characteristics (TA = −40 to 85 °C, 0.9 V < VDD < 6.5 V, C1 = 0.1 µF)

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| Minimum VDD for valid output, V(POR) | IOL = 1 µA | — | — | 0.6 | V | p. 7, §7.5 |
| Supply current, IDD | Output not connected | — | 150 | 500 | nA | p. 7 |
| RESET VOL | VDD 1.2–2.8 V, IOL = 0.5 mA | — | — | 0.4 | V | p. 7 |
| RESET VOH | VDD 1.2–3.3 V, IOH = −0.5 mA | VDD − 0.4 | — | — | V | p. 7 |
| Falling threshold, VIT− (G18) | — | 1.628 | 1.67 | 1.695 | V | p. 7 |
| Threshold accuracy | TA = 25 °C | — | ±1 % | — | — | p. 7 |
| Hysteresis, Vhys (G18) | — | — | 17 | — | mV | p. 7 |

### Timing (§7.6, p. 8)

| Parameter | Min | Typ | Max | Unit |
|---|---|---|---|---|
| RESET delay (power-up delay), td | 120 | 200 | 350 | ms |
| Propagation delay, VDD falling (power-down delay), tPD_VDD | — | 20 | — | µs |

Thermal (DBZ): RθJA 346.6 °C/W (p. 6, §7.4).

## Power by mode

| Mode | Condition | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|
| Average | Output not connected | 150 | 500 | nA | p. 7, §7.5 |
| DC between samples | — | ≈ 100 | — | nA | p. 14, §9.2.2.1 |
| During input sampling | ≈ 200 µs per sample | ≈ 15 | — | µA | p. 14, §9.2.2.1 |

Output load current adds to these figures when RESET drives a load.

## Pinout and package

DBZ pin numbers (Pin Functions, p. 5):

| Pin | Name | I/O | Description |
|---|---|---|---|
| 1 | GND | — | Ground |
| 2 | RESET | O | Active-low reset, push-pull; low while VDD < threshold and for td after VDD rises above it |
| 3 | VDD | I | Supply voltage, also the monitored voltage |

Outline DBZ0003A (drawing 4214838/F, p. 28): body 2.80–3.04 × 1.20–1.40 mm, lead span 2.10–2.64 mm, pitch 0.95 mm (1.9 mm between pins 1 and 2), leads 0.3–0.5 mm wide, 1.12 mm maximum height; JEDEC TO-236 reference. MSL Level-1-260C-UNLIM, NiPdAuAg, −40 to 85 °C, reel 3000 (p. 20).

## Recommended footprint

DBZ0003A example board layout (p. 29, drawing 4214838/F, scale 15:1): 3 pads 1.3 × 0.6 mm (reference); pins 1 and 2 at 2 × 0.95 mm pitch; pin 3 opposite at 2.1 mm between pad-column centres (reference); non-solder-mask-defined preferred, 0.07 mm maximum mask clearance. Stencil on p. 30.

## Application circuit and required passives

- 0.1 µF bypass capacitor near VDD when the supply path has significant impedance, so the ≈ 15 µA sampling pulses do not cause a false reset (§9.2.2.1, p. 14; §11.1, p. 15). The electrical characteristics are specified with C1 = 0.1 µF (p. 7).
- Low-impedance VDD connection able to carry 15 µA without significant drop (§10, §11.1, p. 15).
- When RESET drives a bidirectional pin, add a series resistor (Figure 16 shows 47 kΩ, §9.2.2.2, p. 14). Not needed for the NOR input in the T1.

## Interfaces and timing

Behaviour by VDD (§8.4, p. 12; Figure 1, p. 8):

| VDD | RESET |
|---|---|
| < V(POR) (0.6 V max) | Undefined |
| V(POR) to VDD(min) | Low |
| Rising above VIT− + Vhys | Low for td (120–350 ms), then high |
| Falling below VIT− | Low after tPD_VDD (≈ 20 µs) |

The device ignores fast VDD transients; the trigger boundary of amplitude versus duration is Figure 13 (p. 12).

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. The datasheet states that TI provides SPICE models for the TPS3831 and TPS3839 in the product folders (§12.1.1.2, p. 16); the model file has not been downloaded (**UNVERIFIED** URL and licence).

## Design notes for the T1

- **Window length.** The window is td: 120 ms minimum, 200 ms typical, 350 ms maximum (p. 8), not a fixed 200 ms. BOM v1 already marks the match against the RK3566 BootROM timing as **UNVERIFIED**. The combo must work for any td in 120–350 ms: the BootROM must sample eMMC_D0 while WINDOW_N is still low at td = 120 ms, and holding D0 low until td = 350 ms must not hang a normal boot.
- **Threshold against the 1.8 V rail.** The rising threshold is VIT− + Vhys ≈ 1.687 V typical; VIT− can be up to 1.695 V (p. 7). vcc_1v8 must settle above about 1.72 V (≈ −4.5 % of 1.8 V) for the window to close reliably. The RK809 output tolerance on that rail is **UNVERIFIED** here; a rail sagging near 1.70 V under load could re-open the window (reset asserted again after ≈ 20 µs, p. 8).
- **Supply is the sensed rail.** The TPS3839 has no separate sense input: VDD is both supply and monitored voltage (p. 5). RESET swings to vcc_1v8, while the NOR gate (SN74LVC1G27, line 98) runs from vcca1v8_pmu. Both are nominally 1.8 V, so the levels are compatible, but if vcca1v8_pmu is up while vcc_1v8 is still below 0.6 V, RESET is undefined (§8.4.3, p. 12). Because WINDOW_N is one input of a NOR, an undefined high only suppresses the trigger (fail-safe); an undefined low opens the window early, which is harmless only if Power and Vol− are not both pressed.
- **Temperature.** −40 to 85 °C (p. 6).

## Sources

- TI, *TPS383x 150-nA, Ultralow Power, Supply Voltage Monitor*, SBVS193D, revised July 2015, <https://www.ti.com/lit/ds/symlink/tps3839.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 97–98, ADR 0009 (referenced from the BOM)
