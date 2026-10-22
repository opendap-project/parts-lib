# TPD4E05U06DQAR

- **Manufacturer:** Texas Instruments
- **Function:** 4-channel unidirectional TVS ESD protection, ultra-low capacitance
- **Package:** USON-10 (DQA), 2.5 × 1.0 mm, 0.5 mm pitch
- **Datasheet:** TPD1E05U06, TPD4E05U06, TPD6E05U06, SLVSBO7O (December 2012, revised August 2024), sha256 `c167cf1e72a5…` in `manifest.toml`
- **BOM v1 lines:** 62, 68, 72

## Summary

The TPD4E05U06 is a 4-channel unidirectional TVS diode array for high-speed lines, with 0.5 pF typical line capacitance and IEC 61000-4-2 level 4 rating (SLVSBO7O §1, §5.4). In the T1 it protects the main USB-C D+/D− pair (BOM v1 line 62), the HAT high-speed pairs at the user-touchable pogo field on the device-side piece (line 68, six parts) and the faceplate MIPI DSI clock and data lanes (line 72, three parts).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Electrical fast transient | IEC 61000-4-4 (5/50 ns), 25 °C | — | 80 | A | SLVSBO7O p. 6, Absolute Maximum Ratings |
| Peak pulse current | IEC 61000-4-5 (8/20 µs), 25 °C | — | 2.5 | A | p. 6 |
| Peak pulse power | IEC 61000-4-5 (8/20 µs), 25 °C | — | 40 | W | p. 6 |
| Ambient operating temperature, TA | — | −40 | 125 | °C | p. 6 |
| Storage temperature, Tstg | — | −65 | 155 | °C | p. 6 |
| ESD, HBM (DQA) | ANSI/ESDA/JEDEC JS-001 | — | ±4000 | V | p. 6, §5.1 |
| ESD, CDM (DQA) | JESD22-C101 | — | ±1500 | V | p. 6, §5.1 |
| ESD, IEC 61000-4-2 contact | — | — | ±12000 | V | p. 6, §5.2 |
| ESD, IEC 61000-4-2 air gap | — | — | ±15000 | V | p. 6, §5.2 |

## Recommended operating conditions

| Parameter | Min | Max | Unit | Reference |
|---|---|---|---|---|
| Input pin voltage, VIO | 0 | 5.5 | V | p. 6, Recommended Operating Conditions |
| Operating free-air temperature, TA | −40 | 125 | °C | p. 6 |

### Electrical characteristics

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| Reverse stand-off voltage, VRWM | IIO < 10 µA | — | — | 5.5 | V | p. 7, §5.4 |
| Breakdown voltage, VBR | IIO = 1 mA | 6.5 | — | 8.5 | V | p. 7 |
| Clamp voltage, I/O to GND | IPP = 1 A, TLP | — | 10 | — | V | p. 7 |
| Clamp voltage, I/O to GND | IPP = 5 A, TLP | — | 14 | — | V | p. 7 |
| Clamp voltage, GND to I/O | IPP = 1 A, TLP | — | 3 | — | V | p. 7 |
| Clamp voltage, GND to I/O | IPP = 5 A, TLP | — | 7 | — | V | p. 7 |
| Leakage current, ILEAK | VIO = 2.5 V | — | 0.01 | 10 | nA | p. 7 |
| Dynamic resistance, RDYN (DQA) | I/O to GND and GND to I/O | — | 0.8 | — | Ω | p. 7 |
| Line capacitance, CL (DQA) | VIO = 2.5 V, f = 1 MHz, I/O to GND, 25 °C | — | 0.5 | — | pF | p. 7 |
| Capacitance variation between channels | VBIAS = 2.5 V, f = 1 MHz | — | 0.05 | 0.07 | pF | p. 7 |
| Channel-to-channel capacitance | VBIAS = 2.5 V, f = 1 MHz | — | 0.01 | 0.06 | pF | p. 8 |

Thermal: RθJA 327 °C/W, RθJC(top) 189.5 °C/W, RθJB 257.7 °C/W for DQA (p. 7, §5.3).

## Power by mode

Not applicable: passive device, no supply pin (§7.3, p. 16). Standby loss is the line leakage above (10 nA maximum per line at 2.5 V).

## Pinout and package

USON-10 (DQA), top view (Figure 4-3, Table 4-2, p. 4):

| Pin | Name | Type | Description |
|---|---|---|---|
| 1 | D1+ | I/O | ESD-protected channel |
| 2 | D1− | I/O | ESD-protected channel |
| 3 | GND | Ground | Connect to ground |
| 4 | D2+ | I/O | ESD-protected channel |
| 5 | D2− | I/O | ESD-protected channel |
| 6, 7, 9, 10 | NC | — | Not connected; for straight-through routing, may float or be grounded |
| 8 | GND | Ground | Connect to ground |

Body 2.4–2.6 × 0.9–1.1 mm, 0.55 mm maximum height, 0.5 mm pitch (outline DQA0010A, drawing 4220328/A, p. 28). The datasheet also carries a second outline, DQA0010B (drawing 4230307/A, p. 31), with the same body limits. Which outline a reel ships in is **UNVERIFIED**. MSL Level-1-260C-UNLIM, NiPdAu finish (package option addendum, p. 37). Reel: 3000 units (p. 37).

## Recommended footprint / land pattern

DQA0010A example board layout (p. 29, drawing 4220328/A, scale 30:1):

- 10 pads, pad length 0.565 mm (reference), 0.5 mm pitch along each side, column pitch 0.835 mm (reference).
- Signal pads 0.2 mm wide (8×); the two centre GND pads 0.4 mm wide (2×).
- Non-solder-mask-defined pads preferred, 0.07 mm maximum mask clearance all around.
- Stencil: example on p. 30 (0.1 mm stencil).

DQA0010B has its own land pattern (p. 32) and stencil (p. 33); the KiCad footprint must be checked against both outlines before release.

## Application circuit and required passives

No passives. The protected line passes straight across the pad pair (flow-through), and the device shunts to GND (Figure 7-11, p. 17). Each part protects two differential pairs (D1±, D2±).

## Interfaces and timing

Not applicable (no logic interface). Signal-integrity data: line capacitance 0.5 pF typical, intended for interfaces up to 6 Gb/s (SLVSBO7O title and §3, p. 1).

## Linux driver

None (passive part).

## Simulation models available

None listed in `manifest.toml`. Whether TI publishes an IBIS or SPICE model for this device is **UNVERIFIED**.

## Design notes for the T1

- Place each part as close to its connector as possible and keep unprotected traces away from the protected section between the TVS and the connector (§7.4.1, p. 16; Table 4-2 note 2).
- Route the protected traces straight through the NC-paired pads, with rounded corners (§7.4.1, p. 16; Figure 7-11, p. 17). Each GND pad gets its own via to the ground plane (Figure 7-11).
- VRWM is 5.5 V (p. 7). USB D+/D− (line 62), DSI (line 72) and the HAT high-speed pairs (line 68) all stay well below that.
- The 0.5 pF line capacitance is the figure used in the BOM v1 §4.1 budget for 5 Gb/s USB 3 and PCIe Gen 2 (≈ 25 ps added edge). Per BOM line 68, only one ESD stage is fitted per HAT high-speed line (at the pogo field), so the capacitance is not doubled.
- The part is unidirectional: a line that swings below GND conducts through the GND-to-I/O diode at about 3 V clamp (1 A TLP, p. 7). It is not used on the analog headphone or HAT audio lines.

## Sources

- TI, *TPDxE05U06 1, 4, 6 Channel ESD Protection Device for Super-Speed (Up to 6 Gbps) Interface*, SLVSBO7O, revised August 2024, <https://www.ti.com/lit/ds/symlink/tpd4e05u06.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 62, 68, 72 and §4.1
