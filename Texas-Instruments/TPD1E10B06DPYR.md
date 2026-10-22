# Texas Instruments TPD1E10B06DPYR

- **BOM v1 lines:** 36 (Audio, headphone output and detect-line ESD), quantity 8; 74 (Protection, button ESD: Power, Action, Vol+, Vol−), quantity 4
- **Datasheet:** TI TPD1E10B06 Single-Channel ESD Protection Diode, SLLSEB1G, February 2012, revised August 2024, 33 pages (cited as "SLLSEB1G"); sha256 in `manifest.toml`
- **Package:** DPY, 2-pin X1SON, 1.0 × 0.6 mm (0402)

## Summary

A single-channel bidirectional TVS diode (back-to-back structure) with ±5.5 V working voltage, 12 pF typical capacitance and IEC 61000-4-2 ±30 kV contact protection (SLLSEB1G p. 1). TI lists audio lines among its applications (p. 1, §7.2). In the T1, eight parts protect the headphone outputs (L±, R± on the 4.4 mm jack; L, R on the 3.5 mm jack) and the two jack-detect lines (BOM v1 line 36). Four more protect the buttons (BOM v1 line 74). Bidirectional because the outputs swing ±4 V.

## Absolute maximum ratings

SLLSEB1G §5.1–5.3, p. 4.

| Parameter | Min | Max | Unit | Condition |
|---|---|---|---|---|
| Peak pulse power | — | 90 | W | IEC 61000-4-5, 8/20 µs, 25 °C |
| Peak pulse current | — | 6 | A | IEC 61000-4-5, 8/20 µs, 25 °C |
| Operating free-air temperature | −40 | 125 | °C | — |
| Storage temperature | −65 | 155 | °C | — |
| ESD HBM (DPY) | — | ±2500 | V | ANSI/ESDA/JEDEC JS-001 |
| ESD CDM (DPY) | — | ±1000 | V | JESD22-C101 |
| IEC 61000-4-2 contact | — | ±30 | kV | All pins |
| IEC 61000-4-2 air gap | — | ±30 | kV | All pins |

## Recommended operating conditions

SLLSEB1G §5.4, p. 4.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| Operating voltage, pin 1 to 2 or 2 to 1 | −5.5 | 5.5 | V |
| Operating free-air temperature | −40 | 125 | °C |

Electrical characteristics (SLLSEB1G §5.6, p. 5):

| Parameter | Typ | Max | Unit | Condition |
|---|---|---|---|---|
| VRWM | — | 5.5 | V | Either direction |
| Leakage | — | 100 | nA | Pin 1 = 5 V, pin 2 = 0 V |
| Clamp, pin 1 struck | 10 | — | V | IPP = 1 A, 8/20 µs |
| Clamp, pin 1 struck | 14 | — | V | IPP = 5 A, 8/20 µs |
| Clamp, pin 2 struck | 8.5 / 14 | — | V | IPP = 1 A / 5 A |
| RDYN | 0.32 (1→2), 0.38 (2→1) | — | Ω | TLP 10–20 A |
| CIO | 12 | — | pF | VIO = 2.5 V, 1 MHz |
| VBR, either direction | min 6 | — | V | IIO = 1 mA |

The clamp values are listed in the TYP column position of the table extraction (**UNVERIFIED** whether TYP or MAX; p. 1 states "10 V clamping voltage (maximum at IPP = 1 A)").

Thermal (SLLSEB1G §5.5, p. 4), DPY: RθJA 615.5 °C/W.

## Power by mode

Passive device, no supply. Standby loss is leakage only, ≤ 100 nA at 5 V (SLLSEB1G p. 5, §7.3 p. 10).

## Pinout and package

| Pin | Function |
|---|---|
| 1 | ESD-protected I/O; connect the other pin to GND (symmetric device) |
| 2 | ESD-protected I/O / GND |

SLLSEB1G §4, Table 4-1, p. 3. DPY0002A outline (SLLSEB1G p. 19): body 0.9–1.1 × 0.5–0.7 mm, height 0.30–0.45 mm, pads 0.2–0.3 × 0.45–0.55 mm at 0.65 mm pitch; optional pin-1 chamfer.

## Recommended footprint / land pattern

DPY0002A example board layout (SLLSEB1G p. 20): two pads 0.3 × 0.5 mm, centre-to-centre 0.7 mm, corner radius 0.05 mm; solder-mask-defined preferred (mask 0.07 mm min inside metal), or non-solder-mask-defined with 0.07 mm max opening around metal. Stencil on p. 21.

## Application circuit and required passives

No passives. One device per line between the signal and GND, as close to the connector as possible (SLLSEB1G §7.4.1, p. 11; Figure 7-1, p. 9 shows L/R audio lines to a class-AB amplifier). Thick, short return path to GND (Figure 7-4, p. 11).

## Interfaces and timing

12 pF typical gives a 3 dB bandwidth of about 400 MHz per TI (SLLSEB1G §7.2.2, p. 10); far above audio. Pin capacitance varies with bias (Figure 5-8, p. 7, curve not transcribed).

## Linux driver

None (passive protection device).

## Simulation models available

None listed in `manifest.toml`. TI SPICE/IBIS for this part: **UNVERIFIED** (not searched).

## Design notes for the T1

- The OPA1622 output swing (±4 V per BOM line 36) stays inside the ±5.5 V VRWM.
- The BOM places the diode after the OPA1622 feedback node so the loop corrects its voltage-dependent capacitance; this conflicts with TI's "as close to the connector as possible" (SLLSEB1G §7.4.1). Resolve placement in layout: the feedback tap can still be taken at the connector side of any ballast resistor while the TVS sits near the jack (**UNVERIFIED**, design choice not yet made).
- Detect lines are logic level and see positive voltage only; a bidirectional part is acceptable there.

## Sources

- TI SLLSEB1G, TPD1E10B06, revised August 2024: §4 p. 3, §5.1–5.6 pp. 4–5, §7.2–7.4 pp. 9–11, DPY0002A pp. 19–21. <https://www.ti.com/lit/ds/symlink/tpd1e10b06.pdf>
- Board BOM v1, line 36.
