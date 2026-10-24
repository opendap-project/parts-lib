# BQ28Z610DRZR-R1

- **Manufacturer:** Texas Instruments
- **Function:** Impedance Track gas gauge and protection controller for 1- to 2-series Li-ion packs, with high-side N-FET drive, internal cell balancing and an I2C interface
- **BOM v1 lines:** 42 (Power, fuel gauge for the two-cell pack, gauge only, qty 1; BOM v1.5, board ADR 0014, replaces the [MAX17055EWL+T](../Analog-Devices/MAX17055EWL-T.md)); sense resistor on line 43 (3 mΩ [WSL12063L000FEA](../Vishay/WSL12063L000FEA.md) from board ADR 0017, replacing the 5 mΩ [WSL12065L000FEA](../Vishay/WSL12065L000FEA.md)); board NTC on line 48; wiring, storage shutdown and production configuration decided in board ADR 0017 (2026-10-24)
- **Package:** SON-12 (DRZ) with exposed pad, 2.5 × 4 mm (body size from the LCSC listing; TI outline on SLUSE07B p. 35)
- **Datasheet:** *BQ28Z610-R1 Impedance Track Gas Gauge and Protection Solution for 1-Series to 2-Series Cell Li-Ion Battery Packs*, SLUSE07B, January 2020, revised January 2022, 39 pages. Cited below as "SLUSE07B". File sha256 `d7506515380a903d0e911d3ce523f950c409848f7f1523874db5379d981c4da0`.
  - Firmware configuration (data flash, gauge-only use): *BQ28Z610-R1 Technical Reference*, SLUUC81, January 2020 (no revision letter, no revision history), 127 pages, <https://www.ti.com/lit/ug/sluuc81/sluuc81.pdf>, sha256 `5663b323ede0ce095ff6d75ba83701b9d716eb22492e1f0f220a8fcfe2927bd9`. Cited below as "SLUUC81"; read 2026-10-24.
- **Status:** Partly UNVERIFIED (items marked below)

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

The T1 drops the FETs (protection in the pack). The part has no fuse output (SLUSE07B Table 6-1, p. 3; the permanent-fail actions only turn the FETs off, SLUUC81 §3.1, p. 16). Without FETs (SLUUC81 and SLUSE07B give no gauge-only circuit; items marked **UNVERIFIED** are not stated by TI):

- **CHG, DSG:** left open. Not in SLUUC81 or SLUSE07B; a TI engineer states "If you don't plan to use the protection FET features you can float CHG and DSG pins" ([E2E 903283](https://e2e.ti.com/support/power-management-group/power-management/f/power-management-forum/903283/bq28z610-r1-unused-pins); forum guidance, not a specification). With the drive off, CHG is discharged to VC2 and DSG to PACK internally (SLUSE07B §8.3.14, p. 19).
- **VC2:** the BAT terminal and primary supply ("this device does not have a BAT terminal", SLUSE07B p. 3; SLUUC81 §11.2, p. 53).
- **PBI:** 2.2 µF to VSS (CPBI, SLUSE07B §7.3, p. 4; §11.1, p. 27).
- **PACK:** pack sense and wake input, internal pull-down RPACK(PD) 30/40/50 kΩ (SLUSE07B §7.6, p. 5); whether the pull-down is connected permanently is not stated (**UNVERIFIED**, measure on the first board). Both shutdown paths need PACK < Charger Present Threshold (default 3000 mV): voltage-based (SLUUC81 §5.4.1, p. 27) and commanded, MAC 0x0010, sent twice when sealed, which trips on Current() = 0 and PACK < Charger Present (§12.2.10, p. 68). Wake from SHUTDOWN, with a full reset, needs VPACK > 2.05–2.45 V (SLUSE07B §7.3, p. 4). Tied to BAT+, PACK never falls below 3.0 V on a 2S stack, so the gauge would stay in SLEEP (100 µA typ) until the pack PCM opens. **T1 wiring (board ADR 0017): PACK on the switched side of the BQ25798 ship FET** (the charger BAT node), the place TI's circuits give PACK behind the switch that disconnects the cells (SLUSE07B p. 1 "Pack side / System side", Figure 9-1). VC2, PBI and VC1 stay on the pack side: VC2 must stay above VC1 − 0.3 V (§7.1, p. 4), which a switched VC2 with VC1 on the mid-cell tap would violate.
- **Storage sequence (board ADR 0017 item 3):** with no adapter, the host sends MAC 0x0010 twice, then writes the BQ25798 SDRV_CTRL = 01 (charger shutdown mode). The ship FET opens, PACK falls, the gauge enters SHUTDOWN; plugging an adapter closes the ship FET and wakes it. Pack drain in storage: gauge 0.5 / 2 µA, charger BATP 0.5 / 0.7 µA, ship FET ≤ 1 µA, PACK leakage ≤ 1 µA: ≈ 1 µA typical, 4.7 µA maximum (target ≤ 5 µA, ADR 0017 §1).

## Interfaces and timing

- I2C, 400 kHz (SLUSE07B, p. 1). VIH = 0.7 × VREG and VIL = 0.3 × VREG (SLUSE07B, p. 12, §7.26); with VREG 1.6–2.0 V (p. 6, §7.9), VIH is 1.12–1.40 V, so a 1.8 V pull-up works without translation. Timing: tLOW ≥ 1.3 µs, tHIGH ≥ 600 ns, rise and fall ≤ 300 ns (p. 12, §7.27).
- I2C address: 7-bit **0x55** (0xAA write, 0xAB read), SLUUC81 §12.1, p. 57. Up to 400 kHz needs I2C Configuration[XL] = 1 (default normal speed, SLUUC81 p. 90); clock stretching off by default (FLASH_BUSY_WAIT = 0, p. 90).
- Data flash is reached only through AltManufacturerAccess() (0x3E, block write with the little-endian address, 1–32 bytes; checksum and length at 0x60/0x61), SLUUC81 §12.2.45, pp. 84–85, p. 64. The part ships in FULL ACCESS; once SEALED, data flash is not accessible (SLUUC81 §9.5.3, p. 49). Default keys: not in SLUUC81, **UNVERIFIED**.
- Power-on reset at VREG 1.51 / 1.55 / 1.59 V falling, 300 µs typical reset time (SLUSE07B, p. 6, §7.8).

## Linux driver

Mainline `drivers/power/supply/bq27xxx_battery_i2c.c` binds `ti,bq28z610` (OF table) and `bq28z610` (I2C id); the binding `Documentation/devicetree/bindings/power/supply/bq27xxx.yaml` lists `ti,bq28z610` and sets `interrupts: false` for it (torvalds master `5b0764a53235`, read 2026-10-24). The driver only reads this chip: Temperature 0x06, Voltage 0x08, BatteryStatus 0x0A (FD bit 4, FC bit 5, bit 6), RemainingCapacity 0x10, FullChargeCapacity 0x12, AverageCurrent 0x14, time to empty and full 0x16/0x18, AveragePower 0x22, CycleCount 0x2A, RelativeStateOfCharge 0x2C, DesignCapacity 0x3C. Its data-memory table for the chip is `NULL` ("data memory update not supported for chip"), so it never writes data flash; XCHG/XDSG live in OperationStatus(), which it does not read, so FET_EN = 0 does not affect it. Device-tree node: `compatible = "ti,bq28z610"; reg = <0x55>;` on I2C1. Debian sets `BATTERY_BQ27XXX=m`, but `BATTERY_BQ27XXX_I2C` is explicitly not set and arm64 does not override it (board 2S pre-freeze note): the I2C front end ships through DKMS (board ADR 0014, blackbird-os OS-023).

## Gauge-only configuration (data flash)

SLUUC81 Table 14-1 (pp. 113–118) for addresses and defaults, §13 (pp. 88–106) for bits. Values in the "T1" column are derived from those bits for the T1 (gauge only, 2S, pack-side PCM and balancing); they go into the production golden image (SLUSE07B §9.1, p. 23), not into Linux.

| Setting (Class:Subclass) | Address | Default | T1 | Why (source) |
|---|---|---|---|---|
| Settings:Manufacturing:Mfg Status init | 0x43C0 | 0x0000 | **0x0008** (GAUGE_EN = 1; FET_EN = 0, PF_EN = 0; LF_EN optional, 0x0028) | Gauging is off by default; FET_EN = 0 keeps CHG and DSG off and forces ChargingVoltage() and ChargingCurrent() to 0 (SLUUC81 p. 94, §4.12 pp. 24–25, §6.1 p. 29). Takes effect after a reset or seal (§10.1, p. 50) |
| Settings:Configuration:I2C Configuration | 0x4602 | 0x01 | **0x00** (or 0x08 for 400 kHz) | BCAST = 1 by default makes the gauge broadcast to a smart charger as a bus master on the SoC bus (SLUUC81 p. 90) |
| Settings:Configuration:DA Configuration | 0x469B | 0x11 | **0x19** (CC0 = 1: 2 cells; SLEEP = 1; IN_SYSTEM_SLEEP = 1) | I2C1 stays pulled up while the T1 runs; without IN_SYSTEM_SLEEP a high bus keeps the gauge out of SLEEP (SLUUC81 §5.3.1–5.3.2, p. 26; p. 92; board ADR 0017) |
| Settings:Configuration:Balancing Configuration | 0x470A | 0x01 | **0x00** | CB = 0: no gauge balancing, the pack balances (SLUUC81 p. 92, §7.1 p. 39; SLUSE07B §9.2.2.1, pp. 24–25) |
| Settings:Protection:Enabled Protections A / B / D | 0x46AF / 0x46B0 / 0x46B2 | 0x57 / 0x35 / 0x0C | 0x40 / 0x05 / 0x00 | Firmware protections off (CUV, COV, OCC, OCD, OTC, OTD, UTC, UTD); reserved bits kept (SLUUC81 p. 93) |
| Settings:Protection:Enabled Protections C | 0x46B1 | 0x3C (p. 93) or 0x14 (p. 114) | **Read value with PTO (bit 2) and CTO (bit 4) cleared**: 0x14 → 0x00, 0x3C → 0x28 | The two defaults differ only in reserved bits 3 and 5; the production tool stops on any other read value (board ADR 0017 item 5) |
| Settings:Permanent Failure:Enabled PF A / B / C | 0x46FC–0x46FE | 0x00 | 0x00 | No PF actions (SLUUC81 p. 93) |
| Settings:Configuration:Temperature Enable | 0x469A | 0x03 | 0x03 | Internal sensor and TS1 (board NTC); clear TS1 if it is not fitted (SLUUC81 §2.7, p. 13) |
| Settings:AFE:AFE Protection Control | 0x469D | 0x70 (p. 114) or 0x00 (p. 94) | **RSNS = 0, SCDDx2 = 0; RSTRIM (bits 7–4) as read**, expected 0x7 → 0x70 | p. 94 itself says to leave RSTRIM at 0x7 ("unsupported" trim), matching 0x70; RSNS = 0 keeps the Table A-1 thresholds (board ADR 0017 item 5) |
| Settings:Configuration:IT Gauging Configuration | 0x464D | 0xD4DE (p. 92) or 0x14CE (p. 114) | **Functional bits 0x14CE** (TI defaults: CSYNC, RFACTSTEP, OCVFR, RSOC_CONV, FAST_QMax_LRN, FF_NEAR_EDV, SMOOTH); reserved bits 4, 14, 15 as read | The two defaults differ only in reserved bits (board ADR 0017 §3) |
| Settings:Configuration:Power Configuration | — | 0x00 | 0x00 (AUTO_SHIP_EN = 0) | Shutdown is commanded by the host (SLUUC81 p. 91) |
| Power:Shutdown: Shutdown Voltage, Shutdown Time, Charger Present Threshold | 0x460C, 0x460E, 0x460F | 2300 mV, 10 s, 3000 mV | Same, written explicitly | SLUUC81 p. 118 |
| Power:Ship: FET Off Time, Delay | 0x461B, 0x461C | 10 s, 20 s | Same, written explicitly | SLUUC81 p. 118 |
| Power:Sleep: Sleep Current, Bus Timeout | 0x4611, 0x4613 | 10 mA, 5 s | Same, written explicitly | 30 µV across 3 mΩ (SLUUC81 p. 118) |
| Protections:AOLD:Threshold | 0x469E | 0xF4 | 0xF4, written explicitly | Setting 4 (−19.42 mV, RSNS = 0) = 6.5 A at 3 mΩ, above the 5 A fuse (Table A-1, p. 123) |
| Calibration: CC Gain, Capacity Gain | 0x4006, 0x400A | 3.58422, 1069035.256 | Calibrated per board | §11.4.3 gain calibration at 1–2 A; Capacity Gain = CC Gain × 298261.6178 (SLUUC81 pp. 54–56). Which resistor the default represents: **UNVERIFIED** |
| Gas Gauging: Design Capacity mAh / cWh, Design Voltage, Qmax Cell 1/2/Pack, Device Chemistry | 0x462A, 0x462C, 0x462E, 0x4206–0x420A, 0x4095 | 4400, 6336, 7200, — , LION | Per quoted pack | Chemistry ID from BQSTUDIO (SLUUC81 §6.4.1 p. 33, pp. 117–118) |

- Hardware fault detectors AOLD, ASCC and ASCD have no enable bit (SLUUC81 pp. 93, 114); with no FETs they only set flags, but any SafetyAlert or AOLD/ASCC/ASCD flag prevents SLEEP (§5.3.1, p. 26). AOLD default (setting 4, −19.42 mV at RSNS = 0, Table A-1 p. 123) is 6.5 A across the 3 mΩ resistor, above the 5 A fuse and the 3.2 A worst case, so it stays at the default (board ADR 0017).
- Production rule for the three fields TI documents with two defaults (Enabled Protections C, AFE Protection Control, IT Gauging Configuration): read, check it is one of the two documented values (otherwise stop), write the T1 value, read back, log. The values read from the first device are to be recorded here (**UNVERIFIED** until then).
- Whether PF_EN = 0 also suppresses the instruction-flash checksum and data-flash write PFs (listed with no enable bit, SLUUC81 §3.7–3.8, p. 18): **UNVERIFIED**.
- No learning cycle is required to gauge (SLUSE07B §8.3.23, p. 20); Qmax updates need rests at dV/dt < 4 µV/s, 10–40 °C, ≥ 37 % capacity change (SLUUC81 §6.4.2, p. 33).

## Simulation models

None in the datasheet. Configuration is done with TI Battery Management Studio (BQSTUDIO) and a "golden image" per pack (SLUSE07B, p. 23). Manifest entries: the datasheet and SLUUC81.

## Design notes for the T1

- **Gauge only.** Protection and balancing sit in the quoted pack (board ADR 0014 item 2); the board adds a 5 A fuse and relies on the BQ25798 IBAT_OCP (9.3 A minimum). The board 2S study §3.2 lists the full board-side option (BQ28Z610-R1 with FETs plus a BQ29209) if a pack without PCM is ever considered; it is not the adopted design.
- **Sense resistor: 3 mΩ** (board ADR 0017; was 5 mΩ, outside the 1–3 mΩ SLUSE07B recommends in §8.4.2.3 p. 22, §11.1 p. 27 and Figure 9-1): Vishay WSL12063L000FEA. 9.6 mV and 31 mW at 3.2 A, ±33 A full scale; maximum offset ±2.6 LSB (≈ 3.05 µV per LSB, §7.11 p. 7) ≈ ±2.6 mA. Placement between the cell-stack negative and the pack negative (SLUUC81 §6.1, p. 29), SRP on the cell side; 100 Ω into SRP and SRN with 0.1 µF differential at the pins, Kelvin connections. The WSL1206 component TCR at 3 mΩ is ±150 ppm/°C, above the ≤ 50 ppm/°C guidance (§11.1): accepted, ±0.38 % over 25 K against a calibrated gain (ADR 0017 §2).
- **Temperature:** TS1 takes the board NTC (board BOM line 48): internal pull-up 14.4/18/21.6 kΩ, made for a 10 kΩ NTC such as the Semitec 103AT-2 between TS1 and VSS (SLUSE07B §7.16 p. 8, §8.3.8 p. 17). The pack NTC goes to the charger TS.
- **Configuration per pack:** the golden image of the table above, chemistry ID and design capacity per quoted pack, gauge balancing off (CB = 0), CC Gain calibrated per board in production.
- **Quiescent cost:** 250 µA in NORMAL at 7.4 V ≈ 1.9 mW; 100 µA in SLEEP ≈ 0.74 mW (board 2S study §4.3); 0.5 / 2 µA in SHUTDOWN, reached only through the storage sequence above.

## Sources

- TI, BQ28Z610-R1 datasheet, SLUSE07B (January 2022): <https://www.ti.com/lit/ds/symlink/bq28z610-r1.pdf>
- TI, BQ28Z610-R1 Technical Reference, SLUUC81 (January 2020): <https://www.ti.com/lit/ug/sluuc81/sluuc81.pdf>
- TI E2E thread 903283 (unused pins): <https://e2e.ti.com/support/power-management-group/power-management/f/power-management-forum/903283/bq28z610-r1-unused-pins>
- Linux (torvalds master `5b0764a53235`): `drivers/power/supply/bq27xxx_battery.c`, `bq27xxx_battery_i2c.c`, `Documentation/devicetree/bindings/power/supply/bq27xxx.yaml`
- OpenDAP board ADR 0014, ADR 0017 (gauge wiring, sense resistor and production configuration) and BOM v1.5, lines 42–43, 48; board 2S battery study §3.2–§3.3, §4.3 (`public/board/docs/`).
