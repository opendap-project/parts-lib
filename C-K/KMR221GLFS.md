# KMR221GLFS

- **Manufacturer:** C&K
- **Function:** Microminiature top-actuated SMT tactile switch, SPST normally open, with ground pin
- **Package:** KMR 2 series, 1.9 mm height, gull-wing SMT terminals
- **Datasheet:** KMR 2 Series catalog pages B–11 and B–12, dated 8 June 2016 (copy obtained from the LCSC datasheet mirror; the manifest URL `ckswitches.com/media/1479/kmr2.pdf` redirects to a Littelfuse URL that refused the download)
- **BOM v1 line:** 76 (Open; placeholder)

## Summary

The KMR221GLFS is a 2 N, silver-contact, top-actuated tactile switch with a ground pin, 1.9 mm high (part number description, p. B–11). In the T1 it is only a placeholder for the Action button (BOM v1 line 76), which needs a deeper travel than the other buttons (T1-022). The datasheet gives a travel of **0.25 mm ± 0.1 mm** for the KMR221 (p. B–11), which refutes the BOM's "≈ 0.2 mm" estimate only in its second digit and confirms the BOM's concern: it is a short-travel switch, only 0.05 mm deeper nominal than the PTS815 on line 77 (0.20 mm ± 0.1 mm), with overlapping tolerances.

## Absolute maximum ratings

| Parameter | Silver contacts (KMR221) | Reference |
|---|---|---|
| Maximum power | 1 VA | p. B–11, Electrical |
| Maximum voltage | 32 V DC | p. B–11 |
| Minimum voltage | 20 mV DC | p. B–11 |
| Maximum current | 50 mA | p. B–11 |
| Minimum current | 1 mA (ULC version: 1 µA at 1.8 V DC) | p. B–11 |
| Dielectric strength | ≥ 250 Vrms | p. B–11 |
| Contact resistance | ≤ 100 mΩ | p. B–11 |
| Insulation resistance | ≥ 1 GΩ | p. B–11 |
| Bounce time | ≤ 3 ms | p. B–11 |
| Storage temperature | −55 to 85 °C | p. B–11, Environmental |

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Operating temperature (silver) | −40 to 85 °C | p. B–11, Environmental |
| Operating force | 2.0 N (200 g) ± 0.50 N | p. B–11, Mechanical (KMR221 LFS) |
| Travel | 0.25 mm ± 0.1 mm | p. B–11 |
| Operating life | 200,000 cycles | p. B–11 |
| Tactile feel (2 N, 3 N, 4 N versions) | ≥ 30 % | p. B–11 |
| Soldering | Lead-free reflow per IEC 61760-1 | p. B–11, Process |

## Power by mode

Not applicable (passive switch).

## Pinout and package

Part number decoding (p. B–11): KMR2 = 1.9 mm total height; 2 = 2 N actuation force; 1 = silver contacts; G = ground pin; LFS = lead-free compatible, silver plated. Contact arrangement: 1 make contact, SPST N.O.; IP40 (p. B–11, Features).

Outline (p. B–12, "KMR 2 Series – 1.9 mm height"): body 4.2 mm long (4.6 mm over the terminals), 2.8 mm wide, 1.9 mm high (1.4 mm to the top of the frame). Exact assignment of the four signal terminals and the ground terminal to the two switch contacts is not legible in the downloaded copy: **UNVERIFIED**.

Packaging: reels of 7,000 pieces, 330 mm ± 2 mm reel; 12 mm tape, 4 mm pitch (pp. B–11, B–12).

## Recommended footprint / land pattern

The PCB layout on p. B–12 is shown with the ground-pin option: overall pad span 5 mm, with pad rows at 2.45 mm and 0.55 mm and pad dimensions of 0.6 mm; the remaining figures on the drawing (1.7, 2.11, 3.2, 1.61, 2.2, 2.6, 1) are not attributable to features at the resolution of the available copy. **UNVERIFIED**: draw the footprint only from a full-resolution C&K drawing.

## Application circuit and required passives

Not applicable to the switch. On the T1 the Action button line reads a GPIO through `gpio-keys` (BOM line 76) with ESD protection by TPD1E10B06 (line 74).

## Interfaces and timing

Not applicable. Bounce time ≤ 3 ms (p. B–11) sets the minimum debounce interval for the `gpio-keys` node.

## Linux driver

`gpio-keys` (mainline, `KEYBOARD_GPIO=m` in Debian, BOM v1 §3 and line 76). No device-specific driver.

## Simulation models available

None listed in `manifest.toml`.

## Design notes for the T1

- The datasheet travel, 0.25 mm ± 0.1 mm (p. B–11), is too shallow for a "deeper travel, clear click" Action button against the 0.20 mm ± 0.1 mm PTS815 on line 77. The BOM line stays Open; the replacement needs a datasheet travel clearly above 0.35 mm (the PTS815 upper bound), confirmed with the case plunger.
- 32 V DC and 50 mA maximum (p. B–11) are far above a GPIO input with a pull-up; the 1 mA minimum current of the standard (non-ULC) version (p. B–11) is above a typical SoC internal pull-up current, so contact wetting is not guaranteed at GPIO currents. The ULC version is specified down to 1 µA at 1.8 V DC (p. B–11).
- Top-actuated: the actuation direction is perpendicular to the board. Side-edge buttons (T1-014/015) require either a plunger in the case or a side-actuated part.

## Sources

- C&K, *KMR 2 Series, Microminiature SMT Top Actuated*, catalog pp. B–11 and B–12, 8 June 2016; copy from the LCSC datasheet mirror (part C72443), sha256 `2720f475dd31d921fcb70d1d32dd02bd52de8c88554f63b59809a1b744fb7a26`; manifest URL <https://www.ckswitches.com/media/1479/kmr2.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 74, 76, 77
