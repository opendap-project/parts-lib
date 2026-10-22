# SC-32S

- **Manufacturer:** Seiko Instruments
- **Function:** 32.768 kHz tuning-fork quartz crystal
- **BOM v1 lines:** 16 (RTC 32.768 kHz crystal for the RK809), Core
  - The BOM selects the 7 pF load, ±20 ppm variant (line 16). The leaflet gives the CL range for the family, not an ordering code; the full orderable part number for 7 pF is **UNVERIFIED**.
- **Package:** 3.2 × 1.5 × 0.75 mm SMD, two pads
- **Datasheet:** Seiko Instruments *SC-32S SMD Quartz Crystal Unit* leaflet, 1 page (document title "SC-32S_Leaflet_20151208"; no revision printed). Copy read from the LCSC mirror of part C97604: <https://datasheet.lcsc.com/datasheet/pdf/01dfa0f4259dba8a3f226f0ebcc7a103.pdf>, sha256 `3b4a8a66e16acecca7125bdd3b1ccc68981eef54c0e0982edea8c2f5ea7269b5`. Cited below as "SC-32S leaflet 2015-12-08".
- **Status:** Partly UNVERIFIED

## Summary

The SC-32S is a 32.768 kHz tuning-fork quartz crystal in a 3.2 × 1.5 × 0.75 mm two-pad SMD package (SC-32S leaflet 2015-12-08, p. 1). In the T1 it is the RTC crystal of the RK809-5 PMIC (BOM v1 line 16), always powered.

## Absolute maximum ratings

| Parameter | Value | Reference |
|---|---|---|
| Absolute maximum drive level | 1.0 µW | SC-32S leaflet 2015-12-08, Standard Specifications |
| Storage temperature (piece part) | −55 to +125 °C | SC-32S leaflet 2015-12-08, Standard Specifications |

## Recommended operating conditions

Conditions: 25 ± 2 °C, DL = 0.1 µW (SC-32S leaflet 2015-12-08, Standard Specifications).

| Parameter | Value | Reference |
|---|---|---|
| Nominal frequency | 32.768 kHz | Standard Specifications |
| Frequency tolerance | ±20 × 10⁻⁶ ("please specify") | Standard Specifications |
| Turnover temperature | +25 ± 5 °C | Standard Specifications |
| Parabolic coefficient | (−0.030 ± 10 %) × 10⁻⁶/°C² | Standard Specifications |
| Load capacitance CL | 6 pF to 12.5 pF (to be specified; BOM picks 7 pF) | Standard Specifications |
| Motional resistance R1 (ESR) | 70 kΩ max | Standard Specifications |
| Drive level | 0.1 µW typ | Standard Specifications |
| Shunt capacitance C0 | 1.0 pF typ | Standard Specifications |
| Ageing, first year at +25 ± 3 °C | ±3 × 10⁻⁶ | Standard Specifications |
| Operating temperature | −40 to +85 °C | Standard Specifications |

## Power by mode

Passive resonator. Drive power is set by the RK809 32 kHz oscillator; it must stay within 1.0 µW.

## Pinout and package

- Two terminals #1 and #2, the crystal connected between them; no case ground (SC-32S leaflet, Internal Lead Connections).
- Body 3.2 (+0.1) × 1.5 ± 0.1 mm, height 0.75 ± 0.1 mm; terminal centre spacing 1.7 mm typ (SC-32S leaflet, Dimensions).

## Recommended footprint

SC-32S leaflet, Recommended Soldering Pattern: two pads 1.0 × 1.8 mm with a 1.5 mm gap (overall 3.5 mm).

No copper pattern under the crystal on the circuit board (SC-32S leaflet, Remark).

## Application circuit and required passives

One load capacitor from each terminal to ground, sized from the selected CL (7 pF) and the RK809 oscillator input capacitance and board stray. Whether the RK809 needs external load capacitors with a 7 pF crystal is **UNVERIFIED** here (BOM v1 line 16); see [`Rockchip/RK809-5.md`](../Rockchip/RK809-5.md).

## Interfaces and timing

32.768 kHz reference for the RK809 RTC and its 32 kHz clock outputs.

## Linux driver

None for the crystal (BOM v1 line 16). The RTC is handled by `rtc-rk808` and the 32 kHz output by `clk-rk808` (BOM v1 line 2).

## Simulation models

None found. `manifest.toml`: one `datasheet` entry pointing at the LCSC product page (HTML), no sha256.

## Design notes for the T1

- Frequency error over temperature follows the parabola −0.030 ppm/°C² × (T − 25 °C)²: about −3 ppm at 15 °C or 35 °C and −12 ppm at 5 °C or 45 °C (derived from the leaflet coefficient), on top of the ±20 ppm tolerance.
- Keep the copper keep-out under the body (leaflet remark) and keep the traces to the RK809 short.
- The second source in the BOM is the 12.5 pF variant; the load capacitors change with it.

## Sources

- Seiko Instruments, SC-32S leaflet 2015-12-08 (LCSC mirror, URL and sha256 above).
- OpenDAP board, `docs/specs/bom-v1.md`, lines 2, 16 and §4 clock table.
