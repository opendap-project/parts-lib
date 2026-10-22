# U.FL-R-SMT-1

- **Manufacturer:** Hirose Electric
- **Function:** Ultra-small SMT coaxial receptacle, 50 Ω, DC to 6 GHz
- **BOM v1 lines:** 56 (Wi-Fi/Bluetooth antenna receptacles), ordered as U.FL-R-SMT-1(10), quantity 2
- **Package:** 3.0 × 2.6 mm (3.1 mm over the centre tab), 1.25 mm high
- **Datasheet:** U.FL Series catalog, edition 2009.2 (pages 1–3 used); copy obtained from the LCSC datasheet mirror (part C88373)
- **Status:** Partly UNVERIFIED

## Summary

The U.FL-R-SMT-1 is Hirose's SMT coaxial receptacle for the U.FL plug family: 50 Ω, DC to 6 GHz, 1.9 or 2.4 mm mated height depending on the plug (U.FL catalog 2009.2, pp. 1–2). In the T1 it connects the Wi-Fi/Bluetooth module's RF pins to the two antenna cables (BOM v1 line 56). The (10) suffix is the 2,500-piece reel; (80) is listed in the BOM as an alternative but is not in this catalog edition, which lists (01), (10) and (40) (p. 3).

## Absolute maximum ratings

| Parameter | Value | Condition | Reference |
|---|---|---|---|
| Nominal characteristic impedance | 50 Ω | — | p. 2, Ratings |
| Frequency range | DC to 6 GHz | — | p. 2, Ratings |
| Contact resistance | Centre 20 mΩ max; outer 10 mΩ max | 10 mA max | p. 2, item 1 |
| Insulation resistance | 500 MΩ min | 100 V DC | p. 2, item 2 |
| Withstanding voltage | No flashover or insulation breakdown | 200 V AC, 1 minute | p. 2, item 3 |
| Durability | Contact resistance centre 25 mΩ max, outer 15 mΩ max after test | 30 mating cycles | p. 2, item 5 |
| Storage temperature | −30 to +70 °C | — | p. 2, Ratings |
| Storage humidity | 90 % RH max | — | p. 2, Ratings |

VSWR of mated plug assemblies (p. 2, item 4):

| Plug assembly | Up to 3 GHz | 3 to 6 GHz |
|---|---|---|
| U.FL-LP-040, Ø 0.81 mm cable | 1.3 max | 1.35 max |
| U.FL-LP(V)-040, Ø 0.81 mm cable | 1.3 max | 1.3 max |
| U.FL-LP-066, Ø 1.13 mm cable | 1.3 max | 1.4 max |
| U.FL-LP-066, Ø 1.32 mm cable | 1.3 max | 1.5 max |
| U.FL-LP-062, Ø 1 mm cable | 1.3 max | 1.3 max |
| U.FL-LP-088, Ø 1.37 mm cable | 1.3 max | 1.4 max |

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Operating temperature | −40 to +90 °C | p. 2, Ratings |
| Operating humidity | 90 % RH max | p. 2, Ratings |

Materials (p. 2): phosphor-bronze shell, silver plated; phosphor-bronze female centre contact, gold plated; LCP receptacle insulator, beige, UL94V-0.

## Power by mode

Not applicable (passive connector).

## Pinout and package

Three terminals: SIG (centre, at the tab) and two GND (shell sides) (p. 3, U.FL-R-SMT-1 drawing). Body 3 × 2.6 mm (3.1 mm reference over the tab), Ø 2 mm mating post, 1.25 mm height; occupies 7.7 mm² (p. 1, feature 2). Weight 15.7 mg (p. 3). Mated height with U.FL-LP-066 plugs: 2.5 mm max (p. 1).

| Part number | CL No. | Packaging | Reference |
|---|---|---|---|
| U.FL-R-SMT-1(01) | 331-0472-2-01 | Bag, 100 pieces | p. 3 |
| U.FL-R-SMT-1(10) | 331-0472-2-10 | Reel, 2,500 pieces | p. 3 |
| U.FL-R-SMT-1(40) | 331-0472-2-40 | Reel, 4,000 pieces | p. 3 |

Tape: 12 ± 0.3 mm, 4 ± 0.1 mm pocket pitch; reel Ø 330 ± 2 mm (p. 3).

## Recommended footprint

Recommended PCB mounting pattern (p. 3):

- Two GND pads, 1 ± 0.05 mm wide × 2.2 ± 0.05 mm long, outer edges 4 ± 0.05 mm apart, inner edges 1.9 ± 0.05 mm apart.
- One SIG pad, 1 ± 0.05 × 1 ± 0.05 mm, centred, offset 1.05 ± 0.05 mm from the GND pad row (drawing dimension).
- No conductive traces in the area under the receptacle between the pads (p. 3 note on the pattern).

## Application circuit and required passives

The π matching network on BOM v1 line 58 sits between the module RF pin and this receptacle.

## Interfaces and timing

Not applicable. RF: 50 Ω, DC to 6 GHz, mated VSWR as above (p. 2).

## Linux driver

None (passive part).

## Simulation models

None listed in `manifest.toml`.

## Design notes for the T1

- The Molex 146187 antenna (line 57) uses a Ø 1.13 mm cable with a 2.5 mm-high U.FL plug; the matching catalog row is U.FL-LP-066 with Ø 1.13 mm cable, VSWR 1.3 max to 3 GHz and 1.4 max from 3 to 6 GHz (p. 2), covering both Wi-Fi bands.
- Rated for 30 mating cycles (p. 2): an assembly connector, not a user connector.
- Feed the SIG pad with a 50 Ω grounded coplanar line and keep the area between pads free of copper on the top layer (p. 3 pattern note).
- Catalog note (p. 1): the catalog is for reference; Hirose asks to request the engineering drawing for the current design data. The KiCad footprint should be checked against that drawing (**UNVERIFIED** until obtained).

## Sources

- Hirose Electric, *Ultra Small Surface Mount Coaxial Connectors – 1.9 mm or 2.4 mm Mated Height, U.FL Series*, catalog 2009.2; copy from the LCSC datasheet mirror (part C88373), sha256 `6949727d3bc42a67f6115848d3e5bc7dd4c41db28de7a4b6f0c2f2f5731dcdd2`; manifest URL <https://www.hirose.com/en/product/series/U.FL>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 55–58
