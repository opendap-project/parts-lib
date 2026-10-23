# INA236AIDDFR

- **Manufacturer:** Texas Instruments
- **Function:** 48 V, 16-bit current, voltage and power monitor with I2C, address option A
- **BOM v1 lines:** 54 (Power), ×4: VSYS, audio block, display block, HAT; status Proposed
- **Package:** SOT-23-THIN 8-pin (DDF, drawing DDF0008A)
- **Datasheet:** INA236 48-V, 16-Bit, Ultra-Precise, Current, Voltage, and Power Monitor With an I2C Interface, SBOSA81D (May 2021, revised August 2023), <https://www.ti.com/lit/ds/symlink/ina236.pdf>
- **Status:** Partly UNVERIFIED

## Summary

The INA236 measures the voltage across an external shunt (±81.92 mV or ±20.48 mV full scale) and the bus voltage on IN− (common mode −0.3 to 48 V, independent of its 1.7–5.5 V supply), and computes current and power from a calibration register (SBOSA81D p. 1, §1, §3; p. 24, §8.1.1). Its I2C interface is specified for 1.2 V, 1.8 V, 3.3 V and 5 V buses (p. 1, §3). The "A" option uses addresses 0x40–0x43 selected by one pin (p. 16, Table 7-1). The T1 fits four on I2C1 (1.8 V) for power instrumentation (T1-026): VSYS (10 mΩ shunt), audio block (100 mΩ), display block (100 mΩ) and HAT (20 mΩ) (BOM v1 line 54, §5).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| Supply VS | — | 6 | V | SBOSA81D p. 4, §6.1 |
| Differential VIN+ − VIN− | −26 | 26 | V | p. 4, §6.1 |
| Common mode IN+, IN− | GND − 0.3 | 50 | V | p. 4, §6.1 |
| SDA, SCL, ALERT, A0 | GND − 0.3 | 6 | V | p. 4, §6.1 |
| Input current into any pin | — | 5 | mA | p. 4, §6.1 |
| Open-drain output current (SDA, ALERT) | — | 10 | mA | p. 4, §6.1 |
| Operating temperature | −55 | 150 | °C | p. 4, §6.1 |
| Junction temperature | — | 150 | °C | p. 4, §6.1 |
| Storage temperature | −65 | 150 | °C | p. 4, §6.1 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 4, §6.2 |
| ESD, CDM (JS-002) | — | ±1000 | V | p. 4, §6.2 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Common-mode input range | GND − 0.3 | — | 48 | V | SBOSA81D p. 4, §6.3 |
| Supply VS | 1.7 | — | 5.5 | V | p. 4, §6.3 |
| Ambient temperature | −40 | — | 125 | °C | p. 4, §6.3 |
| Shunt input range, ADCRANGE = 0 | −81.9175 | — | 81.92 | mV | p. 5, §6.5 |
| Shunt input range, ADCRANGE = 1 | −20.4794 | — | 20.48 | mV | p. 5, §6.5 |
| Shunt LSB, ADCRANGE = 0 / 1 | — | 2.5 / 0.625 | — | µV | p. 5, §6.5 |
| Bus voltage LSB | — | 1.6 | — | mV | p. 5, §6.5 |
| Shunt offset voltage (VCM = 12 V) | — | ±1 | ±5 | µV | p. 5, §6.5 |
| Shunt gain error | — | ±0.015 | ±0.1 | % | p. 5, §6.5 |
| Bus (IN−) offset | — | ±1 | ±7.5 | mV | p. 5, §6.5 |
| Bus gain error | — | ±0.015 | ±0.1 | % | p. 5, §6.5 |
| CMRR, −0.3 to 48 V | 136 | 150 | — | dB | p. 5, §6.5 |
| Input bias current, current-measurement mode | — | 0.1 | 10 | nA | p. 5, §6.5 |
| IN− input impedance, bus-measurement mode | — | 1.05 | — | MΩ | p. 5, §6.5 |
| Differential input impedance | — | 140 | — | kΩ | p. 5, §6.5 |
| VIH (VS = 1.7–5.5 V, −40 to 125 °C) | 0.9 | — | 5.5 | V | p. 6, §6.5 |
| VIL | 0 | — | 0.4 | V | p. 6, §6.5 |
| Input hysteresis | — | 130 | — | mV | p. 6, §6.5 |
| VOL at 3 mA | 0 | — | 0.3 | V | p. 6, §6.5 |
| Power-on reset, VS falling | — | 0.95 | — | V | p. 5, §6.5 |

Thermal (DDF, p. 4, §6.4): RθJA 146.8 °C/W, RθJC(top) 70.5 °C/W, RθJB 67.1 °C/W.

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Active (continuous or triggered conversion) | VSENSE = 0 mV, VS = 3.3 V, 25 °C | 300 | 380 | µA | SBOSA81D p. 5, §6.5 |
| Active, over temperature | −40 to 125 °C | — | 500 | µA | p. 5, §6.5 |
| Shutdown (MODE = 000b or 100b) | 25 °C | 2.2 | 3 | µA | p. 5, §6.5; p. 20, Table 7-4 |
| Input leakage in shutdown (IN+, IN−) | — | 0.1 | 5 | nA | p. 5, §6.5 |
| Recovery from shutdown | — | 100 | — | µs | p. 15, §7.4.2 |

Power-up default is MODE = 111b, continuous shunt and bus conversion (reset value 4127h, p. 19–20, Table 7-2, Table 7-4). The device is active, not in shutdown, until software writes the mode.

## Pinout and package

| Pin (DDF) | Name | Type | Function |
|---|---|---|---|
| 1 | IN+ | Analog in | Shunt positive input (supply side for high-side sensing) |
| 2 | IN− | Analog in | Shunt negative input (load side); bus voltage is measured on this pin |
| 3 | GND | Ground | Analog and digital ground |
| 4 | VS | Power | Supply, 1.7–5.5 V |
| 5 | SCL | Digital in | I2C clock, open drain |
| 6 | SDA | Digital I/O | I2C data, open drain |
| 7 | A0 | Digital in | Address select: GND, VS, SDA or SCL |
| 8 | ALERT | Digital out | Open-drain alert or conversion-ready output; may float if unused |

Source: SBOSA81D p. 3, Figure 5-2, Table 5-1; ALERT p. 14, §7.3.5. Marking 2QRF, MSL 1 at 260 °C, 3000 per reel (p. 37, Package Option Addendum).

## Recommended footprint

- Drawing DDF0008A (4222047/E, July 2024), SBOSA81D p. 41–43. Body 2.85–2.95 mm × 1.55–1.65 mm, 1.1 mm maximum height, lead span 2.65–2.95 mm, pitch 0.65 mm (p. 41).
- Land pattern example: 8 pads 1.05 mm × 0.45 mm, 0.65 mm pitch, 2.6 mm between pad-row centres (p. 42). Stencil example: same openings, 0.125 mm stencil (p. 43).
- Kelvin (4-wire) connection from IN+ and IN− to the shunt pads; bypass capacitor next to VS and GND (p. 31, §8.4.1). Layout example for DDF: Figure 8-6, p. 32.

## Application circuit and required passives

| Item | Value / rule | Source |
|---|---|---|
| VS bypass | 0.1 µF, close to VS and GND | SBOSA81D p. 31, §8.3 |
| Shunt | RSHUNT < VSENSE_MAX / IMAX | p. 29, Equation 5 |
| Calibration | SHUNT_CAL = 0.00512 / (CURRENT_LSB × RSHUNT); divide by 4 for ADCRANGE = 1 | p. 25, Equation 1 |
| Current, power | Current = CURRENT_LSB × CURRENT; Power = 32 × CURRENT_LSB × POWER | p. 25, Equations 3–4 |
| Optional input filter | ≤ 100 Ω series per input, 0.1–1 µF across inputs; only needed for transients near harmonics of the 500 kHz sampling rate | p. 27–28, §8.1.4, Figure 8-1 |
| Optional dV/dt protection | 10 Ω in series with each input protects against dV/dt failures up to 48 V | p. 28, §8.1.4 |
| I2C pull-ups | to the bus voltage (1.2–5.5 V shown in layout example) | p. 31–32, Figures 8-5, 8-6 |

## Interfaces and timing

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| SCL, fast mode | 1 | — | 400 | kHz | SBOSA81D p. 7, §6.6 |
| SCL, high-speed mode | 10 | — | 2940 | kHz | p. 7, §6.6 |
| Bus free time (fast mode) | 600 | — | — | ns | p. 7, §6.6 |
| SCL low / high (fast mode) | 1300 / 600 | — | — | ns | p. 7, §6.6 |
| Data hold time (fast mode) | 10 | — | 900 | ns | p. 7, §6.6 |
| Data setup time (fast mode) | 100 | — | — | ns | p. 7, §6.6 |
| SMBus timeout | 28 | — | 35 | ms | p. 6, §6.5 |
| ADC conversion time (per channel, CT = 000b … 111b) | 0.133 | 0.140 … 8.244 | 8.656 | ms | p. 5, §6.5 |
| Averaging | 1 | — | 1024 | samples | p. 20, Table 7-4 |

- **Addresses (p. 16, Table 7-1):** INA236A: A0 = GND 0x40, VS 0x41, SDA 0x42, SCL 0x43. INA236B: 0x48–0x4B. With A0 tied to SDA, add 100 ns extra hold time on the MSB of the address (p. 16, §7.5.1).
- **Protocol:** registers are 16-bit, MSB first; no packet error checking, no clock stretching (p. 17, Figures 7-3, 7-4). Supports general-call reset (00h + 06h), general-call conversion start, and SMBus Alert Response (p. 18, §7.5.4–7.5.6).
- **Registers (p. 19, Table 7-2):** 0h configuration (reset 4127h), 1h shunt voltage, 2h bus voltage, 3h power, 4h current, 5h calibration, 6h mask/enable, 7h alert limit, 3Eh manufacturer ID (5449h), 3Fh device ID (A080h).
- **ALERT:** one function at a time (shunt over/under, bus over/under, power over) plus optional conversion ready; response one to two conversion cycles (p. 13–14, §7.3.5; p. 30, §8.2.3).

## Linux driver

Mainline IIO driver `drivers/iio/adc/ina2xx-adc.c`, compatible `ti,ina236` and I2C id `ina236`; its chip table gives shunt LSB 2.5 µV, bus LSB 1.6 mV and power LSB factor 32, matching the datasheet (source read 2026-10-22 from the mainline `master` tree). Kconfig `CONFIG_INA2XX_ADC`, built as a module in Debian trixie-backports `linux-config-7.2` per BOM v1 §Conventions (not re-checked here). The shunt value is set in the device tree with `shunt-resistor` in µΩ (binding `ti,ina2xx.yaml`, **UNVERIFIED** for this exact property name with the IIO driver). Whether the IIO driver places the device in shutdown when no capture is running is **UNVERIFIED**.

## Simulation models

No model is listed in `manifest.toml`. Vendor models are **UNVERIFIED**; the device is a digital monitor and is unlikely to need electrical simulation beyond the shunt and filter.

## Design notes for the T1

- **1.8 V I2C:** VIH is 0.9 V minimum for any VS from 1.7 to 5.5 V (p. 6), so the INA236 runs on I2C1 at 1.8 V while VS is 3.3 V. This confirms the BOM reason for dropping the INA226.
- **Addresses:** the INA236A option gives exactly 0x40–0x43 (p. 16), matching the BOM. A0 = SDA (0x42) needs the 100 ns MSB hold; whether the RK3566 I2C controller provides it is **UNVERIFIED**. If not, use the INA236B for that position, or map the four devices so that the A0 = SDA slot is checked on the first boards. The BQ25895 (0x6A), FUSB302B (0x22) and MAX17055 (0x36) on I2C1 do not collide with 0x40–0x43.
- **General call:** a general-call reset (00h, 06h) on I2C1 resets all four INA236 to defaults (p. 18). No T1 software should issue it on that bus.
- **Full-scale currents** with ADCRANGE = 0 (81.92 mV): 10 mΩ → 8.19 A, 100 mΩ → 0.82 A, 20 mΩ → 4.10 A (calculation from p. 5). All exceed the design maxima in the power tree §3 (VSYS 3.5 A on adapter, HAT 1.5 + 1.0 A); the 100 mΩ audio and display blocks are limited to 0.82 A, to check against the display block peak with full backlight (0.33 A input, power tree §4.5) and the audio block peak.
- **Bus voltage on IN−:** in bus-measurement mode IN− sees about 1 MΩ to ground (p. 13, §7.3.3), about 4 µA at 4.4 V per device. Shunt-only mode (MODE = 101b) avoids it.
- **Default state (power tree §5):** the power tree lists the instrumentation default as "power-down"; the device actually powers up converting continuously (MODE = 111b, p. 20), about 300 µA each, 1.2 mA for four, until software writes MODE = 000b. The power-down default therefore depends on Blackbird OS or the boot loader, not on hardware.
- **Supply sequencing:** none required; bus voltage may be present with VS off (p. 12, §7.3.1).

## Sources

- TI, INA236 datasheet, SBOSA81D, revised August 2023, <https://www.ti.com/lit/ds/symlink/ina236.pdf>, sha256 `47e4c0976d958a27621450eb4732ba2f1b3b3e7f5606b3f7370ad8ba456ec45d` (manifest). Page numbers are PDF page numbers.
- Linux mainline `drivers/iio/adc/ina2xx-adc.c` (`master`, read 2026-10-22), <https://github.com/torvalds/linux/blob/master/drivers/iio/adc/ina2xx-adc.c>.
- OpenDAP board BOM v1 line 54 and power tree v0 §1 finding 13, §3, §5 (T1 context).
