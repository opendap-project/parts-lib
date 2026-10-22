# TPD1E04U04DPYR

- **Manufacturer:** Texas Instruments
- **Function:** 1-channel unidirectional TVS ESD protection diode, 0.5 pF, low RDYN (snapback)
- **BOM v1 lines:** 68 (second source: per-line HAT high-speed ESD at the pogo field)
- **Package:** X1SON-2 (DPY), 1.0 × 0.6 mm (0402)
- **Datasheet:** TPD1E04U04, SLVSDG4B (March 2016, revised August 2016), sha256 `f48a05822f3f…` in `manifest.toml`
- **Status:** Partly UNVERIFIED

## Summary

The TPD1E04U04 is a single-channel unidirectional ESD diode for high-speed interfaces up to 6 Gb/s, with 0.5 pF typical line capacitance and an 8.9 V clamp at 16 A TLP (SLVSDG4B §1, §3, p. 1). In the T1 BOM it is the per-line second source for the HAT high-speed ESD at the pogo field (BOM v1 line 68), in place of the 4-channel TPD4E05U06.

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Electrical fast transient | IEC 61000-4-4 (5/50 ns) | — | 80 | A | SLVSDG4B p. 4, §6.1 |
| Peak pulse power, DPY | IEC 61000-4-5 (8/20 µs) | — | 19 | W | p. 4 |
| Peak pulse current | IEC 61000-4-5 (8/20 µs) | — | 2.5 | A | p. 4 |
| Operating free-air temperature, TA | — | −40 | 125 | °C | p. 4 |
| Storage temperature, Tstg | — | −65 | 155 | °C | p. 4 |
| ESD, HBM | JS-001 | — | ±2500 | V | p. 4, §6.2 |
| ESD, CDM | JESD22-C101 | — | ±1000 | V | p. 4, §6.2 |
| ESD, IEC 61000-4-2 contact | — | — | ±16000 | V | p. 4, §6.3 |
| ESD, IEC 61000-4-2 air gap | — | — | ±16000 | V | p. 4, §6.3 |

## Recommended operating conditions

| Parameter | Min | Max | Unit | Reference |
|---|---|---|---|---|
| Input pin voltage, VIO | 0 | 3.6 | V | p. 4, §6.4 |
| Operating free-air temperature, TA | −40 | 125 | °C | p. 4, §6.4 |

### Electrical characteristics

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| Reverse stand-off voltage, VRWM | IIO < 10 nA | — | — | 3.6 | V | p. 5, §6.6 |
| Breakdown voltage, VBR (before snapback) | 25 °C | 4.5 | 6.2 | 7.5 | V | p. 5 |
| Holding voltage, VHOLD | IIO = 1 mA | — | 5.3 | — | V | p. 5 |
| Forward voltage, GND to IO | 1 mA, 25 °C | — | 0.8 | — | V | p. 5 |
| Clamp, IO to GND | 1 A / 16 A TLP | — | 5.3 / 8.9 | — | V | p. 5 |
| Clamp, GND to IO | 1 A / 16 A TLP | — | 1.3 / 4.6 | — | V | p. 5 |
| Leakage, ILEAK | VIO = 2.5 V | — | 0.1 | 10 | nA | p. 5 |
| Dynamic resistance, IO to GND / GND to IO | — | — | 0.25 / 0.18 | — | Ω | p. 5 |
| Line capacitance, CL | VIO = 0 V, 1 MHz, 25 °C | — | 0.5 | 0.65 | pF | p. 5 |

Thermal (DPY): RθJA 683.6 °C/W (p. 4, §6.5).

## Power by mode

Not applicable: passive device, no supply pin (§9, p. 13).

## Pinout and package

X1SON-2 (DPY) (Pin Functions, p. 3): pin 1 IO (ESD-protected channel), pin 2 GND.

Outline DPY0002A (drawing 4224561/C 07/2024, PDF p. 21): body 0.9–1.1 × 0.5–0.7 mm, 0.30–0.45 mm height, terminal pitch 0.65 mm. MSL Level-1-260C, reel of 10 000 (package option addendum, p. 16).

## Recommended footprint

DPY0002A example board layout (PDF p. 22): two pads 0.3 × 0.5 mm (reference) at 0.7 mm centre-to-centre; solder-mask-defined preferred, 0.07 mm minimum overlap. Same drawing and land pattern as the TPD1E10B06DPYR.

## Application circuit and required passives

No passives. One part per line, IO on the signal, GND pin to the ground plane (typical application, p. 1; layout guidelines §10.1, p. 13).

## Interfaces and timing

Not applicable (no logic interface).

## Linux driver

None (passive part).

## Simulation models

None listed in `manifest.toml`. IBIS or SPICE availability is **UNVERIFIED**.

## Design notes for the T1

- VRWM is 3.6 V (p. 5), lower than the TPD4E05U06 (5.5 V). Fine for USB 3, PCIe and CSI-2 differential lines; not for any line that can sit above 3.6 V.
- The device snaps back to a 5.3 V holding voltage (p. 5 note 1); it must not be placed on a DC rail that can exceed the holding voltage.
- Using it on line 68 multiplies part count (one per line instead of four per part) and changes the footprint; the board must be laid out for one option.

## Sources

- TI, *TPD1E04U04 1-Channel ESD Protection Diode with Low RDYN for HDMI 2.0 and USB 3.0*, SLVSDG4B, revised August 2016, <https://www.ti.com/lit/ds/symlink/tpd1e04u04.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 68
