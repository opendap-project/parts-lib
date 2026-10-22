# USB4105-GF-A

- **Manufacturer:** GCT (Global Connector Technology)
- **Function:** USB Type-C receptacle for USB 2.0, SMT, PCB top mount
- **Package:** 16 signal contacts plus 4 shell stakes, 8.94 × 7.35 mm footprint outline
- **Datasheet:** USB4105 product drawing, revision B4, dated 18/12/23 (drawing date 4 October 2019), 2 sheets, sha256 `fb331fbabee8…` in `manifest.toml`
- **BOM v1 line:** 61

## Summary

The USB4105 is a USB 2.0 Type-C receptacle with 16 signal contacts (no SuperSpeed pairs) and a stainless-steel shell, rated 5 A on VBUS and 48 V DC (drawing sheet 1, Specifications). In the T1 it is the main USB-C port for USB 2.0 OTG and USB Power Delivery (BOM v1 line 61). The `-GF-A` suffix selects gold-flash contact plating, tape-and-reel packing and the default 0.95 mm shell stake length (sheet 1, Ordering Grid).

## Absolute maximum ratings

The drawing gives ratings, not absolute maxima.

| Parameter | Value | Reference |
|---|---|---|
| Current rating, VBUS pins collectively | 5.00 A | Sheet 1, Specifications, Electrical |
| Current rating, GND pins collectively | 6.25 A | Sheet 1 |
| Current rating, A5/B5 (CC) pin | 1.25 A | Sheet 1 |
| Current rating, every other pin | 0.25 A per pin | Sheet 1 |
| Voltage rating | 48 V DC | Sheet 1 |
| Power rating | 240 W | Sheet 1 |
| Dielectric withstanding voltage | 100 V AC | Sheet 1 |
| Contact resistance | 40 mΩ maximum initial; 50 mΩ maximum after test | Sheet 1 |
| Insulation resistance | 100 MΩ minimum | Sheet 1 |

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Operating temperature | −40 to +85 °C | Sheet 1, Mechanical & Environmental |
| Mating force | 5 to 20 N | Sheet 1 |
| Unmating force | 6 to 20 N after test | Sheet 1 |
| Durability | 20,000 cycles | Sheet 1 |

Materials: LCP insulator (UL 94V-0, black), copper-alloy contacts, stainless-steel shell and mid plate. Plating: gold flash on the solder tails over 50 µin minimum nickel; shell 30 µin minimum nickel (sheet 1, Material and Plating).

## Power by mode

Not applicable (passive connector).

## Pinout and package

Pin table (sheet 1):

| Pin | Signal | Mating sequence | Pin | Signal | Mating sequence |
|---|---|---|---|---|---|
| A1 | GND | First | B12 | GND | First |
| A4 | VBUS | First | B9 | VBUS | First |
| A5 | CC1 | Second | B8 | SBU2 | Second |
| A6 | Dp1 | Second | B7 | Dn2 | Second |
| A7 | Dn1 | Second | B6 | Dp2 | Second |
| A8 | SBU1 | Second | B5 | CC2 | Second |
| A9 | VBUS | First | B4 | VBUS | First |
| A12 | GND | First | B1 | GND | First |
| Shell | GND | — | Shell | GND | — |

Solder-tail order along the board edge: A1/B12, A4/B9, B8, A5, B7, A6, A7, B6, A8, B5, A4/B9 (B4/A9), B1/A12 (sheet 1, front and bottom views). The GND and VBUS pairs share combined pads.

Outline: 8.94 mm wide (footprint outline), 7.35 mm deep; receptacle opening 8.34 (+0.06/−0.02) × 2.56 ± 0.04 mm; height 3.31 mm above the board (sheet 1, side and front views). Plug-and-receptacle mating view: 6.5 mm maximum plug overmould, 1.85 mm minimum (sheet 1).

## Recommended footprint / land pattern

Recommended PCB layout, as viewed from the component side, tolerance ±0.05 mm (sheet 1):

- 12 signal pads, 1.15 mm long: 4 pads 0.60 mm wide (combined GND and VBUS) and 8 pads 0.30 mm wide, 0.50 mm pitch; outer pad span 6.40 mm, VBUS-pair span 4.80 mm, inner span 3.50 mm.
- 2 non-plated locating holes, Ø 0.65 mm.
- 4 shell stake slots (plated, slotted): front pair 0.60 × 2.10 mm (2.10/1.70 mm dimensions) and rear pair 0.60 × 1.80 mm (1.80/1.40 and 1.00/0.60 mm dimensions); stake row spacing 8.64 mm (front) and 5.78 mm (rear); the rear slot row sits 4.18 mm and the front row 2.60/3.68 mm from the pad row.
- PCB edge reference shown on the layout; receptacle front at the edge.

The slot dimensions above are transcribed from a compact drawing: check every pad and slot against sheet 1 at full scale before releasing the KiCad footprint.

## Application circuit and required passives

Not applicable to the connector itself. On the T1 the CC lines go to the FUSB302B (line 41) through TPD8S300A (line 63), D+/D− through TPD4E05U06 (line 62), and VBUS through TVS2200 (line 64) (BOM v1).

## Interfaces and timing

USB 2.0 only (product description, sheet 1): one D+/D− pair per orientation (Dp1/Dn1, Dp2/Dn2), CC1/CC2 and SBU1/SBU2. No SuperSpeed contacts.

## Linux driver

None (passive part).

## Simulation models available

None listed in `manifest.toml`. GCT 3D models: **UNVERIFIED** (not fetched).

## Design notes for the T1

- The 5 A VBUS rating (sheet 1) covers USB PD at 20 V/3 A sink and the T1's 5 V source path.
- Tie D+ (A6, B6) and D− (A7, B7) together on the board for orientation independence; keep the stubs short (USB 2.0 standard practice; the drawing only lists the pins).
- VBUS and GND are first-mate contacts, CC/D±/SBU second-mate (sheet 1 pin table): ESD and surge parts must sit between the connector and the first IC on each net.
- Shell stake length variants (blank 0.95 mm, `060` 0.60 mm, `120` 1.20 mm, sheet 1 Ordering Grid) depend on board thickness; the T1 board thickness has not been decided, so the variant choice is open (LCSC stocks the `-120` and `-060` variants, BOM line 61).
- Operating range −40 to +85 °C (sheet 1).

## Sources

- GCT, *USB4105 USB Type C Receptacle for USB 2.0, SMT Type, PCB Top Mount*, drawing revision B4 (18/12/23), <https://gct.co/files/drawings/usb4105.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 41, 61–64
