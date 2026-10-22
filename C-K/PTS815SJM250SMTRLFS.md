# PTS815SJM250SMTRLFS

- **Manufacturer:** C&K
- **Function:** Microminiature top-actuated SMT tactile switch, SPST normally open, 180 gf
- **Package:** PTS 815 series, 4.2 × 3.2 mm, 2.5 mm height, J-bend SMT terminals (4)
- **Datasheet:** PTS 815 Series catalog pages B–43 and B–44, dated 8 April 2021 (copy obtained from the LCSC datasheet mirror; the manifest URL returned an HTML page)
- **BOM v1 line:** 77 (Power, Vol+, Vol−; quantity 3)

## Summary

The PTS815 is a commercial-grade, top-actuated tactile switch with a 4.2 × 3.2 mm footprint and 2.5 mm height; the SJM variant has a 180 gf white actuator (p. B–43). In the T1 three of them are the Power (also MaskROM), Vol+ and Vol− buttons (BOM v1 line 77): Power drives the RK809 PWRON input, Vol+ and Vol− sit on separate SARADC inputs.

## Absolute maximum ratings

| Parameter | Value | Reference |
|---|---|---|
| Maximum voltage | 12 V DC | p. B–43, Electrical |
| Maximum current DC | 50 mA | p. B–43 |
| Dielectric strength | 250 V AC (1 min) | p. B–43 |
| Contact resistance | ≤ 100 mΩ initial | p. B–43 |
| Insulation resistance | ≥ 100 MΩ | p. B–43 |
| Bounce time | ≤ 10 ms | p. B–43 |

No minimum-current (wetting) figure is given. Storage temperature: not stated.

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Operating temperature | −20 to 70 °C | p. B–43, Environmental |
| Operating force (SJM) | 180 ± 50 gf | p. B–43 |
| Travel | 0.20 mm ± 0.1 mm | p. B–43, Specifications |
| Operating life (SJM) | 100,000 operations | p. B–43 |
| Soldering | Infrared reflow per IEC 61760-1 | p. B–43, Process |

## Power by mode

Not applicable (passive switch).

## Pinout and package

Part number decoding (p. B–43, How To Order): PTS815 S (standard actuator) J (J-bend SMT) M (180 gf, white actuator) 250 (2.5 mm height) SMTR (tape and reel) LFS (RoHS, silver plated). Contact arrangement: 1 make contact, SPST N.O.

Outline (p. B–44): body 4.2 ± 0.2 mm × 3.20 ± 0.2 mm, 4.6 ± 0.2 mm over the terminals, height 2.5 ± 0.2 mm (1.55 mm to the frame top), actuator 3.0 × 2.2 mm. Four terminals numbered 1–4; terminal-to-terminal spacing 2.15 ± 0.1 mm; terminal width 4 × 0.55 mm. The circuit diagram on p. B–44 shows the switch between terminal pairs; which terminals are internally common is not legible in the available copy (**UNVERIFIED**; check before drawing the symbol).

Packaging: reels of 3,000 pieces, EIA 481B, 330 mm reel, 12 mm tape, 8 mm pocket pitch (pp. B–43, B–44).

## Recommended footprint / land pattern

P.C.B land dimension (p. B–44):

- 4 pads, 1.0 mm long (inner edges 3.5 mm apart, outer edges 5.5 mm apart) × 0.7 mm wide.
- Pad rows 2.15 mm apart (centre to centre).

## Application circuit and required passives

Not applicable to the switch. On the T1 (BOM v1 line 77): Power → RK809 PWRON (and, through BAT54 line 78, the MaskROM NOR on line 98); Vol+ on SARADC_VIN0 with the ladder resistor of the `adc-keys` node; Vol− on its own SARADC_VIN1 node. ESD: TPD1E10B06 per button (line 74).

## Interfaces and timing

Not applicable. Bounce time ≤ 10 ms (p. B–43) sets the minimum debounce interval in software.

## Linux driver

From BOM v1 line 77: Power through `rk805-pwrkey` (RK809 PWRON, mainline + Debian); Vol+ and Vol− through `adc-keys` (`KEYBOARD_ADC=m`) on `rockchip-saradc` (`ROCKCHIP_SARADC=m`). No device-specific driver.

## Simulation models available

None listed in `manifest.toml`.

## Design notes for the T1

- Operating temperature −20 to 70 °C (p. B–43) is narrower than the KMR2 (−40 to 85 °C); it is the binding limit for the button subsystem.
- Travel 0.20 mm ± 0.1 mm (p. B–43) is the baseline the Action button (line 76) must exceed.
- Top-actuated: side-edge buttons need a case plunger (BOM line 77 note, T1-014/015).
- No minimum switching current is specified; contacts are silver-plated (LFS) (p. B–43).
- 12 V DC / 50 mA maximum (p. B–43) covers the 1.8 V and 3.3 V logic levels at the PWRON and SARADC nodes.

## Sources

- C&K, *PTS 815 Series, Microminiature SMT Top Actuated*, catalog pp. B–43 and B–44, 8 April 2021; copy from the LCSC datasheet mirror (part C2689510), sha256 `858ecdb21e9c8ce7146be4f3512defc531f6ffc4c67dd152d41d80c3a1c5d915`; manifest URL <https://www.ckswitches.com/media/2768/pts815.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 74, 76–78, 98 and §3
