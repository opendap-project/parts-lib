# AT24C02D-STUM-T

- **Manufacturer:** Microchip
- **Function:** 2-kbit (256 × 8) I²C serial EEPROM
- **BOM v1 lines:** 17 (board-ID / calibration EEPROM, 2 kbit), Core
- **Package:** 5-lead SOT23 (5TS1), matte-tin finish
- **Datasheet:** Atmel *AT24C01D and AT24C02D I2C-Compatible (2-wire) Serial EEPROM*, Atmel-8871F, 01/2017, 26 pages. Copy read from the LCSC mirror of part C79996: <https://datasheet.lcsc.com/datasheet/pdf/c29e4cc385dd45a5834baf0ecd97c09b.pdf>, sha256 `397ff061aa7a4ae36864592813831e9386e9467f10049064d7f139f26be6475e`. Cited below as "8871F".
  - The Microchip re-issue listed in `manifest.toml` (DS20006064) returned HTTP 403 from this host and was not read. Values below are from Atmel 8871F; differences in DS20006064 are **UNVERIFIED**.
- **Status:** Partly UNVERIFIED

## Summary

The AT24C02D is a 2-kbit (256 × 8) I²C serial EEPROM for 1.7–3.6 V with an 8-byte page and a write-protect pin (8871F, p. 1). The -STUM-T ordering code is the 5-lead SOT23 (5TS1) package, matte-tin finish, 1.7–3.6 V, industrial temperature range, tape and reel (8871F, pp. 16–17). In the T1 it holds the board revision, serial number and headphone-output trim on I2C2 (1.8 V, PMUIO2), BOM v1 line 17.

## Absolute maximum ratings

8871F, p. 13, §8.1:

| Parameter | Min | Max | Unit |
|---|---|---|---|
| Supply voltage to ground | −0.5 | 4.10 | V |
| Voltage on any pin to ground | −0.6 | VCC + 0.5 | V |
| DC output current | — | 5.0 | mA |
| Temperature under bias | −55 | +125 | °C |
| Storage temperature | −65 | +150 | °C |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|
| VCC | 1.7 | — | 3.6 | V | 8871F, p. 13, Table 8-1 / 8-2 |
| Operating temperature (case) | −40 | — | +85 | °C | 8871F, p. 13, Table 8-1 |
| VIL | −0.6 | — | 0.3 × VCC | V | 8871F, p. 13, Table 8-2 |
| VIH | 0.7 × VCC | — | VCC + 0.5 | V | 8871F, p. 13, Table 8-2 |
| VOL at VCC = 1.7 V, IOL = 0.15 mA | — | — | 0.2 | V | 8871F, p. 13, Table 8-2 |
| VOL at VCC = 3.0 V, IOL = 2.1 mA | — | — | 0.4 | V | 8871F, p. 13, Table 8-2 |
| Input / output leakage | — | 0.10 / 0.05 | 3.0 | µA | 8871F, p. 13, Table 8-2 |
| SDA capacitance | — | — | 8 | pF | 8871F, p. 15, Table 8-4 |
| Input capacitance (A0–A2, SCL) | — | — | 6 | pF | 8871F, p. 15, Table 8-4 |
| VCC rise slew rate | — | — | 0.1 | V/µs | 8871F, p. 15, §8.6 |
| tPUP, VCC stable to first command | 100 | — | — | µs | 8871F, p. 15, Table 8-5 |
| VPOR, power-on reset threshold | — | — | 1.5 | V | 8871F, p. 15, Table 8-5 |
| tPOFF, minimum time at 0 V between power cycles | 1 | — | — | ms | 8871F, p. 15, Table 8-5 |

## Power by mode

8871F, p. 13, Table 8-2:

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Read (ICC1) | VCC = 1.8 V, 400 kHz | 0.08 | 0.3 | mA |
| Read (ICC1) | VCC = 3.6 V, 1 MHz | 0.15 | 0.5 | mA |
| Write (ICC2) | VCC = 3.6 V, 1 MHz | 0.20 | 1.0 | mA |
| Standby (ISB) | VCC = 1.8 V | 0.08 | 0.4 | µA |
| Standby (ISB) | VCC = 3.6 V | 0.10 | 0.8 | µA |

Endurance 1,000,000 write cycles at 25 °C; data retention 100 years at 55 °C (8871F, p. 15, Table 8-6).

## Pinout and package

5-lead SOT23, top view (8871F, p. 2, pinout figure):

| Pin | Name | Function (8871F, p. 2, Table 1-1) |
|---|---|---|
| 1 | SCL | Serial clock input |
| 2 | GND | Ground |
| 3 | SDA | Open-drain data I/O; external pull-up required, not above 10 kΩ |
| 4 | VCC | Supply |
| 5 | WP | Write protect, active high; internal pull-down when floating |

Package 5TS1: body D = 2.90 mm BSC × E1 = 1.60 mm BSC, E = 2.80 mm BSC, pitch e = 0.95 mm, e1 = 1.90 mm, lead width b = 0.30–0.50 mm, height A ≤ 1.00 mm; JEDEC MO-193 variation AB (8871F, p. 23, drawing 5TS1 rev D). 5,000 pieces per reel (8871F, p. 17).

## Recommended footprint

8871F gives the package outline only, no land pattern. Use the IPC-7351 SOT-23-5 (MO-193 AB) pattern from the 5TS1 dimensions; the exact pad sizes are **UNVERIFIED** against a Microchip land-pattern drawing.

## Application circuit and required passives

- 100 nF decoupling from VCC to GND close to pin 4 (common practice; the datasheet does not state a value, **UNVERIFIED**).
- SDA and SCL pull-ups to the 1.8 V bus rail, sized with RPUP(max) = tR(max) / (0.8473 × CL) and RPUP(min) = (VCC − VOL(max)) / IOL (8871F, p. 3, Figure 2-2). The bus pull-ups are shared with the other I2C2 devices.
- WP to GND for writes; to VCC to protect the whole array (8871F, p. 2, Table 1-1; p. 10, §5.5).

## Interfaces and timing

- I²C: 100 kHz and 400 kHz at 1.7–3.6 V; 1 MHz (Fm+) only at 2.5–3.6 V (8871F, p. 1; p. 14, Table 8-3). On the 1.8 V T1 bus the limit is 400 kHz.
- Fast-mode timing at 1.7–3.6 V (8871F, p. 14, Table 8-3): tLOW ≥ 1,300 ns, tHIGH ≥ 600 ns, tAA ≤ 900 ns, tSU.DAT ≥ 100 ns, tR ≤ 300 ns, tF ≤ 300 ns, tSU.WP / tHD.WP ≥ 600 ns, tWR ≤ 5 ms.
- Device address byte: `1010 A2 A1 A0 R/W`. **In the SOT23 package A2, A1 and A0 are not bonded out and are pulled to 0 internally; the software address bits must always be 000** (8871F, p. 7, §4.1 and Table 4-1). The 7-bit address of the AT24C02D-STUM-T is therefore fixed at 0x50.
- Page write: up to 8 bytes in one row (address bits A7–A3 equal); the word address rolls over within the page (8871F, p. 8, §5.2). Acknowledge polling may replace the fixed tWR wait (8871F, p. 9, §5.3).

## Linux driver

Mainline `at24` (drivers/misc/eeprom/at24.c), `EEPROM_AT24=m` in Debian (BOM v1 line 17 and §3). Device-tree compatible `"atmel,24c02"` with `reg` = the 7-bit address and `pagesize = <8>`; `read-only` if WP is tied high. The exposed nvmem cell layout is defined by Blackbird OS.

## Simulation models

None found. IBIS for this part is not referenced in 8871F. `manifest.toml`: one `datasheet` entry (Microchip DS20006064 URL), no revision and no sha256.

## Design notes for the T1

- **Address conflict with the BOM: resolved (board BOM v1.5, 2026-10-22).** BOM v1 line 17 and the pin plan put this EEPROM at 0x57 "A2–A0 = 111", but the -STUM-T (SOT23) part has no address pins and answers only at 0x50 (8871F, p. 7). Decision (taken by the lead under the maintainers' delegation): keep the SOT23 part at **0x50** on I2C2. No other I2C2 device in BOM §4 uses 0x50, and the HAT ID EEPROM, also at 0x50, sits on its own bus (I2C4 behind the PCA9306), so the two never share a bus. The packages with A0–A2 pins (SOIC 8S1 -SSHM-T, TSSOP 8X -XHM-T, UDFN 8MA2 -MAHM-T; 8871F, pp. 16–17) are not needed.
- VIH = 0.7 × VCC: with VCC = 1.8 V on the PMUIO2 bank, the bus is level-compatible without translation.
- Power-up: the 1.8 V rail must rise no faster than 0.1 V/µs, and software must wait 100 µs after the rail is stable (8871F, p. 15).
- Write-protect strategy (WP strapped high after factory programming, or driven from a GPIO) is open.

## Sources

- Atmel, AT24C01D and AT24C02D datasheet, Atmel-8871F, 01/2017 (LCSC mirror, URL and sha256 above).
- OpenDAP board, `docs/specs/bom-v1.md`, line 17, §3 and §4 (PMUIO2 I2C2 address map).
