# TPS7A1006PDSER

- **Manufacturer:** Texas Instruments
- **Function:** 300 mA LDO with a separate bias input, fixed 0.6 V output, active output pull-down
- **BOM v1 lines:** 9 (LPDDR4X VDDQ 0.6 V LDO), Core
- **Package:** 6-pin WSON (DSE), 1.5 × 1.5 mm
- **Datasheet:** TI *TPS7A10 300-mA, Low VIN, Low VOUT, Ultra-Low Dropout Regulator*, SBVS314B, March 2018, revised October 2018, 40 pages (<https://www.ti.com/lit/ds/symlink/tps7a10.pdf>, sha256 `c2c2c5ff934b44df9fdbbff6e66f5d6397ffd5b78f6d918c91f3ffcb4dd355f9`). Cited below as "SBVS314B".
- **Status:** Partly UNVERIFIED

## Summary

The TPS7A10 is a 300 mA LDO with a separate bias input, so it regulates outputs from 0.5 V with an input as low as 0.75 V and a dropout of tens of millivolts (SBVS314B, p. 1). TPS7A1006PDSER is the fixed 0.6 V output ("06", SBVS314B p. 25, Table 3), "P" version with active output pull-down (p. 6, RPULLDOWN), in the 1.5 × 1.5 mm 6-pin WSON (DSE), reel of 3000 (p. 27, package option addendum). In the T1 it makes the LPDDR4X VDDQ 0.6 V rail from vcc_ddr (1.1 V) with BIAS from vcc_1v8 (BOM v1 line 9).

## Absolute maximum ratings

SBVS314B, p. 4, §6.1 and §6.2:

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VIN | −0.3 | 3.6 | V |
| VEN | −0.3 | 6.0 | V |
| VBIAS | −0.3 | 6.0 | V |
| VOUT | −0.3 | lesser of 3.6 and VIN + 0.3 | V |
| Output current | internally limited | — | — |
| Junction temperature TJ | −40 | 150 | °C |
| Storage temperature | −65 | 150 | °C |
| ESD HBM / CDM | — | ±1000 / ±500 | V |

## Recommended operating conditions

SBVS314B, p. 4, §6.3, unless noted:

| Parameter | Min | Nom | Max | Unit |
|---|---|---|---|---|
| VIN | 0.75 | — | 3.3 | V |
| VBIAS | 1.7 | — | 5.5 | V |
| VOUT (family) | 0.5 | — | 3.0 | V |
| IOUT (peak) | 0 | — | 300 | mA |
| CIN | 2.2 | — | — | µF |
| CBIAS | — | 0.1 | — | µF |
| COUT (ESR < 250 mΩ) | 2.2 | — | 22 | µF |
| TJ | −40 | — | 125 | °C |

Key electrical characteristics (SBVS314B, pp. 5–6, §6.5; TJ = −40 to 125 °C, VIN = VOUT + 0.5 V, VBIAS = VOUT + 1.4 V unless noted):

| Parameter | Condition | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| Output accuracy | TJ = 25 °C | −0.5 | — | 0.5 | % |
| Output accuracy | −40 to 125 °C, 1–300 mA, full VIN/VBIAS range | −1.5 | — | 1.5 | % |
| Load regulation | 0.1–300 mA | — | 0.2 | — | %/A |
| Output current limit (DSE) | VOUT = 0.9 × VOUT(NOM) | 350 | 450 | 625 | mA |
| Short-circuit current | VOUT = 0 V | — | 150 | — | mA |
| VIN dropout (DSE) | 300 mA (not measured for VOUT < 1.0 V) | — | 55 | 90 | mV |
| VBIAS dropout | 300 mA / 150 mA | — | 0.85 / 0.75 | 1.05 / 0.95 | V |
| VIN PSRR, VOUT = 1.1 V, 50 mA | 1 kHz / 100 kHz / 1 MHz | — | 60 / 36 / 32 | — | dB |
| Output noise, 10 Hz–100 kHz | VOUT = 1.0 V, 50 mA | — | 93.9 | — | µVrms |
| BIAS UVLO rising / falling | — | 1.46 / 1.35 | 1.54 / 1.44 | 1.63 / 1.55 | V |
| VIN UVLO rising / falling | — | 645 / 565 | 675 / 600 | 710 / 640 | mV |
| Start-up time (EN to 0.95 × VOUT) | — | — | 525 | 1200 | µs |
| EN high / low | — | 0.9 | — | 0.4 (low max) | V |
| Active pull-down (P version) | VBIAS = 3.3 V | — | 120 | — | Ω |
| Thermal shutdown / reset | — | — | 160 / 145 | — | °C |

## Power by mode

SBVS314B, p. 5, §6.5:

| Mode | Pin | Condition | Typ | Max | Unit |
|---|---|---|---|---|---|
| On, no load | IQ(BIAS) | TJ = 25 °C | 6 | 8 | µA |
| On, no load | IQ(IN) | TJ = 25 °C | 1.6 | 2.1 | µA |
| On, 300 mA | IQ(BIAS) / IQ(IN) | — | — | 60 / 9 | µA |
| Shutdown (VEN ≤ 0.4 V) | ISHDN(BIAS) | −40 to 85 °C | — | 400 | nA |
| Shutdown (VEN ≤ 0.4 V) | ISHDN(IN) | −40 to 85 °C | — | 1 | µA |

Dissipation PD = (IGND + IOUT) × (VIN − VOUT) (SBVS314B, p. 23, Eq. 8). For VIN = 1.1 V, VOUT = 0.6 V: 0.5 V × IOUT, i.e. 50 mW at 100 mA, 150 mW at 300 mA (derived). RθJA (DSE) 188.8 °C/W (p. 4, §6.4), so 300 mA continuous raises TJ by about 28 °C on the JEDEC board (derived).

## Pinout and package

DSE 6-pin WSON, top view (SBVS314B, p. 3; p. 24, Figure 45):

| Pin | Name | I/O | Function |
|---|---|---|---|
| 1 | OUT | O | Regulated output; COUT to GND required |
| 2 | NC | — | Not connected (shown as NC in Figure 45; absent from the pin table) |
| 3 | EN | I | Enable, active high; tie to IN only if VIN > 0.9 V |
| 4 | BIAS | I | Bias supply for the internal circuitry |
| 5 | GND | — | Ground |
| 6 | IN | I | Power input |

Package DSE0006A: 1.45–1.55 × 1.45–1.55 mm, 0.8 mm max height, pitch 0.5 mm, leads 0.2–0.3 mm wide, 0.4–0.6 mm long; pin 1 lead 0.5–0.7 mm long (SBVS314B, p. 34, drawing 4220552/B 01/2024).

## Recommended footprint

SBVS314B, p. 35, DSE0006A example board layout: six pads 0.25 mm wide on 0.5 mm pitch; pads 4–6 are 0.7 mm long and non-solder-mask-defined (0.05 mm max mask clearance); pads 1–3 are solder-mask-defined (0.05 mm min metal under mask), pad 1 is 0.8 mm long; 1.2 mm between pad-row centres; corner radius 0.05 mm. Stencil: p. 36.

## Application circuit and required passives

SBVS314B, p. 22, Figure 42 and §8.2.2; p. 24, §10:

- CIN ≥ 2.2 µF ceramic at IN, CBIAS 0.1 µF at BIAS, COUT 2.2–22 µF ceramic with ESR < 250 mΩ at OUT, all as close as possible to the pins.
- The worked example uses 4.7 µF on IN and OUT for better transient response.
- EN driven by the sequencing logic (or tied to BIAS); VIN must be ≥ VOUT + 0.5 V and VBIAS ≥ VOUT + 1.05 V for full regulation (p. 24, §9).

For the T1: VIN = vcc_ddr 1.1 V (VIN − VOUT = 0.5 V, meets §9), VBIAS = vcc_1v8 (1.8 V − 0.6 V = 1.2 V ≥ 1.05 V, meets §9).

## Interfaces and timing

- Soft-start with monotonic VOUT rise; start-up 525 µs typ, 1200 µs max from EN (SBVS314B, p. 6).
- BIAS and IN UVLO thresholds as in the table above; the output is discharged through 120 Ω when disabled (P version).

## Linux driver

None (BOM v1 line 9). The rail is described as a fixed regulator in the device tree if software needs to see it; normally it follows the PMIC sequence.

## Simulation models

- SPICE model in the TI product folder (SBVS314B, p. 25, §11.1.1.2). Not in the local cache; not listed in `manifest.toml`.
- `manifest.toml`: `datasheet` entry SBVS314B, 2018-10, sha256 `c2c2c5ff…55f9`.

## Design notes for the T1

- The LPDDR4X VDDQ load current is **UNVERIFIED** (BOM v1 line 9). The RK3566 LPDDR4X VDDQ window is 0.54–0.66 V (RK3568 Datasheet Rev 1.0, p. 55, Table 3-2), ±10 %; the LDO's ±1.5 % accuracy fits.
- Dropout is not specified below VOUT = 1.0 V (p. 5, note 2); with 0.5 V of headroom (1.1 V in) the device is far from dropout, but PSRR at this headroom is not characterised for 0.6 V output.
- Sequencing relative to the LPDDR4X VDD1/VDD2 rails follows the memory's power-up rules, which are under NDA (see [`Samsung/K4UBE3D4AB-MGCL.md`](../Samsung/K4UBE3D4AB-MGCL.md)); the Radxa ZERO 3W v1.12 reference uses a VCC0V6_DDR option (BOM v1 §6).
- Pins 1–3 on solder-mask-defined pads: draw the footprint from the p. 35 drawing, not a generic WSON-6.

## Sources

- Texas Instruments, TPS7A10 datasheet, SBVS314B (October 2018).
- Rockchip, RK3568 Datasheet Rev 1.0, 2020-12-10.
- OpenDAP board, `docs/specs/bom-v1.md`, line 9 and §6.
