# LSM6DSV16XTR

- **Manufacturer:** STMicroelectronics
- **Function:** 6-axis inertial measurement unit (3-axis accelerometer, 3-axis gyroscope) with embedded sensor fusion, finite state machine, machine learning core and Qvar
- **Package:** LGA-14L, 2.5 × 3.0 × 0.86 mm (maximum height)
- **Datasheet:** LSM6DSV16X, DS13510 Rev 4 (25 May 2023). The `manifest.toml` entry has no sha256 yet; the copy read here (198 pages, obtained from the LCSC datasheet mirror) has sha256 `ec53c0e5952fc0c9587ed32b56d066016c2954bc6e9d18355b13a1c4cda17894`
- **BOM v1 line:** 59

## Summary

The LSM6DSV16X is a 6-axis IMU with an I²C / MIPI I3C / SPI host interface, two programmable interrupt pins and embedded low-power functions: pedometer, tilt, significant motion, wake-up and activity detection (DS13510 §1–§2, pp. 3–8). In the T1 it is the motion sensor (BOM v1 line 59). It runs from vcc_1v8 (VDDIO 1.8 V) on I2C2 at 0x6A, and INT1 goes to GPIO 0_C5 for wake-on-motion.

## Absolute maximum ratings

| Parameter | Rating | Unit | Reference |
|---|---|---|---|
| Supply voltage, Vdd | −0.3 to 4.8 | V | DS13510 p. 19, Table 9 |
| Input voltage on any control pin (CS, SCL/SPC, SDA/SDI/SDO, SDO/SA0), Vin | −0.3 to Vdd_IO + 0.3 | V | p. 19, Table 9 |
| Supply voltage on any pin | ≤ 4.8 | V | p. 19, note to Table 9 |
| Storage temperature, TSTG | −40 to +125 | °C | p. 19, Table 9 |
| Acceleration for 0.2 ms, Sg | 20,000 | g | p. 19, Table 9 |
| ESD, HBM | 2 | kV | p. 19, Table 9 |

## Recommended operating conditions

Electrical characteristics at Vdd = 1.8 V, T = 25 °C (DS13510 p. 14, Table 4). Typical values are not guaranteed (Table 4 note 1).

| Parameter | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, Vdd | 1.71 | 1.8 | 3.6 | V | p. 14, Table 4 |
| I/O supply, Vdd_IO | 1.08 | — | 3.6 | V | p. 14, Table 4 |
| Operating temperature, Top | −40 | — | +85 | °C | p. 14, Table 4 |
| Digital input high, VIH | 0.7 × Vdd_IO | — | — | V | p. 14, Table 4 |
| Digital input low, VIL | — | — | 0.3 × Vdd_IO | V | p. 14, Table 4 |
| Output high, VOH (IOH = 4 mA) | Vdd_IO − 0.2 | — | — | V | p. 14, Table 4 |
| Output low, VOL (IOL = 4 mA) | — | — | 0.2 | V | p. 14, Table 4 |
| Gyroscope turn-on time, Ton | — | 30 | — | ms | p. 14, Table 4 |

4 mA is the maximum DC drive of a digital pin (Table 4 note 2).

Measurement ranges: accelerometer ±2/±4/±8/±16 g; gyroscope ±125/±250/±500/±1000/±2000/±4000 dps (p. 12, Table 3). Rate noise density 2.8 mdps/√Hz (high-performance mode). Acceleration noise density 60 µg/√Hz (high-performance) and 100 µg/√Hz (normal mode) (p. 12, Table 3).

## Power by mode

Vdd = 1.8 V, T = 25 °C, typical (DS13510 p. 14, Table 4).

| Mode | Condition | Typ | Unit | Reference |
|---|---|---|---|---|
| Gyroscope + accelerometer, high-performance (IddHP) | — | 0.65 | mA | Table 4 |
| Accelerometer only, high-performance (LA_IddHP) | — | 190 | µA | Table 4 |
| Accelerometer only, normal mode (LA_IddNM) | — | 100 | µA | Table 4 |
| Accelerometer only, low-power LPM2 | ODR 60 Hz | 20 | µA | Table 4 |
| Accelerometer only, low-power LPM2 | ODR 1.875 Hz | 4.2 | µA | Table 4 |
| Accelerometer only, low-power LPM1 | ODR 60 Hz | 17 | µA | Table 4 |
| Accelerometer only, low-power LPM1 | ODR 1.875 Hz | 4.0 | µA | Table 4 |
| Power-down, gyroscope + accelerometer (IddPD) | — | 2.6 | µA | Table 4 |
| Qvar / analog hub, extra | Accelerometer in HP or normal mode | 15 | µA | p. 14, Table 5 |
| High-accuracy ODR mode, extra | vs. the same HP configuration | 20 | µA | p. 33, §6.5 |

The accelerometer and gyroscope are switched on and off independently, with independent ODRs and power modes (§6.1, p. 31). Accelerometer modes: power-down, LPM1/2/3 (ODR 1.875–240 Hz), normal (7.5 Hz–1.92 kHz), high-performance (7.5 Hz–7.68 kHz), high-accuracy ODR (§6.2, p. 31). Gyroscope modes: power-down, sleep, low-power (7.5–240 Hz), high-performance, high-accuracy ODR (§6.4, p. 33). The embedded functions (wake-up, activity/inactivity, step counter, tilt, significant motion and others) run in every accelerometer mode (§6.2, p. 31).

## Pinout and package

LGA-14L (Figure 5, p. 9; Table 2, p. 11). Functions shown for mode 1 (host interface only), the T1 configuration:

| Pin | Name | Mode 1 function |
|---|---|---|
| 1 | SDO/SA0 | SPI 4-wire SDO / I²C address LSB (SA0) |
| 2 | SDx/AH1/Qvar1 | Connect to Vdd_IO or GND when the analog hub and Qvar are disabled |
| 3 | SCx/AH2/Qvar2 | Connect to Vdd_IO or GND when the analog hub and Qvar are disabled |
| 4 | INT1 | Programmable interrupt 1 |
| 5 | Vdd_IO | I/O supply (100 nF recommended) |
| 6 | GND | 0 V |
| 7 | GND | 0 V |
| 8 | Vdd | Core supply (100 nF recommended) |
| 9 | INT2 | Programmable interrupt 2 / data enable (DEN) |
| 10 | OCS_Aux | Connect to Vdd_IO or leave unconnected (soldered) |
| 11 | SDO_Aux | Connect to Vdd_IO or leave unconnected (soldered) |
| 12 | CS | I²C/I3C/SPI selection: 1 = I²C/I3C enabled, 0 = SPI |
| 13 | SCL | I²C/I3C SCL / SPI SPC |
| 14 | SDA | I²C/I3C SDA / SPI SDI / 3-wire SDO |

Default pin states (Table 23, pp. 50–51): SDO/SA0, SDx, SCx, SCL and SDA are inputs without pull-up; INT1 is driven to ground; pins 10 and 11 have internal pull-ups in modes 1 and 2. Internal pull-up value: 30–50 kΩ depending on Vdd_IO (p. 51).

Package: body 2.50 ± 0.1 × 3.00 ± 0.1 mm, 0.86 mm maximum height; 14 lands of 0.25 ± 0.05 × 0.475 ± 0.05 mm at 0.5 mm pitch (Figure 33, p. 175, drawing DM00249496_5). Reel A (max) 330 mm (Table 506, p. 177). Qualified for soldering heat resistance per JEDEC J-STD-020 (§18, p. 174).

## Recommended footprint / land pattern

The datasheet does not give a land pattern. It refers to ST technical note TN0018 for land pattern and soldering recommendations (§18, p. 174). TN0018 was not opened for this sheet, so any pad dimensions beyond the package lands above are **UNVERIFIED**.

## Application circuit and required passives

Mode 1 connection (§7.1, Figure 28, p. 47):

- C1 = 100 nF ceramic on Vdd and C2 = 100 nF ceramic on Vdd_IO, placed as close as possible to the supply pins.
- I²C pull-ups Rpu = 10 kΩ on SCL and SDA to Vdd_IO. The T1 uses the shared I2C2 bus pull-ups.
- CS tied to Vdd_IO to select I²C (§5.1, p. 21).
- SDO/SA0 to GND for address 0x6A.
- Pins 10 and 11 (OCS_Aux, SDO_Aux) left unconnected but soldered; pins 2 and 3 tied to Vdd_IO or GND (Table 2, p. 11).

## Interfaces and timing

- **I²C slave address:** 110101xb; SA0 = GND gives 1101010b (0x6A), SA0 = supply gives 1101011b (0x6B) (§5.1.2, p. 22, Table 12).
- **I²C speed:** fast mode 400 kHz and fast mode plus 1000 kHz (§5.1.1, p. 21).
- **WHO_AM_I** (0Fh) is fixed at 70h (p. 64).
- **Interrupts:** INT1 and INT2 are push-pull by default; the PP_OD bit selects open-drain (p. 58).

I²C slave timing (p. 18, Table 8; characterization data, not tested in production):

| Symbol | Parameter | Fast mode min | Fast mode max | Fast mode plus min | Fast mode plus max | Unit |
|---|---|---|---|---|---|---|
| f(SCL) | SCL clock frequency | 0 | 400 | 0 | 1000 | kHz |
| tw(SCLL) | SCL low time | 1.3 | — | 0.5 | — | µs |
| tw(SCLH) | SCL high time | 0.6 | — | 0.26 | — | µs |
| tsu(SDA) | SDA setup time | 100 | — | 50 | — | ns |
| th(SDA) | SDA hold time | 0 | 0.9 | 0 | — | µs |
| th(ST) | START / repeated START hold time | 0.6 | — | 0.26 | — | µs |
| tsu(SR) | Repeated START setup time | 0.6 | — | 0.26 | — | µs |
| tsu(SP) | STOP setup time | 0.6 | — | 0.26 | — | µs |
| tw(SP:SR) | Bus free time between STOP and START | 1.3 | — | 0.5 | — | µs |
| — | Data valid time | — | 0.9 | — | 0.45 | µs |
| — | Data valid acknowledge time | — | 0.9 | — | 0.45 | µs |
| CB | Capacitive load per bus line | — | 400 | — | 550 | pF |

SPI: up to 10 MHz, modes 0 and 3 (p. 16, Table 7; §5.1, p. 21). The T1 does not use SPI.

## Linux driver

- Mainline IIO driver `st_lsm6dsx` (`drivers/iio/imu/st_lsm6dsx/`, Kconfig `IIO_ST_LSM6DSX` with the I²C front end `IIO_ST_LSM6DSX_I2C`). The BOM records the driver path as *mainline + Debian*.
- The device tree compatible is `st,lsm6dsv16x`. The kernel version that added it and whether Debian enables `IIO_ST_LSM6DSX` are **UNVERIFIED** (not re-checked against the source or the Debian config in this pass).
- Whether the driver supports wake-on-motion through INT1 as a system wakeup source (`wakeup-source`) for this device is **UNVERIFIED**.

## Simulation models available

None listed in `manifest.toml`. Not expected for a MEMS sensor; any ST IBIS model is **UNVERIFIED**.

## Design notes for the T1

- Vdd and Vdd_IO both at 1.8 V (vcc_1v8) are inside 1.71–3.6 V and 1.08–3.6 V (Table 4). The I²C levels (VIH 0.7 × Vdd_IO) match the 1.8 V PMUIO2 I2C2 bus.
- SA0 to GND → 0x6A on I2C2. The BQ25895 also sits at 0x6A, but on I2C1, so there is no clash (BOM line 59).
- INT1 is driven low by default and push-pull at Vdd_IO (Table 23; p. 58), so it connects directly to the 1.8 V GPIO 0_C5 without a pull-up.
- Wake-on-motion: run the accelerometer in LPM1 at 1.875 Hz (4.0 µA typical) with the gyroscope in power-down. Datasheet figures only; the residual current of the full suspend configuration is **UNVERIFIED**.
- The part is a MEMS sensor: avoid placing it near board-flex points, mounting screws or the speaker. This is general MEMS practice, not a datasheet requirement (**UNVERIFIED**). The datasheet warns of sensitivity to mechanical shock (p. 19).

## Sources

- STMicroelectronics, *LSM6DSV16X 6-axis IMU and AI sensor with embedded sensor fusion, Qvar for high-end applications*, DS13510 Rev 4, May 2023, <https://www.st.com/resource/en/datasheet/lsm6dsv16x.pdf> (copy obtained from the LCSC datasheet mirror)
- OpenDAP board, `docs/specs/bom-v1.md`, line 59 and §4.2
