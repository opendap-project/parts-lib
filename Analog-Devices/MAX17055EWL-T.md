# MAX17055EWL+T

- **Manufacturer:** Analog Devices
- **Function:** 1-cell fuel gauge (ModelGauge m5 EZ per the vendor's product naming, **UNVERIFIED**)
- **BOM v1 lines:** 42 (Power, battery fuel gauge), status Proposed; sense resistor line 43, optional thermistor line 101
- **Package:** WLP (the `EWL` suffix; ball count and pitch **UNVERIFIED**)
- **Datasheet:** MAX17055 datasheet, revision and date **UNVERIFIED**, <https://www.analog.com/media/en/technical-documentation/data-sheets/MAX17055.pdf>
- **Status:** Datasheet not downloaded: every field UNVERIFIED. The manifest URL timed out from this host on 2026-10-22 (curl and WebFetch, three attempts). Every value below comes from the OpenDAP BOM v1 or power tree v0 and is **UNVERIFIED** until the datasheet is read.

## Summary

The MAX17055 is the T1 battery fuel gauge on I2C1 (1.8 V) at 7-bit address 0x36, powered from BAT, measuring current through a 10 mΩ sense resistor (BOM lines 42–43, power tree §2). Its TH input needs its own thermistor (line 101, optional) or the internal die sensor, because the board NTC is on the charger TS pin (BOM line 42). All of this is from the BOM; nothing has been checked against the datasheet (**UNVERIFIED**).

## Absolute maximum ratings

Not available: datasheet not downloaded. **UNVERIFIED**

## Recommended operating conditions

Not available: datasheet not downloaded. **UNVERIFIED**

## Power by mode

Power tree §4.9 lumps the gauge into "IMU, gauge, TCPC, charger: 3 mW" from datasheets; per-mode currents (active, hibernate, shutdown) are **UNVERIFIED**.

## Pinout and package

Package code `EWL` (WLP) from the MPN. Ball map **UNVERIFIED**.

## Recommended footprint

Not available: datasheet not downloaded. **UNVERIFIED**

## Application circuit and required passives

- Sense resistor: 10 mΩ 1 % (BOM line 43, Yageo RL0603FR-070R01L); "typical 10 mΩ" is itself marked **UNVERIFIED** in the BOM.
- Thermistor on TH: optional 10 kΩ NTC, Murata NCP15XH103F03RC (BOM line 101). **UNVERIFIED**
- Supply decoupling and the REG/ALRT pins: **UNVERIFIED**.

## Interfaces and timing

I2C (2-wire) at 0x36 on the 1.8 V I2C1 bus (BOM line 42). Input thresholds at 1.8 V, maximum SCL rate and the ALRT output type are **UNVERIFIED**.

## Linux driver

Mainline `max17042_battery` (drivers/power/supply/max17042_battery.c, Kconfig `BATTERY_MAX17042`) supports the MAX17055 with compatible `maxim,max17055`. The BOM states that Debian does not enable `BATTERY_MAX17042`, so the T1 builds it as DKMS (opendap-os ADR 0007). The compatible string and the driver's handling of the MAX17055 model registers are from memory of the mainline source and are **UNVERIFIED**.

## Simulation models

None listed in `manifest.toml`. Vendor models **UNVERIFIED** (not checked).

## Design notes for the T1

- Read the datasheet before the schematic: VBATT range, I2C VIH/VIL at 1.8 V, sense-resistor recommendation, and whether TH can be left unused with the internal temperature (**UNVERIFIED**).
- The battery model (EZ configuration with the Adafruit 328 capacity 2500 mAh and charge voltage 4.2 V) must be set at boot by the driver or a DT property; method **UNVERIFIED**.
- Lowest-current mode for suspend: the gauge stays on in suspend (power tree §6.5).

## Sources

- Manifest URL above (not downloaded; no sha256).
- OpenDAP board BOM v1 (2026-10-22) lines 42, 43, 101; power tree v0 §2, §4.9, §6.5.
