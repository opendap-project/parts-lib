# DM3AT-SF-PEJM5

- **Manufacturer:** Hirose Electric
- **Function:** MicroSD card connector, push-push (ejection mechanism), top board mounting, right-angle SMT, with card-detection switch
- **BOM v1 lines:** 11 (Core, microSD socket)
- **Package:** 8 contacts plus detect switch and shell, 13.85 × 15.95 mm, 1.68 mm high
- **Datasheet:** DM3 Series microSD Card Connectors catalog, edition 2017.1 (copyright stamp May 1, 2017), 13 pages (copy obtained from the LCSC datasheet mirror, part C114218)
- **Status:** Partly UNVERIFIED

## Summary

The DM3AT is Hirose's push-push microSD connector for top-board mounting, with a built-in card tray, reverse-insertion protection, four shield-to-board ground points and a normally open card-detection switch (DM3 catalog 2017.1, p. 1). In the T1 it is the microSD socket (BOM v1 line 11): VDD from RK809 SWOUT2, signalling from RK809 LDO5 at 1.8 or 3.3 V, protected by a TPD6E05U06 on CLK, CMD and D0–D3 (line 73).

## Absolute maximum ratings

| Parameter | Value | Condition | Reference |
|---|---|---|---|
| Current rating | 0.5 A | — | p. 2, Ratings |
| Voltage rating | 125 V AC | — | p. 2, Ratings |
| Insulation resistance | 1000 MΩ min (initial) | 500 V DC | p. 2, item 1 |
| Withstanding voltage | No flashover or insulation breakdown | 500 V AC, 1 minute | p. 2, item 2 |
| Contact resistance | 100 mΩ max (initial) | 1 mA | p. 2, item 3 |
| Durability (DM3AT) | Contact resistance change ≤ 40 mΩ | 10,000 cycles at 400–600 cycles per hour | p. 2, item 7 |
| Storage temperature | −40 to +85 °C (Note 2) | — | p. 2, Ratings |
| Soldering heat | Reflow per profile; manual 350 °C for 3 s | — | p. 2, item 8 |

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Operating temperature | −25 to +85 °C, including temperature rise from current (Note 1) | p. 2, Ratings |
| Operating humidity | 95 % RH max, no condensation | p. 2, Ratings |

Materials (DM3AT, p. 2): LCP insulator (black, UL94V-0); copper-alloy contacts, gold plated on contact and lead areas; stainless-steel guide cover, gold-plated leads; other components stainless steel, nickel plated.

## Power by mode

Not applicable (passive connector).

## Pinout and package

Card contacts (p. 3, top view): #1 DAT2, #2 CD/DAT3, #3 CMD, #4 VDD, #5 CLK, #6 VSS, #7 DAT0, #8 DAT1, at 1.1 mm pitch. Card-detection switch terminals A and B: open without a card, closed with the card inserted (p. 3, note 2). The metal cover connects to the board ground at four points (p. 1, feature 3).

Dimensions (p. 3): 13.85 mm wide, 15.95 mm deep, 1.68 mm high; card positions 16.75 mm (over-stroke), 17.55 mm (lock), 21.55 mm (eject), reference from the rear; ejected card protrudes to a distance of 4.0 mm (p. 1). HRS No. 609-0031-0 (p. 3).

Packaging: embossed carrier tape, 1,500 pieces per reel, 32 mm tape, 20 mm pitch, Ø 380 mm reel (p. 4).

## Recommended footprint

Recommended PCB mounting pattern (p. 3, all dimensions in mm):

- 8 signal lands at P = 1.1 mm, 0.7 mm wide, 1.2 mm long; the signal row spans 7.7 mm (8.65 mm and 9.25 mm max over the outer features, 10 mm min overall).
- Shell and detect-switch lands at the sides and front (dimensions 1.55, 1.0, 0.5, 2.7, 3.25, 1.3, 0.8, 2.8, 1.9, C0.15 on the drawing; overall pattern 14.05 / 14.5 / 15.1 mm deep).
- Keep-out (no conductive traces) areas marked on the pattern (note 3), including a band 8.9 mm min × 8.2 mm min under the card path and the areas at 4.4 mm max / 6 mm min and 5.7 mm max / 7.9 mm min.

The individual shell-land dimensions are transcribed from a compact drawing: check every land against the catalog page at full scale before releasing the footprint.

## Application circuit and required passives

Not given in the catalog. The SD/SDIO pull-ups, the VDD bulk capacitance and the LDO5 1.8/3.3 V signalling switch follow the RK3566 reference design (Radxa ZERO 3W schematic in the cache); values are **UNVERIFIED** here. ESD: TPD4E05U06DQAR ×2 on CLK, CMD, D0–D3 (line 73; TPD6E05U06 until BOM v1.1).

## Interfaces and timing

Not applicable to the connector. The catalog gives no signal-integrity data. On the T1 the socket carries UHS-I (SDR104 at 1.8 V) per BOM line 73.

## Linux driver

None for the socket. The card detect switch is read as a GPIO by the `dw_mmc-rockchip` host (SD detect on PMUIO1, BOM §4.2); not a device-specific driver.

## Simulation models

None listed in `manifest.toml`.

## Design notes for the T1

- The card-detection switch is normally open and closes on insertion (p. 3, note 2): pull the detect line up and read it active-low, or invert in the device tree.
- 0.5 A current rating (p. 2) covers microSD VDD supply current.
- Respect the keep-out areas under the connector (p. 3, note 3); route no traces under the card path on the top layer.
- 10,000-cycle durability (p. 2) suits a user-accessible card slot.
- Operating temperature −25 to +85 °C (p. 2).

## Sources

- Hirose Electric, *microSD Card Connectors, DM3 Series*, catalog 2017.1 (May 1, 2017); copy from the LCSC datasheet mirror (part C114218), sha256 `b74bee24f5e7f9bc68b403a21b2c5ff94ca4230072b10a41ca62664ea95a5951`; manifest URL <https://www.hirose.com/en/product/series/DM3>
- OpenDAP board, `docs/specs/bom-v1.md`, lines 11, 73 and §4.2
