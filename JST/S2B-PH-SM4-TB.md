# S2B-PH-SM4-TB(LF)(SN)

- **Manufacturer:** JST
- **Function:** 2-circuit, 2.0 mm pitch wire-to-board header, side entry, surface mount (PH series)
- **BOM v1 lines:** 47 (Power), battery connector mating the Adafruit 328 JST PHR-2 lead, status Proposed
- **BOM v1.5:** removed from line 47 by board ADR 0014; replaced by the Molex Micro-Fit 3.0 [43650-0400](../Molex/43650-0400.md). Kept for traceability.
- **Package:** SMT side-entry header, 2 contacts plus 2 tin-plated reinforcement tabs, 7.9 mm wide
- **Datasheet:** JST PH Connector catalog (2.0 mm pitch wire-to-board, crimp style), 5 pages, <https://www.jst-mfg.com/product/pdf/eng/ePH.pdf>; revision and date not printed (**UNVERIFIED**)
- **Status:** Partly UNVERIFIED

## Summary

The S2B-PH-SM4-TB is the 2-circuit side-entry SMT header of JST's PH series: 2.0 mm pitch, 2 A per contact with AWG #24 wire, 100 V, −40 to +105 °C (ePH p. 1, Specifications; p. 4, Header SMT type). In the T1 it is the only battery footprint and mates with the PHR-2 housing on the Adafruit 328 pack (BOM lines 46–47). Its per-contact rating sets the 2.0 A continuous battery current budget (power tree §4.7, finding 8).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| Current rating (AWG #24) | — | 2 | A AC/DC | ePH p. 1, Specifications |
| Voltage rating | — | 100 | V AC/DC | p. 1 |
| Temperature (including temperature rise from current) | −40 | +105 | °C | p. 1 |
| Withstanding voltage | 800 VAC for 1 min without breakdown | — | — | p. 1 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Contact resistance, initial | — | — | 10 | mΩ | ePH p. 1 |
| Contact resistance, after test | — | — | 20 | mΩ | p. 1 |
| Insulation resistance | 1000 | — | — | MΩ | p. 1 |
| Applicable wire (mating side) | AWG #32 | — | AWG #24 | — | p. 1 |
| Insulation O.D. (mating side) | 0.5 | — | 1.5 | mm | p. 1 |
| PCB thickness (stated for the series) | 0.8 | — | 1.6 | mm | p. 1 |

## Power by mode

Passive part. Loss per contact at 2 A: 2² × 10 mΩ = 40 mW initial, 80 mW at the 20 mΩ after-test limit (calculation).

## Pinout and package

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | circuit 1 | power | Battery contact (polarity set by the T1 schematic to match the pack lead; see Design notes) |
| 2 | circuit 2 | power | Battery contact |
| — | reinforcement ×2 | mechanical | Tin-plated copper-alloy hold-down tabs, soldered |

Dimensions (ePH p. 4, Header SMT side entry): A = 2.0 mm (contact pitch span), B = 7.9 mm (overall width), 1000 per reel. Posts and reinforcement copper alloy, tin-plated; housing PA (heat resistant), natural ivory; label (LF)(SN) (p. 4). Assembly drawing (p. 2): (9.6) mm depth and (5.5) mm reference dimensions on the side view, (2.6) mm from the reinforcement to the rear edge; the exact reference edges should be read from the drawing before the 3D model is drawn.

## Recommended footprint

JST PC board layout, SMT side-entry type (ePH p. 2, viewed from the mounting surface; dimensions for reference only):

- Signal pads: 1 mm minimum width, 2.0 ±0.05 mm pitch (non-accumulating).
- Reinforcement pads: 1.6 ±0.1 mm wide, 3.4 ±0.1 mm long, one each side; 1.5 ±0.1 mm from the outer signal pad centre line to the reinforcement pad (as dimensioned on the drawing).
- Overall pattern depth 9 mm minimum (signal pad far end to reinforcement pad far end); 5.5 mm maximum between the signal pad near end and the reinforcement pad far end; (0.2) mm reference offset of the reinforcement pads to the connector outline.

The drawing labels No. 1 circuit at the pad nearest the corner marked on the outline. Draw the KiCad footprint from the drawing itself; the figure above is a transcription.

## Application circuit and required passives

None of its own. The pack side uses PHR-2 housings and SPH-002T-P0.5S contacts for AWG #30 to #24 (ePH pp. 2–3).

## Interfaces and timing

Not applicable.

## Linux driver

None (passive part).

## Simulation models

None listed in `manifest.toml`. A JST 3D model is **UNVERIFIED** (not checked); ADR 0001 has OpenDAP generate its own.

## Design notes for the T1

- **Current rating applies to AWG #24.** The 2 A rating is stated with AWG #24 wire (p. 1). The Adafruit 328 lead is UL 26 AWG (pack sheet p. 10), and the catalog gives no rating for AWG #26, so 2 A through this header with the Adafruit lead is **UNVERIFIED**; the 2.0 A battery budget (power tree §4.7) should be treated as an upper bound until measured.
- **Temperature:** the −40 to +105 °C range includes the self-heating from current (p. 1). Contact loss at 2 A is 40–80 mW per contact (calculation).
- **Polarity:** JST does not define polarity; it comes from the pack. Adafruit's lead polarity is not in the pack sheet (**UNVERIFIED**). BOM line 47 requires a check on every lot; add a silkscreen mark for BAT+ and BAT− at the header.
- **Board thickness:** the catalog's 0.8–1.6 mm board thickness is stated for the series (p. 1), relevant to through-hole parts; for the SMT header it is not a stated constraint (**UNVERIFIED**).
- **Second source:** BOM line 47 lists the through-hole B2B-PH-K-S as an alternative (top entry, different footprint; p. 3).

## Sources

- JST, PH Connector catalog, 5 pages, <https://www.jst-mfg.com/product/pdf/eng/ePH.pdf>, sha256 `447624f4f2f7d37c58c1eaa7ee314ad757fe7aff48f6186491ef6f69fbc00b96` (manifest). Page numbers are the catalog's printed page numbers (‑1‑ to ‑5‑).
- Adafruit 328 pack sheet Q/WAPL785060-1011 p. 10 (lead gauge and connector).
- OpenDAP board BOM v1 lines 46–47 and power tree v0 §4.7 (T1 context).
