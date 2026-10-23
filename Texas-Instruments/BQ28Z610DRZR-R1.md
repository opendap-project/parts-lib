# BQ28Z610DRZR-R1

- **Manufacturer:** Texas Instruments
- **Function:** Impedance Track gas gauge and protection controller for 1- to 2-series Li-ion packs, with high-side N-FET drive, internal cell balancing and an I2C interface
- **BOM v1 lines:** 42 (Power, fuel gauge for the two-cell pack, gauge only, qty 1; BOM v1.5, board ADR 0014, replaces the [MAX17055EWL+T](../Analog-Devices/MAX17055EWL-T.md)); sense resistor on line 43 ([WSL12065L000FEA](../Vishay/WSL12065L000FEA.md)); board NTC on line 48
- **Package:** SON-12 (DRZ) with exposed pad, 2.5 × 4 mm (body size from the LCSC listing; TI outline on SLUSE07B p. 35)
- **Datasheet:** *BQ28Z610-R1 Impedance Track Gas Gauge and Protection Solution for 1-Series to 2-Series Cell Li-Ion Battery Packs*, SLUSE07B, January 2020, revised January 2022, 39 pages. Cited below as "SLUSE07B". File sha256 `d7506515380a903d0e911d3ce523f950c409848f7f1523874db5379d981c4da0`.
  - Firmware configuration (data flash, gauge-only use): *BQ28Z610-R1 Technical Reference Manual*, SLUUC81 (named on SLUSE07B p. 23): not read, **UNVERIFIED**.
- **Status:** Partly UNVERIFIED

## Summary

The BQ28Z610-R1 is a 1–2S pack-side gas gauge with Impedance Track gauging, primary protection through two high-side N-channel FET drivers (CHG, DSG), internal cell balancing, SHA-1 authentication, a broadcast mode for autonomous charger control and an I2C interface; it supports sense resistors down to 1 mΩ (SLUSE07B, p. 1). In the T1 it gauges the two-cell pack from the board side: the pack carries its own PCM and balancing (board ADR 0014 item 2), so the CHG/DSG drives are unused and the part works as a gauge only. VC2 sees BAT+ and VC1 the mid-cell tap through the battery connector, so both cell voltages are measured (board BOM v1.5 line 42).

## Absolute maximum ratings

SLUSE07B, p. 4, §7.1.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VC2, PBI (supply) | −0.3 | 30 | V |
| PACK | −0.3 | 30 | V |
| TS | −0.3 | VREG + 0.3 | V |
| SRP, SRN | −0.3 | VREG + 0.3 | V |
| VC2 | VC1 − 0.3 | VC1 + 8.5 or VSS + 30 | V |
| VC1 | VSS − 0.3 | VSS + 8.5 or VSS + 30 | V |
| SDA, SCL | −0.3 | 6 | V |
| CHG, DSG output | −0.3 | 32 | V |
| VSS current | | ±50 | mA |
| Functional temperature | −40 | 110 | °C |
| Storage temperature | −65 | 150 | °C |

ESD (SLUSE07B, p. 4, §7.2): HBM ±2000 V; CDM ±500 V.

## Recommended operating conditions

SLUSE07B, p. 4, §7.3, and pp. 5–8.

| Parameter | Min | Typ | Max | Unit |
|---|---|---|---|---|
| Supply VCC (VC2, PBI) | 2.2 | | 26 | V |
| Shutdown voltage (VPACK falling) | 1.8 | 2.0 | 2.2 | V |
| Start-up voltage (VPACK rising) | 2.05 | 2.25 | 2.45 | V |
| SDA, SCL input | | | 5.5 | V |
| SRP, SRN input | −0.2 | | 0.2 | V |
| VC2 input (relative to VC1); VC1 (relative to VSS) | 0 | | 5 | V |
| PACK input | | | 26 | V |
| CHG, DSG output | | | 26 | V |
| External PBI capacitor | 2.2 | | | µF |
| Operating temperature | −40 | | 85 | °C |
| Internal LDO VREG | 1.6 | 1.8 | 2.0 | V |

- Coulomb counter input range ±100 mV, 16-bit, offset ±2.6 LSB max after calibration (SLUSE07B, p. 7, §7.11).
- Cell balancing: internal bypass FET ≤ 200 Ω at 2 V < VDS < 4 V (SLUSE07B, p. 8, §7.14).
- Thermal (SLUSE07B, p. 5, §7.4): RθJA 186.4 °C/W (high-K), RθJC(top) 90.4 °C/W, RθJB 110.7 °C/W.

## Power by mode

SLUSE07B, p. 5, §7.5 (TA 25 °C, VCC 7.2 V; depends on the firmware configuration).

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| NORMAL | CHG and DSG on, no flash write | 250 | | µA |
| SLEEP | CHG and DSG off, no bus traffic | 100 | | µA |
| SHUTDOWN | | 0.5 | 2 | µA |

Flash writes draw up to 5 mA, erase up to 15 mA (SLUSE07B, p. 9, §7.21).

## Pinout and package

SLUSE07B, p. 3, Figure 6-1 and Table 6-1.

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | VSS | P | Ground |
| 2 | SRN | AI | Coulomb counter input, bottom of the sense resistor |
| 3 | SRP | AI | Coulomb counter input, top of the sense resistor |
| 4 | TS1 | AI | External temperature input (or BTP output) |
| 5 | SCL | I/O | I2C clock, external pull-up |
| 6 | SDA | I/O | I2C data, external pull-up |
| 7 | DSG | O | High-side N-FET drive |
| 8 | PACK | AI, P | Pack sense input |
| 9 | CHG | O | High-side N-FET drive |
| 10 | PBI | P | Power supply backup input |
| 11 | VC2 | AI, P | Top cell sense and balancing; primary supply and stack measurement (BAT) |
| 12 | VC1 | AI | Bottom cell sense and balancing |
| — | PWPD | — | Exposed pad, connected to VSS by an external trace |

Ordering (SLUSE07B, package option addendum, p. 30): BQ28Z610DRZR-R1, 3000 per large reel, NiPdAu, MSL 2 at 260 °C (1 year), −40 to 85 °C, marking 28Z6. BQ28Z610DRZT-R1 is the 250-piece reel.

## Recommended footprint

TI outline, example land pattern and stencil for DRZ: SLUSE07B, pp. 35–37. Not transcribed here: **UNVERIFIED** until the footprint is drawn against those pages. Layout guidance on p. 27: the 0.1 µF SRP/SRN filter capacitors near the pins (p. 23 note).

## Application circuit and required passives

SLUSE07B, p. 23, Figure 9-1 (2S typical implementation, with protection FETs and fuse):

- SRP and SRN through 100 Ω each with 0.1 µF filter capacitors near the pins; sense resistor 1–3 mΩ in Figure 9-1 (the p. 1 simplified schematic shows 1–10 mΩ).
- VC1, VC2 cell inputs through 100 Ω with 0.1 µF; PBI 2.2 µF; TS1 to a 10 kΩ NTC; SCL and SDA through 100 Ω with MM3Z5V6C Zener clamps.
- CHG and DSG to two N-FETs, with a 2N7002K, 10 MΩ and 10 kΩ network around them.

The T1 drops the FETs and the fuse driver (protection in the pack); how PACK and PBI are tied without FETs comes from SLUUC81, not read (**UNVERIFIED**).

## Interfaces and timing

- I2C, 400 kHz (SLUSE07B, p. 1). VIH = 0.7 × VREG and VIL = 0.3 × VREG (SLUSE07B, p. 12, §7.26); with VREG 1.6–2.0 V (p. 6, §7.9), VIH is 1.12–1.40 V, so a 1.8 V pull-up works without translation. Timing: tLOW ≥ 1.3 µs, tHIGH ≥ 600 ns, rise and fall ≤ 300 ns (p. 12, §7.27).
- I2C address: not stated in SLUSE07B. The mainline binding uses the 7-bit address 0x55 (board [2S pre-freeze note](https://github.com/opendap-project/board/blob/main/docs/research/2026-10-battery-2s-prefreeze.md)).
- Power-on reset at VREG 1.51 / 1.55 / 1.59 V falling, 300 µs typical reset time (SLUSE07B, p. 6, §7.8).

## Linux driver

Mainline `drivers/power/supply/bq27xxx_battery_i2c.c` binds `ti,bq28z610` (board 2S study §3.3). Debian sets `BATTERY_BQ27XXX=m`, but `BATTERY_BQ27XXX_I2C` is explicitly not set and arm64 does not override it (board 2S pre-freeze note): the I2C front end ships through DKMS (board ADR 0014, blackbird-os OS-023).

## Simulation models

None in the datasheet. Configuration is done with TI Battery Management Studio (BQSTUDIO) and a "golden image" per pack (SLUSE07B, p. 23). No manifest entry beyond the datasheet.

## Design notes for the T1

- **Gauge only.** Protection and balancing sit in the quoted pack (board ADR 0014 item 2); the board adds a 5 A fuse and relies on the BQ25798 IBAT_OCP (9.3 A minimum). The board 2S study §3.2 lists the full board-side option (BQ28Z610-R1 with FETs plus a BQ29209) if a pack without PCM is ever considered; it is not the adopted design.
- **Sense resistor:** 5 mΩ (board BOM line 43): 12 mV at 2.4 A, 20 A full scale on the ±100 mV counter.
- **Temperature:** TS1 takes the board NTC (board BOM line 48); the pack NTC goes to the charger TS.
- **Configuration per pack:** chemistry ID and design capacity in data flash; cell balancing in the gauge can stay disabled while the pack balances itself (configuration bit per SLUSE07B p. 25).
- **Quiescent cost:** 250 µA in NORMAL at 7.4 V ≈ 1.9 mW; 100 µA in SLEEP ≈ 0.74 mW (board 2S study §4.3).

## Sources

- TI, BQ28Z610-R1 datasheet, SLUSE07B (January 2022): <https://www.ti.com/lit/ds/symlink/bq28z610-r1.pdf>
- OpenDAP board ADR 0014 and BOM v1.5, lines 42–43, 48; board 2S battery study §3.2–§3.3, §4.3 (`public/board/docs/`).
