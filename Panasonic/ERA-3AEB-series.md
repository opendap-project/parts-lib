# ERA-3AEB series

- **Manufacturer:** Panasonic
- **Function:** Thin-film chip resistors, ±0.1 % tolerance (code B), ±25 ppm/K TCR (code E)
- **BOM v1 lines:** 37 (Audio, headphone-amplifier precision resistors), about 40 pieces
- **Package:** 0603 (1608 metric)
- **Datasheet:** Panasonic "Metal Film (Thin Film) Chip Resistors, High Reliability Type, Series ERA 1A, 2A, 3A, 6A, 8A" series catalogue, pages dated 8-Jun-20, 7 pages (cited as "ERA catalogue"). Obtained from the LCSC-hosted copy (<https://datasheet.lcsc.com/datasheet/pdf/4fab4a4bbac579220253950d6371122a.pdf?productCode=C2074417>); the manifest URL timed out from this host.
- **Status:** Partly UNVERIFIED

## Summary

Thin-film chip resistors, 0603, ±0.1 % tolerance (code B), ±25 ppm/K TCR (code E), 0.1 W, AEC-Q200 grade 0 (ERA catalogue pp. 1–2). In the T1 they set the OPA1622 difference-amplifier gain, feedback and output ballast, where tolerance matching sets common-mode rejection and channel balance (BOM v1 line 37). Values come from the OPA1622 difference-amplifier example; C0G 470 pF capacitors pair with them (BOM §5). Second sources: Susumu RG1608, Yageo RT0603.

## Absolute maximum ratings

ERA catalogue p. 2, "Ratings", ERA3A row.

| Parameter | Value | Unit | Note |
|---|---|---|---|
| Power rating at 85 °C | 0.1 | W | Derate linearly to 0 % at 155 °C |
| Limiting element voltage | 75 | V | RCWV = √(P × R) or this, whichever is less |
| Maximum overload voltage | 150 | V | OTV = 2.5 × RCWV or this, whichever is less |
| Category temperature range | −55 to +155 | °C | — |

## Recommended operating conditions

ERA catalogue pp. 1–2.

| Parameter | ERA3AEB | Unit |
|---|---|---|
| Tolerance | ±0.1 | % |
| TCR | ±25 | ×10⁻⁶/K |
| Resistance range | 47 to 330 k (E24, E96) | Ω |
| AEC-Q200 grade | Grade 0 | — |

Part number format (p. 1): ERA3AEB + 3-digit value code for E24 (e.g. ERA3AEB102V = 1 kΩ) or 4-digit code for E96 (e.g. ERA3AEB1051V = 1.05 kΩ), suffix V = punched carrier taping, 4 mm pitch, 5000 pcs. E192 values on request (note 4, p. 2).

## Power by mode

Not applicable (passive). Check the ballast resistor dissipation at full headphone output against 0.1 W with derating above 85 °C (p. 2).

## Pinout and package

Two terminals, no polarity. ERA3A dimensions (ERA catalogue p. 3): L 1.60 ± 0.20, W 0.80 ± 0.20, a 0.30 ± 0.20, b 0.30 ± 0.20, T 0.45 ± 0.10 mm; mass 2 g / 1000 pcs. E96 values carry no value marking (p. 3).

## Recommended footprint

Not in the series catalogue; it points to Panasonic's separate "Data Files" for land pattern and soldering conditions (p. 1). **UNVERIFIED**; use the KiCad 0603 resistor footprint until the Panasonic land-pattern document is retrieved.

## Application circuit and required passives

OPA1622 difference amplifier and feedback network; values from the OPA1622 datasheet example (see the OPA1622IDRCR sheet). Not transcribed here.

## Interfaces and timing

Not applicable.

## Linux driver

None (passive component).

## Simulation models

None listed in `manifest.toml`.

## Design notes for the T1

- Panasonic lists "low current noise, excellent linearity" as a series feature (p. 1); no numeric noise index is given in the catalogue (**UNVERIFIED** value).
- ±0.1 % tolerance on four difference-amplifier resistors bounds the common-mode rejection of each balanced leg; if the CMRR target needs tighter matching, ERA3ARB/ERA3ARW (±10 ppm/K, down to ±0.05 %) exist in the same footprint for 1 k–100 kΩ (p. 2).
- Keep the resistor value range inside 47 Ω–330 kΩ for ERA3AEB; lower values need ERA3AHD (±0.5 %, ±50 ppm/K) (p. 2).

## Sources

- Panasonic ERA series catalogue (8-Jun-20 pages), pp. 1–3 (LCSC-hosted copy, URL above).
- Board BOM v1, line 37 and §5.
