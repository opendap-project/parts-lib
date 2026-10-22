# TPD4E1U06

- **Manufacturer:** Texas Instruments
- **Function:** 4-channel unidirectional TVS ESD protection, 0.8 pF
- **Package:** SC70-6 (DCK, TPD4E1U06DCKR) or SOT-23-6 (DBV, TPD4E1U06DBVR); the T1 has not picked an orderable
- **Datasheet:** TPD4E1U06, TPD4E1U06-G4, SLVSBQ9E (December 2012, revised October 2026), sha256 `aaf78b3eda25…` in `manifest.toml`
- **BOM v1:** §4.1 (ESD capacitance budget, CSI-2 row); no BOM line of its own

## Summary

The TPD4E1U06 is a quad-channel unidirectional TVS diode array with 0.8 pF typical line capacitance and IEC 61000-4-2 level 4 rating (SLVSBQ9E §1, §3, p. 1). BOM v1 §4.1 evaluates it for the HAT CSI-2 D-PHY lines (0.8 pF, 11 % of the unit interval) and keeps the TPD4E05U06 instead for one part number. It is therefore an alternative to BOM v1 line 68, not a fitted part.

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| EFT | IEC 61000-4-4 (5/50 ns) | — | 80 | A | SLVSBQ9E p. 4, §5.1 |
| Peak pulse current, IPP | IEC 61000-4-5 (8/20 µs) | — | 3 | A | p. 4 |
| Peak pulse power, PPP | IEC 61000-4-5 (8/20 µs) | — | 45 | W | p. 4 |
| Operating temperature | — | −40 | 125 | °C | p. 4 |
| Storage temperature, Tstg | — | −65 | 115 | °C | p. 4 |
| ESD, HBM, all pins | JS-001 | — | ±4000 | V | p. 4, §5.2 |
| ESD, CDM, all pins | JESD22-C101 | — | ±1500 | V | p. 4, §5.2 |
| ESD, IEC 61000-4-2 contact / air gap | — | — | ±15000 | V | p. 4, §5.3 |

## Recommended operating conditions

| Parameter | Min | Max | Unit | Reference |
|---|---|---|---|---|
| Input pin voltage, VIO | 0 | 5.5 | V | p. 4, §5.4 |
| Operating free-air temperature, TA | −40 | 125 | °C | p. 4, §5.4 |

### Electrical characteristics

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| Reverse stand-off voltage, VRWM | IIO = 10 µA | — | — | 5.5 | V | p. 5, §5.6 |
| Clamp, I/O to GND | IPP = 1 A, 8/20 µs | — | 11 | — | V | p. 5 |
| Clamp, I/O to GND | IPP = 3 A, 8/20 µs | — | 15 | — | V | p. 5 |
| Dynamic resistance, pin to GND / GND to pin | — | — | 1.0 / 0.6 | — | Ω | p. 5 |
| Line capacitance, CL | f = 1 MHz, VBIAS = 2.5 V, 25 °C | — | 0.8 | 1 | pF | p. 5 |
| Channel-to-channel capacitance, DCK / DBV | f = 1 MHz, VBIAS = 2.5 V | — | 0.006 / 0.01 | 0.015 / 0.025 | pF | p. 5 |
| Breakdown voltage, VBR | IIO = 1 mA | 6.5 | — | 8.5 | V | p. 5 |
| Leakage, ILEAK | VIO = 2.5 V | — | 1 | 10 | nA | p. 5 |

Thermal: RθJA 274.3 °C/W (DCK), 224.3 °C/W (DBV) (p. 4, §5.5).

## Power by mode

Not applicable: passive device, no supply pin.

## Pinout and package

DCK and DBV share one pinout (Table 4-1, p. 3):

| Pin | Name | Type | Description |
|---|---|---|---|
| 1 | D1+ | I/O | ESD-protected channel, close to the connector |
| 2 | GND | GND | Ground |
| 3 | D2+ | I/O | ESD-protected channel |
| 4 | D2− | I/O | ESD-protected channel |
| 5 | NC | I/O | No connect; may float, be grounded or tied to VCC |
| 6 | D1− | I/O | ESD-protected channel |

Outline DCK0006A (drawing 4214835/D 11/2024, PDF p. 20): body 1.1–1.4 × 1.85–2.15 mm, 1.8–2.4 mm over leads, 1.1 mm maximum height, 0.65 mm pitch. DBV0006A (SOT-23-6, 1.45 mm maximum height) drawings are on PDF pp. 17–19. Reels of 3000 (package option addendum, p. 14).

## Recommended footprint / land pattern

DCK0006A example board layout (PDF p. 21): six pads 0.9 × 0.4 mm (reference), 0.65 mm pitch, 2.2 mm (reference) pad-row spacing; non-solder-mask-defined preferred, 0.07 mm maximum clearance. DBV0006A land pattern on PDF p. 18.

## Application circuit and required passives

No passives. Data lines pass the D pins; GND pin to the ground plane (simplified schematic, p. 1; layout guidelines §7.4.1, p. 11).

## Interfaces and timing

Not applicable (no logic interface).

## Linux driver

None (passive part).

## Simulation models available

None listed in `manifest.toml`. IBIS or SPICE availability is **UNVERIFIED**.

## Design notes for the T1

- 0.8 pF typical, 1 pF maximum (p. 5). BOM v1 §4.1 rates 1.0 pF as marginal on 5 Gb/s lines, so this part fits CSI-2 and USB 2.0 but not the HAT USB 3 or PCIe pairs.
- A leaded SC70 or SOT-23 package differs from the USON footprint of the TPD4E05U06; it is not a drop-in substitute on line 68.

## Sources

- TI, *TPD4E1U06 Quad-Channel, High-Speed ESD Protection Device*, SLVSBQ9E, revised October 2026, <https://www.ti.com/lit/ds/symlink/tpd4e1u06.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, §4.1 and line 68
