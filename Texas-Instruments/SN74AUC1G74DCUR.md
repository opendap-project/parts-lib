# SN74AUC1G74DCUR

- **Manufacturer:** Texas Instruments
- **Function:** Single positive-edge-triggered D-type flip-flop with clear and preset, AUC family, optimised for 1.65–1.95 V, 3.6 V-tolerant inputs, Ioff
- **BOM v1 lines:** none yet; board ADR 0019 adds a line "MCLK dividers", qty 2 (one divide-by-two per CS43198, from the 45.1584 / 49.152 MHz NSC5083D oscillators to 22.5792 / 24.576 MHz)
- **Package:** VSSOP-8 (DCU, DCU0008A), body 2.0 × 2.3 mm nominal, 3.0–3.2 mm over leads, 0.5 mm pitch, 0.9 mm max height
- **Datasheet:** *SN74AUC1G74 Single Positive-Edge-Triggered D-Type Flip-Flop With Clear and Preset*, SCES537D, December 2003, revised June 2007. Cited below as "SCES537D". File sha256 `78ef342668836a8c3bffdb203769e9e4404e1914badcff849016b7ff429445c6`.
- **Availability (2026-10-24):** Digi-Key 24,658 @ $0.62 (Active); Mouser 3,269 @ $0.27–0.62 (via FindChips); LCSC C2677720: 170 @ $0.43. Same die: SN74AUC1G74YZPR Digi-Key 2,905 @ $0.71, SN74AUC1G74RSER 812 @ $0.68; SN74AUC1G74DCTR is Last Time Buy. TI product page: Active.
- **Status:** Partly UNVERIFIED

## Summary

The SN74AUC1G74 is a single D flip-flop with active-low preset and clear, designed for 1.65–1.95 V and operational from 0.8 to 2.7 V; its inputs and outputs tolerate 3.6 V, and Ioff disables the outputs when unpowered (SCES537D, p. 1). In the T1 each CS43198 has one, wired as a divide-by-two (Q̅ to D, PRE high): the 45.1584 or 49.152 MHz oscillator clocks it, and Q drives the DAC's XTI/MCLK input at 22.5792 or 24.576 MHz. Because Q changes only on rising clock edges, the output duty cycle does not depend on the oscillator's symmetry; it depends only on tPHL − tPLH of this part (board ADR 0019).

## Absolute maximum ratings

SCES537D, p. 3.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| Supply voltage VCC | −0.5 | 3.6 | V |
| Input voltage VI | −0.5 | 3.6 | V |
| Voltage on an output, high-impedance or power-off | −0.5 | 3.6 | V |
| Output voltage | −0.5 | VCC + 0.5 | V |
| Input / output clamp current (V < 0) | | −50 | mA |
| Continuous output current | | ±20 | mA |
| Current through VCC or GND | | ±100 | mA |
| Storage temperature | −65 | 150 | °C |

θJA DCU 227 °C/W (JESD 51-7). ESD: 2000 V HBM, 200 V MM, 1000 V CDM; latch-up > 100 mA (JESD 78 Class II) (p. 1).

## Recommended operating conditions

SCES537D, p. 3.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VCC | | 0.8 | 2.7 | V |
| VIH | VCC 1.1–1.95 V | 0.65 × VCC | | V |
| VIL | VCC 1.1–1.95 V | | 0.35 × VCC | V |
| VI | | 0 | 3.6 | V |
| VO | | 0 | VCC | V |
| IOH / IOL | VCC 1.65 V | | −8 / 8 | mA |
| Input transition rate | VCC 1.65–2.3 V | | 20 | ns/V |
| TA | | −40 | 85 | °C |

All unused inputs must be held at VCC or GND (p. 3, note 1).

## Power by mode

| Mode | Value | Source |
|---|---|---|
| Static ICC | 10 µA max, VCC 0.8–2.7 V, IO = 0 | SCES537D p. 4 |
| Power dissipation capacitance Cpd | 44 pF typ at VCC 1.8 V, f = 10 MHz, 25 °C | SCES537D p. 5 |
| Ioff | ±10 µA max, VI or VO = 2.7 V, VCC = 0 | SCES537D p. 4 |

T1 estimate (board ADR 0019): Cpd × VCC × 49.152 MHz + 12.6 pF × VCC × 24.576 MHz ≈ 4.45 mA per part at 1.8 V (typical Cpd; not a datasheet figure).

## Pinout and package

DCU (VSSOP-8), top view (SCES537D, p. 1).

| Pin | Name | Function |
|---|---|---|
| 1 | CLK | Clock input, positive edge |
| 2 | D | Data input |
| 3 | Q̅ | Inverted output |
| 4 | GND | Ground |
| 5 | Q | Output |
| 6 | CLR̅ | Clear, active low (overrides PRE̅) |
| 7 | PRE̅ | Preset, active low |
| 8 | VCC | Supply |

DCU0008A (drawing 4225266/A): body 1.9–2.1 × 2.2–2.4 mm, 3.0–3.2 mm over leads, pitch 0.5 mm, lead width 0.17–0.25 mm, height 0.9 mm max, JEDEC MO-187 CA (SCES537D package pages). MSL 1 at 260 °C; marking U74_ (pp. 2, package option addendum).

## Recommended footprint

TI example board layout for DCU0008A (SCES537D package pages): eight pads of (0.85) × (0.3) mm, 0.5 mm pitch, (3.1) mm between pad-row outer edges, solder paste on a 0.125 mm stencil. Values in parentheses are reference values from the drawing. The KiCad footprint is to be generated to IPC-7351 from these dimensions in `kicad-lib` (**UNVERIFIED** until done).

## Application circuit and required passives

- Decoupling on VCC: value not stated in the datasheet (**UNVERIFIED**); the T1 uses 100 nF at pin 8.
- T1 divide-by-two (board ADR 0019): Q̅ (pin 3) to D (pin 2) directly; PRE̅ (pin 7) to VCC; CLR̅ (pin 6) to the shared `MCLK_DIV_RUN` line with a 100 kΩ pull-down; CLK (pin 1) on the oscillator net (100 kΩ pull-down there); Q (pin 5) through 27 Ω to the DAC's XTI/MCLK, ≤ 15 mm. VCC from MCLK_1V8 (TPS7A2018).
- Feedback timing at VCC 1.8 V ± 0.15 V: CLK → Q̅ minimum 0.9 ns against hold time 0.3 ns; maximum 1.5 ns plus setup time 0.5 ns against the 20.3 ns period at 49.152 MHz (SCES537D p. 4).

## Interfaces and timing

SCES537D, pp. 4–5, VCC 1.8 V ± 0.15 V, over temperature.

| Parameter | Min | Typ | Max | Unit |
|---|---|---|---|---|
| fclock (timing requirement) | | | 250 | MHz |
| tw, CLK high or low | 1 | | | ns |
| tw, PRE̅ or CLR̅ low | 1 | | | ns |
| tsu, data before CLK↑ | 0.5 | | | ns |
| tsu, PRE̅ or CLR̅ inactive before CLK↑ | 0.7 | | | ns |
| th, data after CLK↑ | 0.3 | | | ns |
| tpd CLK → Q, CL 15 pF | 1.0 | 1.2 | 1.7 | ns |
| tpd CLK → Q̅, CL 15 pF | 0.9 | 1.1 | 1.5 | ns |
| tpd PRE̅ or CLR̅ → Q or Q̅, CL 15 pF | 1.1 | 1.5 | 2.2 | ns |
| tpd CLK → Q, CL 30 pF | 1.5 | 1.9 | 2.4 | ns |
| tpd CLK → Q̅, CL 30 pF | 1.4 | 1.9 | 2.4 | ns |
| VOH, IOH −8 mA, VCC 1.65 V | 1.2 | | | V |
| VOL, IOL 8 mA, VCC 1.65 V | | | 0.45 | V |
| CI, VCC 2.5 V | | 2.5 | | pF |

tPLH and tPHL are the same as tpd (parameter measurement notes). No pulse skew, output impedance, additive jitter or supply sensitivity is published. The board bounds |tPHL − tPLH| ≤ 0.7 ns at CL 15 pF from the min–max spread above (board ADR 0019); that bound treats the two transitions as independent and is pessimistic.

## Linux driver

None. No digital interface; the divided clock appears to Linux as the CS43198's fixed MCLK (`fixed-clock` or `gpio-gate-clock`; board ADR 0019).

## Simulation models

TI offers an IBIS model for the AUC family (not downloaded, not in `manifest.toml`; **UNVERIFIED**). The board simulation `sim/mclk-divider` uses a behavioural source with tPHL − tPLH and an output resistance of 15 or 56 Ω (56 Ω from VOH at −8 mA, p. 4).

## Design notes for the T1

- **Duty cycle:** at 24.576 MHz the 0.7 ns bound gives 50 ± 1.7 %, at 22.5792 MHz 50 ± 1.6 %; the CS43198 needs 45–55 %. Simulated at XTI with every corner: 45.08–54.35 % (board ADR 0019).
- **Keep each output at or under 15 pF** (trace, pad, XTI): the 0.7 ns bound is from the 15 pF column; at 30 pF the spread is 0.9 ns.
- **Mixed voltage:** the 3.1 V oscillator drives CLK while VCC is 1.8 V; VI up to 3.6 V is allowed at any VCC (pp. 3). With VCC = 0 the Ioff limit is specified at 2.7 V only; the driver keeps the oscillators in standby unless MCLK_1V8 is up.
- **No other logic family found gives a comparable bound at 1.8 V:** SN74LVC1G74 spreads CLK → Q over 4.8–13.4 ns (SCES794G p. 7). The second source is the same die in YZP or RSE.
- **Two dividers on one clock** can start in opposite phase; CLR̅ held low until the clock is stopped and released before the oscillator starts makes the start deterministic unless the oscillator emits start-up runts (**UNVERIFIED**).

## Sources

- Texas Instruments, SN74AUC1G74 SCES537D: <https://www.ti.com/lit/ds/symlink/sn74auc1g74.pdf>
- Texas Instruments product page, read 2026-10-24: <https://www.ti.com/product/SN74AUC1G74>
- Distributor stock read 2026-10-24: Digi-Key search, FindChips, LCSC through the JLCPCB parts search.
- OpenDAP board ADR 0019 and `sim/mclk-divider`.
