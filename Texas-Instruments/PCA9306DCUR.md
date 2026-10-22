# PCA9306DCUR

- **Manufacturer:** Texas Instruments
- **Function:** Dual bidirectional I2C and SMBus voltage-level translator (pass-FET type) with enable
- **Package:** VSSOP-8 (DCU), 2.3 × 3.1 mm nominal, 0.5 mm pitch
- **Datasheet:** PCA9306, SCPS113O (October 2004, revised September 2023), sha256 `1cd97c734729…` in `manifest.toml`
- **BOM v1 line:** 94

## Summary

The PCA9306 is a two-channel pass-FET translator for open-drain I2C and SMBus lines, with no direction pin, VREF1 from 1.2 to 3.3 V and VREF2 from 1.8 to 5.5 V (SCPS113O §3, §8.1, pp. 1, 10). When EN is low, both sides are high-impedance and isolated (§1, p. 1; §8.4, p. 16). In the T1 it joins the 1.8 V I2C4 M1 host side (VCCIO4) to the 3.3 V HAT ID EEPROM bus at 0x50, and its EN keeps the HAT bus isolated until HAT_DET# (BOM v1 line 94).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Reference |
|---|---|---|---|---|
| VREF1 DC reference voltage | −0.5 | 7 | V | SCPS113O p. 5, §6.1 |
| VREF2 DC reference bias voltage | −0.5 | 7 | V | p. 5 |
| Input voltage, VI | −0.5 | 7 | V | p. 5 |
| Input/output voltage, VI/O | −0.5 | 7 | V | p. 5 |
| Continuous channel current | — | 128 | mA | p. 5 |
| Input clamp current, IIK (VI < 0) | — | −50 | mA | p. 5 |
| Maximum junction temperature | — | 125 | °C | p. 5 |
| Storage temperature | −65 | 150 | °C | p. 5 |
| ESD, HBM (JS-001, all pins) | — | ±2000 | V | p. 5, §6.2 |
| ESD, CDM (JS-001, all pins) | — | ±1000 | V | p. 5, §6.2 |

## Recommended operating conditions

| Parameter | Min | Max | Unit | Reference |
|---|---|---|---|---|
| I/O voltage, SCL1, SDA1, SCL2, SDA2 | 0 | 5.5 | V | p. 5, §6.3 |
| VREF1 | 0 | 5.5 | V | p. 5 |
| VREF2 | 0 | 5.5 | V | p. 5 |
| EN input voltage | 0 | 5.5 | V | p. 5 |
| Pass switch current, IPASS | — | 64 | mA | p. 5 |
| Operating ambient temperature, TA | −40 | 85 | °C | p. 5 |

For translation, VREF1 must be between 1.2 V and VREF2 − 0.6 V, and VREF2 between VREF1 + 0.6 V and 5.5 V (§6.3 note 1, p. 5). Design requirements of the typical application (§9.2.1, p. 18): VREF2 and EN ≥ VREF1 + 0.6 V (typ 2.1, max 5 V), VREF1 1.2–4.4 V (typ 1.5 V), IPASS 6 mA maximum, reference-transistor current IREF 5 µA maximum.

### Electrical characteristics (selected)

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| Input leakage, IIH | VI = 5 V, EN = 0 V | — | — | 5 | µA | p. 6, §6.5 |
| EN input capacitance | VI = 3 V or 0 | — | 11 | — | pF | p. 6 |
| Off capacitance, Cio(off) | EN = 0 V | — | 4 | 6 | pF | p. 6 |
| On capacitance, Cio(on) | EN = 3 V | — | 10.5 | 12.5 | pF | p. 6 |
| On resistance, RON | VI = 0, IO = 64 mA, EN = 3 V | — | 4.7 | 7 | Ω | p. 6 |
| On resistance, RON | VI = 0, IO = 15 mA, EN = 2.3 V | — | 6.3 | 9.5 | Ω | p. 6 |
| On resistance, RON | VI = 0, IO = 15 mA, EN = 1.5 V | — | 25.5 | 32 | Ω | p. 6 |
| On resistance, RON | VI = 1.7 V, IO = 15 mA, EN = 2.3 V | 20 | 60 | 140 | Ω | p. 6 |

Thermal (DCU): RθJA 275.5 °C/W (p. 6, §6.4). The FET threshold Vth is about 0.6 V at room temperature (§8.1.1, p. 10).

## Power by mode

No supply current is specified: the device draws only the reference bias current through the VREF2 resistor, Ibias = (VCC2 − Ven) / 200 kΩ with Ven = VREF1 + Vth (§8.1.7 Equations 1–2, p. 14; §8.1.8 Equation 5, p. 15). For VREF1 = 1.8 V and VDPU = 3.3 V this gives about (3.3 − 2.4) / 200 kΩ ≈ 4.5 µA (calculated here from the datasheet equation, Vth ≈ 0.6 V). With EN low, no bias flows through the pass FETs. IREF maximum is 5 µA (§9.2.1, p. 18).

## Pinout and package

DCU pin numbers (Figure 5-2, Table 5-1, p. 4):

| Pin | Name | I/O | Description |
|---|---|---|---|
| 1 | GND | — | Ground |
| 2 | VREF1 | I | Low-voltage-side reference for SCL1 and SDA1 |
| 3 | SCL1 | I/O | Serial clock, low-voltage side |
| 4 | SDA1 | I/O | Serial data, low-voltage side |
| 5 | SDA2 | I/O | Serial data, high-voltage side |
| 6 | SCL2 | I/O | Serial clock, high-voltage side |
| 7 | VREF2 | I | High-voltage-side reference for SCL2 and SDA2 |
| 8 | EN | I | Switch enable |

Outline DCU0008A (drawing 4225266/A, p. 31): body 2.2–2.4 × 1.9–2.1 mm (excluding mold flash, ≤ 0.15 mm per side), lead span 3.0–3.2 mm, 0.5 mm pitch, leads 0.17–0.25 mm wide, 0.6–0.9 mm height; JEDEC MO-187 variation CA. MSL Level-1-260C-UNLIM, NiPdAu or Sn; −40 to 85 °C; reel 3000 (p. 24).

## Recommended footprint / land pattern

DCU0008A example board layout (p. 32, drawing 4225266/A, scale 25:1): 8 pads 0.85 × 0.3 mm (reference), 0.5 mm pitch, 3.1 mm between pad-row centres (reference); non-solder-mask-defined preferred, 0.05 mm maximum mask clearance. Stencil example on p. 33.

## Application circuit and required passives

From §8.1.2 (p. 10), §9.2 (pp. 17–18) and §10 (p. 21):

- EN shorted to VREF2, both pulled to the high-side supply VDPU through 200 kΩ. VREF2 must never be tied directly to VDPU: without the resistor the pass FET can carry current above the 128 mA absolute maximum (§8.1.2, Figure 8-2, pp. 10–11; §10, p. 21).
- 100 pF filter capacitor on VREF2, placed close to the pin (§9.2.2.1, p. 18; §11.1, p. 22). A larger capacitor lengthens turn-on and turn-off through the 200 kΩ.
- VREF1 directly to the low-side supply (§10, p. 21).
- Pull-up resistors on both sides: SCL1/SDA1 to VREF1, SCL2/SDA2 to VDPU (§8.3.2, p. 16; §9.1.1, p. 17). Sizing per SLVA689 (§9.2.2.2, p. 18).
- If VREF1 comes from an LDO that cannot sink current, add a pull-down on VREF1: Rpulldown = 0.75 × VOUT / Ibias (§8.1.7 Equations 3–4, p. 14).
- Gated enable: Figure 9-2 (p. 18) drives the 200 kΩ from a 3.3 V enable signal instead of from VDPU.

## Interfaces and timing

Bidirectional, open-drain only. Lows pass from either side; highs are restored by each side's pull-ups. The switch conducts when EN is at least 0.6 V above the line (§8.4, note 1, p. 16). Total capacitance of both sides counts towards the 400 pF I2C limit (§8.1, p. 10).

Propagation delay, maximum, DCU package (§6.6–6.9, p. 7):

| Direction | EN | CL = 50 pF | CL = 30 pF | CL = 15 pF | Unit |
|---|---|---|---|---|---|
| Down (side 2 → 1), tPLH | 3.3 V | 0.8 | 0.6 | 0.3 | ns |
| Down (side 2 → 1), tPHL | 3.3 V | 1.2 | 1 | 0.75 | ns |
| Up (side 1 → 2), tPLH | 3.3 V | 0.9 | 0.6 | 0.4 | ns |
| Up (side 1 → 2), tPHL | 3.3 V | 1.7 | 1.4 | 1.0 | ns |

## Linux driver

None. The translator is transparent; the HAT EEPROM behind it uses `at24` (not part of this sheet).

## Simulation models available

None listed in `manifest.toml`. Whether TI publishes an IBIS model for this device is **UNVERIFIED**.

## Design notes for the T1

- VREF1 = 1.8 V and VDPU = 3.3 V meet the VREF2 ≥ VREF1 + 0.6 V rule (p. 5).
- **EN gating.** The BOM wants EN to isolate the HAT bus until HAT_DET#. Per Figure 9-2 (p. 18), the enable signal must be at the VDPU level (3.3 V) and drive the EN/VREF2 node through the 200 kΩ resistor; EN must be at least VREF1 + 0.6 V = 2.4 V to translate (§9.2.1). A 1.8 V GPIO cannot enable the part. The control net (a 3.3 V GPIO, the TCA6416A, or a 3.3 V signal derived from HAT_DET#) is not fixed in the BOM: **UNVERIFIED** design choice.
- When EN is low the HAT side is high-impedance (Cio(off) 6 pF maximum, p. 6) and the bus is lockup-free (§1, p. 1), which supports hot insertion (§8.1.4, p. 12): enable only when the HAT is powered and both buses are idle.
- The device adds no drive strength (§9.2.2.3, p. 19); pull-ups on the HAT side must be sized for the flat-cable and HAT capacitance.
- Operating range −40 to 85 °C (p. 5).

## Sources

- TI, *PCA9306 Dual Bidirectional I2C Bus and SMBus Voltage-Level Translator*, SCPS113O, revised September 2023, <https://www.ti.com/lit/ds/symlink/pca9306.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 94, §4.2
