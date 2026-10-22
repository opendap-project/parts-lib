# BAT54

- **Manufacturer:** Nexperia
- **Function:** Single Schottky barrier diode, 30 V, 200 mA
- **BOM v1 lines:** 78 (MaskROM combo, PWRON isolation diode)
- **BOM v1.6:** the PWRON_N pull-up goes from 20 kΩ to 100 kΩ: pressed level 261 mV at −20 °C against the 350 mV SN74LVC1G57 VT− minimum (89 mV margin) ([boost and MaskROM simulation](https://github.com/opendap-project/board/blob/main/docs/research/2026-10-boost-and-maskrom-simulation.md) §5.4).
- **Package:** SOT23 (TO-236AB), 2.9 × 1.3 × 1 mm body; ordered as BAT54,215
- **Datasheet:** BAT54 Schottky barrier diode, product data sheet BAT54 v.6 (1 July 2022). Obtained from the LCSC mirror of the Nexperia document, sha256 `40b7447c4bbe3a9153d07a28620275322e1b4a7375c89de312d1f4b8c7325847`. The manifest URL (assets.nexperia.com) refused the download in this session.
- **Status:** Partly UNVERIFIED

## Summary

The BAT54 is a planar Schottky barrier diode with an integrated guard ring in SOT23 (BAT54 v.6 §1, p. 1). In the T1 it isolates the RK809 PWRON node from the MaskROM combo logic: cathode on PWRON, anode on the In2 input of the SN74LVC1G57 configured as a NOR (BOM v1.1 line 98; it replaced the SN74LVC1G27), which has a pull-up to vcca1v8_pmu (BOM v1 line 78). The ",215" suffix is Nexperia's packing code. v.6 removed packing information (Revision history, p. 8), so the ",215" reel details are **UNVERIFIED** from this document.

## Absolute maximum ratings

Limiting values per IEC 60134 (BAT54 v.6 Table 5, p. 3).

| Parameter | Symbol | Condition | Min | Max | Unit |
|---|---|---|---|---|---|
| Reverse voltage | VR | — | — | 30 | V |
| Forward current | IF | Tamb = 25 °C | — | 200 | mA |
| Repetitive peak forward current | IFRM | tp ≤ 1 s, δ ≤ 0.5, Tamb = 25 °C | — | 300 | mA |
| Non-repetitive peak forward current | IFSM | tp < 10 ms, Tj(init) = 25 °C | — | 600 | mA |
| Total power dissipation | Ptot | Tamb ≤ 25 °C, FR4, standard footprint | — | 250 | mW |
| Junction temperature | Tj | — | — | 150 | °C |
| Ambient temperature | Tamb | — | −55 | 150 | °C |
| Storage temperature | Tstg | — | −65 | 150 | °C |

Thermal resistance junction to ambient, Rth(j-a): 500 K/W maximum, FR4, standard footprint (Table 6, p. 3).

## Recommended operating conditions

The datasheet has no recommended operating conditions table. Characteristics at Tamb = 25 °C, pulsed (tp ≤ 300 µs, δ ≤ 0.02) (Table 7, p. 4):

| Parameter | Condition | Max | Unit |
|---|---|---|---|
| Forward voltage, VF | IF = 0.1 mA | 240 | mV |
| Forward voltage, VF | IF = 1 mA | 320 | mV |
| Forward voltage, VF | IF = 10 mA | 400 | mV |
| Forward voltage, VF | IF = 30 mA | 500 | mV |
| Forward voltage, VF | IF = 100 mA | 800 | mV |
| Reverse current, IR | VR = 25 V | 2 | µA |
| Diode capacitance, Cd | VR = 1 V, f = 1 MHz | 10 | pF |
| Reverse recovery time, trr | IF = IR = 10 mA, IR(meas) = 1 mA, RL = 100 Ω | 5 | ns |

Typical forward and reverse curves at 25, 85 and 125 °C are in Fig. 1 and Fig. 2 (p. 4); capacitance against VR in Fig. 3 (p. 5).

## Power by mode

Not applicable (discrete diode). In the T1 the steady-state loss is the reverse leakage while PWRON is high and the pull-up current while PWRON is pressed (set by the pull-up value, not by the diode).

## Pinout and package

Pinning (Table 2, p. 2):

| Pin | Symbol | Description |
|---|---|---|
| 1 | A | Anode |
| 2 | n.c. | Not connected |
| 3 | K | Cathode |

SOT23, 1.9 mm lead pitch, body 2.8–3.0 × 1.2–1.4 mm, height 0.9–1.1 mm, overall width across leads 2.1–2.5 mm (Fig. 5, p. 6). Marking code `L4%`, where `%` is the manufacturing-site code (Table 4, p. 2).

## Recommended footprint

Reflow soldering footprint for SOT23 (Fig. 6, p. 7, `sot023_fr`):

- Solder lands 0.6 mm (x) × 0.7 mm (y), 3×; paste openings 0.5 mm wide, 3×; solder-resist openings 0.6 mm, 3×.
- Pins 1 and 2 at 1.9 mm pitch (basic); pin 3 centred opposite them, 2 mm row-to-row (basic).
- Occupied area 3.3 × 3 mm; the other labelled outlines are 2.9 mm, 1.7 mm and 1 mm.

A wave-soldering footprint is in Fig. 7 (p. 7) and is not used in the T1.

## Application circuit and required passives

No passives belong to the diode itself. In the T1 circuit (BOM v1 line 78) the NOR-input pull-up to vcca1v8_pmu sets the diode current when PWRON is pulled low. Its value is set in the schematic.

## Interfaces and timing

Not applicable. Switching figure: trr ≤ 5 ns (Table 7, p. 4).

## Linux driver

None.

## Simulation models

None listed in `manifest.toml`. Whether Nexperia publishes a SPICE model for BAT54 is **UNVERIFIED** (not checked; the Nexperia site refused requests in this session).

## Design notes for the T1

- Isolation function: when PWRON is pressed (low), the diode conducts and pulls the NOR input to about VF above PWRON. At the µA–mA currents set by a pull-up from 1.8 V, VF max is 240 mV at 0.1 mA and 320 mV at 1 mA (Table 7, p. 4). The SN74LVC1G57 negative-going threshold at 1.8 V supply must be checked against PWRON-low + VF (see [its sheet](../Texas-Instruments/SN74LVC1G57DCKR.md)).
- When PWRON is released, the diode must stay off: the RK809 PWRON idle voltage must be at or above the NOR input's pull-up level minus a few hundred mV. The BOM marks the RK809 PWRON idle voltage **UNVERIFIED**. If it is well below 1.8 V, the diode forward-biases at idle, the NOR sees a low input and the combo logic is defeated (BOM v1 line 78 note).
- Reverse leakage at 25 V is ≤ 2 µA at 25 °C (Table 7). At the ≤ 1.8 V reverse bias in this circuit it is lower, but it rises with temperature (Fig. 2, p. 4). Size the pull-up so the leakage at 85 °C cannot pull the NOR input below VIH. The 85 °C value at 1.8 V is not tabulated, only plotted (**UNVERIFIED** numeric value).
- v.6 states the product moved to non-automotive qualification (p. 8); no impact for the T1.

## Sources

- Nexperia, *BAT54 Schottky barrier diode*, product data sheet v.6, 1 July 2022 (manifest URL <https://assets.nexperia.com/documents/data-sheet/BAT54_SER.pdf>; copy fetched from the LCSC mirror for C85084)
- OpenDAP board, `docs/specs/bom-v1.md`, lines 78, 97, 98
