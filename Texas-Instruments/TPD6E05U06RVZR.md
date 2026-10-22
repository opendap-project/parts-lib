# TPD6E05U06RVZR

- **Manufacturer:** Texas Instruments
- **Function:** 6-channel unidirectional TVS ESD protection, ultra-low capacitance
- **BOM v1 lines:** 69 (HAT low-speed and analog lines at the pogo field, quantity 9), 73 (microSD CLK, CMD, D0–D3), 75 (faceplate low-speed lines, quantity 3)
- **Package:** USON-14 (RVZ)
- **Datasheet:** TPD1E05U06, TPD4E05U06, TPD6E05U06, SLVSBO7O (December 2012, revised August 2024), sha256 `c167cf1e72a5…` in `manifest.toml` (same document as the TPD4E05U06)
- **Status:** Not in the current BOM (replaced in BOM v1.1 by TPD4E05U06DQAR). Partly UNVERIFIED

## Summary

The TPD6E05U06 is the 6-channel member of the TPDxE05U06 family: unidirectional TVS diodes with 0.47 pF typical line capacitance and IEC 61000-4-2 level 4 rating (SLVSBO7O §1, §5.4, §6.3.4). In the T1 it protects the HAT low-speed and analog lines at the pogo field on the device-side piece (BOM v1 line 69, nine parts, 54 channels), the microSD CLK, CMD and D0–D3 lines (line 73) and the faceplate low-speed lines (I2C, SPI/DBI, INT/RST, TE, LED, PDM, detect, spares; line 75, three parts).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Electrical fast transient | IEC 61000-4-4 (5/50 ns), 25 °C | — | 80 | A | SLVSBO7O p. 6, Absolute Maximum Ratings |
| Peak pulse current | IEC 61000-4-5 (8/20 µs), 25 °C | — | 2.5 | A | p. 6 |
| Peak pulse power | IEC 61000-4-5 (8/20 µs), 25 °C | — | 40 | W | p. 6 |
| Ambient operating temperature, TA | — | −40 | 125 | °C | p. 6 |
| Storage temperature, Tstg | — | −65 | 155 | °C | p. 6 |
| ESD, HBM (RVZ) | ANSI/ESDA/JEDEC JS-001 | — | ±4000 | V | p. 6, §5.1 |
| ESD, CDM (RVZ) | JESD22-C101 | — | ±1500 | V | p. 6, §5.1 |
| ESD, IEC 61000-4-2 contact | — | — | ±12000 | V | p. 6, §5.2 |
| ESD, IEC 61000-4-2 air gap | — | — | ±15000 | V | p. 6, §5.2 |

The EFT rating was validated on the TPD4E05U06 only (§6.3.2, p. 12).

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
| Dynamic resistance, RDYN (RVZ) | I/O to GND and GND to I/O | — | 0.8 | — | Ω | p. 7 |
| Line capacitance, CL (RVZ) | VIO = 2.5 V, f = 1 MHz, I/O to GND, 25 °C | — | 0.47 | — | pF | p. 7 |
| Capacitance variation between channels | VBIAS = 2.5 V, f = 1 MHz | — | 0.05 | 0.07 | pF | p. 7 |
| Channel-to-channel capacitance | VBIAS = 2.5 V, f = 1 MHz | — | 0.01 | 0.06 | pF | p. 8 |

The device triggers above VBR or below the lower diode forward voltage (about −0.6 V) and reverts to passive within tens of nanoseconds after the event (§6.4, p. 12).

Thermal (RVZ): RθJA 197.9 °C/W, RθJC(top) 119.1 °C/W, RθJB 92.6 °C/W (p. 7, §5.3).

## Power by mode

Not applicable: passive device, no supply pin (§7.3, p. 16). Standby loss is the line leakage (10 nA maximum per line at 2.5 V).

## Pinout and package

USON-14 (RVZ), top view (Figure 4-4, Table 4-3, p. 5):

| Pin | Name | Type | Description |
|---|---|---|---|
| 14 | D1+ | I/O | ESD-protected channel |
| 13 | D1− | I/O | ESD-protected channel |
| 12 | D2+ | I/O | ESD-protected channel |
| 11 | D2− | I/O | ESD-protected channel |
| 9 | D3+ | I/O | ESD-protected channel |
| 8 | D3− | I/O | ESD-protected channel |
| 5, 10 | GND | Ground | Connect to ground |
| 1, 2, 3, 4, 6, 7 | NC | — | Not connected; for straight-through routing, may float or be grounded |

The "+/−" names are channel labels only; each channel is an independent single-ended clamp to GND (Figure 6-3, p. 11).

Package dimensions: **UNVERIFIED.** SLVSBO7O revised August 2024 contains outline drawings for DQA, DYA and DPY only (pp. 24–36); no RVZ outline, land pattern or stencil is included, although the RVZ orderables are active (package option addendum, p. 37; tape and reel data, pp. 20–21). The RVZ0014 drawing must be obtained separately from TI before the footprint is drawn. NiPdAu finish, MSL Level-1-260C-UNLIM, reel of 3000 (p. 37).

## Recommended footprint

**UNVERIFIED**: not in SLVSBO7O (see above). Do not derive the footprint from the tape cavity dimensions.

## Application circuit and required passives

No passives. Each protected line passes straight across a D pin and the NC pin opposite it (flow-through, §6.3.9, p. 12), and the device shunts to GND.

## Interfaces and timing

Not applicable (no logic interface). Line capacitance 0.47 pF typical; the family supports data rates up to 6 Gb/s (§6.3.4, p. 12).

## Linux driver

None (passive part).

## Simulation models

None listed in `manifest.toml`. Whether TI publishes an IBIS or SPICE model for this device is **UNVERIFIED**.

## Design notes for the T1

- Place as close to the connector as possible, keep unprotected traces away from the protected section, route protected traces straight with rounded corners (§7.4.1, p. 16).
- VRWM is 5.5 V and VIO must stay within 0–5.5 V (pp. 6–7). All T1 lines on this part are 3.3 V or 1.8 V logic (microSD 1.8/3.3 V, faceplate bank 3.3 V, HAT low-speed 3.3 V).
- The part is unidirectional: a line driven below about −0.6 V conducts into the GND-to-I/O diode (§6.4). The six HAT analog lines on line 69 (line out, line in) are fine only if they never swing below ground; if they are AC-coupled bipolar signals, a bidirectional part is needed (BOM v1 line 69 note, **UNVERIFIED**).
- On microSD (line 73) the 0.47 pF load keeps UHS-I SDR104 edges (BOM v1 line 73).
- Second option in the BOM is TPD4E05U06 in DQA, whose drawings are in the same datasheet (line 69: ×13; line 73: ×2; line 75: ×5).

## Sources

- TI, *TPDxE05U06 1, 4, 6 Channel ESD Protection Device for Super-Speed (Up to 6 Gbps) Interface*, SLVSBO7O, revised August 2024, <https://www.ti.com/lit/ds/symlink/tpd6e05u06.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 69, 73, 75
