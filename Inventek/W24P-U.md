# W24P-U

- **Manufacturer:** Inventek Systems
- **Function:** 2.4 GHz PCB dipole antenna, 30 × 5 mm, with 90 mm cable and U.FL plug
- **BOM v1 lines:** none in production. Prototype only: second antenna on the module's ANT1 for the dedicated-configuration experiment of board ADR 0018 (with line 57)
- **Package:** PCB antenna 30 × 5.0 mm, 90 mm cable, U.FL
- **Datasheet:** Inventek *OEM Wi-Fi Antennas, P/N W24P-U*, DOC-DS-20075-1.0, 2013-10-01 ("Preliminary"), 8 pages. Cited as "DS-20075".
- **Availability (2026-10-24):** Digi-Key 8,353 @ $1.48; Mouser 2,491 (FindChips range $1.44–1.64); LCSC C6604641 0.
- **Status:** Partly UNVERIFIED

## Summary

The W24P-U is a 2.4 GHz-only PCB antenna, 30 × 5 mm, linear polarisation, 3.2 dBi typical peak gain, delivered with a 90 mm cable and a U.FL plug (DS-20075 §1–3). It is on the FCC, ISED and Japan antenna lists of the Murata Type 2EL at 3.2 dBi, 2.4 GHz only, cable "90 mm or more" (CER-0248 Tables 20, 36, 56; E2B-09-1413 Table 3). Murata allows it on ANT1 in the dedicated configuration (CER-0248 §2.1.6.1). In the T1 it is only a prototype experiment for the dedicated configuration (board ADR 0018): it fits flat in the 7.0 mm top band but closer than the provisional 5 mm keep-out to the battery.

## Absolute maximum ratings

Not published (DS-20075).

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| Centre frequency | 2442 MHz | DS-20075 §3 |
| Bandwidth | 100 MHz min | DS-20075 §3 |
| VSWR | 2 max | DS-20075 §3 |
| Impedance | 50 Ω | DS-20075 §3 |
| Peak gain | 3.2 dBi typical; 2.76–3.58 dBi across 2400–2484 MHz | DS-20075 §3, §8.2 |
| Efficiency | 79 % typical; 70.6–83.4 % across 2400–2484 MHz | DS-20075 §3, §8.2 |
| Operating temperature | −40 to +80 °C | DS-20075 §3.1 |
| Storage temperature | −55 to +100 °C | DS-20075 §3.1 |
| Humidity | 95 % max, non-condensing | DS-20075 §3.1 |

## Power by mode

Not applicable (passive part).

## Pinout and package

| Item | Value | Reference |
|---|---|---|
| Outline | 30 × 5.0 mm; thickness printed ".05" mm (DS-20075 §3), 0.50 mm max per Digi-Key: **UNVERIFIED** which is right | DS-20075 §3; Digi-Key |
| Cable | 90 mm standard; custom lengths by special order | DS-20075 §2, §7 |
| Connector | U.FL | DS-20075 §2 |

## Recommended footprint

Not applicable (cabled antenna, mounted to the case).

## Application circuit and required passives

On ANT1 (pin 23) through Murata's dedicated-configuration positions (E2B-09-1413 Figure 10) and a U.FL receptacle.

## Interfaces and timing

Not applicable.

## Linux driver

None (passive part). The dedicated configuration needs `WlanCalData_ext_dANT.conf` (E2B-09-1413 §4.4).

## Simulation models

None published.

## Design notes for the T1

- 2.4 GHz only: suitable for ANT1 (Bluetooth), never for ANT0 (Wi-Fi 5 GHz).
- Fits flat in the 7.0 mm top band (5.0 mm wide), but about 1–2 mm from the battery pocket, below the provisional 5 mm keep-out (board research *Antennas and RF exposure* §3.2). Prototype measurement only.
- The 90 mm cable needs a routed path in the case.

## Sources

- Inventek DS-20075 rev. 1.0: <https://www.inventeksys.com/wp-content/uploads/W24P-U_2.4Ghz_-Antenna_Specification.pdf>, sha256 `68cde1cc9ebc00631efe68414a5c1dce6e3f248c57385f4c0f66edbb11dfecbc`; listed in `manifest.toml`.
- Murata CER-0248 Rev. 6.0, E2B-09-1413 Rev. 9.0 (LBES5PL2EL-923 entries in `manifest.toml`).
- Availability: Digi-Key search, FindChips, JLCPCB parts API, 2026-10-24.
- OpenDAP board, [ADR 0018](https://github.com/opendap-project/board/blob/main/docs/adr/0018-antennas-and-certification-route.md).
