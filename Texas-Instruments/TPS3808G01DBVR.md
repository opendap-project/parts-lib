# TPS3808G01DBVR

- **Manufacturer:** Texas Instruments
- **Function:** Low-quiescent-current voltage supervisor with adjustable threshold (0.405 V SENSE reference), programmable reset delay and manual reset
- **BOM v1 lines:** 97 (MaskROM combo boot-window supervisor, qty 1; BOM v1.6, replaces the [TPS3839G18DBZR](TPS3839G18DBZR.md))
- **Package:** SOT-23-6 (DBV)
- **Datasheet:** *TPS3808 Low-Quiescent-Current, Programmable-Delay Supervisory Circuit*, SBVS050N, May 2004, revised August 2026. Cited below as "SBVS050N". File sha256 `74d889c0f68af88032f1633c26381817cc03e10d9fd3b4c177a044ad3ed86eed` (the copy read by the board boost and MaskROM simulation).
- **Status:** Partly UNVERIFIED

## Summary

The TPS3808 asserts an open-drain RESET when SENSE falls below its threshold or MR is pulled low, and holds it for a delay set by the CT pin: 20 ms (open), 300 ms (resistor to VDD) or 1.25 ms to 10 s with a capacitor (SBVS050N, p. 1). The G01 version has an adjustable threshold, 0.405 V at SENSE (Table 4-1, p. 3). In the T1 its RESET delay is the MaskROM entry window: while RESET is low after vcca1v8_pmu rises, holding Main + Volume − pulls eMMC_D0 low (board BOM lines 35, 97, 98).

## Absolute maximum ratings

SBVS050N, p. 5, §6.1: VDD −0.3 to 7 V; CT −0.3 to VDD + 0.3 V; RESET, MR, SENSE −0.3 to 7 V; RESET current ±5 mA.

## Recommended operating conditions

SBVS050N, p. 5, §6.3 and p. 6: VDD 1.7–6.5 V (−40 to 125 °C; 1.65 V from 0 to 85 °C); SENSE, MR, RESET 0–6.5 V; CT ≤ VDD; RESET current 0.0003–5 mA.

## Power by mode

SBVS050N, p. 6: supply current 2.4 µA typ, 5 µA max at VDD 3.3 V; 2.7 / 6 µA at 6.5 V (RESET not asserted).

## Pinout and package

SBVS050N, p. 4, Table 5-1 (SOT-23).

| Pin | Name | Function |
|---|---|---|
| 1 | RESET | Open-drain reset output; 10 kΩ–1 MΩ pull-up |
| 2 | GND | Ground |
| 3 | MR | Manual reset, active low; internal 70–90 kΩ pull-up to VDD |
| 4 | CT | Delay programming: open, resistor to VDD, or capacitor ≥ 100 pF to GND |
| 5 | SENSE | Monitored voltage input |
| 6 | VDD | Supply; 0.1 µF bypass |

Ordering (addendum, p. 19): TPS3808G01DBVR, 3000 per reel, MSL 1 at 260 °C, −40 to 125 °C, marking AVW.

## Recommended footprint

TI DBV (SOT-23-6) land pattern in the SBVS050N mechanical pages: not transcribed, **UNVERIFIED** until drawn.

## Application circuit and required passives

T1 values (board boost and MaskROM simulation §5.6): VDD and SENSE on vcca1v8_pmu; SENSE divider 280 kΩ / 100 kΩ (1 %) → trip at 0.405 V × 3.8 = 1.54 V; CT 390 nF X7R ±10 %; RESET pull-up 100 kΩ to vcca1v8_pmu; MR open; 0.1 µF on VDD.

## Interfaces and timing

- VIT (G01) 0.405 V, ±2 % with 1.5 % typ hysteresis; SENSE input current ±25 nA (p. 6).
- RESET delay (p. 7, §6.6): CT open 12 / 20 / 28 ms; CT to VDD 180 / 300 / 420 ms; CT 180 nF 0.62 / 1.03 / 1.44 s. CT (nF) = (td (s) − 0.5 ms) × 175 (Eq. 1). With 390 nF: 2.23 s typ, 1.21–3.43 s if the 180 nF spread scales with CT and the capacitor is ±10 % (**UNVERIFIED** that it scales).
- VOL 0.4 V at 1 mA (VDD ≥ 1.8 V); VPOR 0.8 V (p. 6).

## Linux driver

None. Its output gates the MaskROM logic (board BOM line 98).

## Simulation models

Behavioural model built from datasheet thresholds in the board MaskROM simulation (`public/board/sim/maskrom/`). No vendor model in the manifest.

## Design notes for the T1

- **Why it replaced the TPS3839** (board boost and MaskROM simulation §5): the TPS3839 window (120–350 ms on vcc_1v8) could not be shown to cover the BootROM's eMMC attempt and reopened at every resume, because vcc_1v8 is off in suspend. vcca1v8_pmu stays on in suspend, so the window opens only at a cold power-on (simulated: D0 held 1.20–3.42 s after RESETB, nothing at resume).
- **Supply margin:** VDD minimum is 1.7 V over −40 to 125 °C; vcca1v8_pmu at −5 % is 1.71 V.
- **Consequence:** MaskROM through the buttons needs a full power-off and an empty or unbootable SD slot.
- **Stock (2026-10-22):** Arrow 3,000 (Europe), Verical 1,332, LCSC C19653 471 @ $0.42, Mouser 0: thin.

## Sources

- TI, TPS3808 datasheet SBVS050N (August 2026): <https://www.ti.com/lit/ds/symlink/tps3808.pdf>
- OpenDAP board BOM v1.6, lines 35, 78, 97, 98; boost and MaskROM simulation §5 (`public/board/docs/`).
