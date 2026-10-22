# Analog Devices MAX98357AETE+T

- **BOM:** board BOM v1, line 32 (Audio), quantity 1
- **Datasheet:** MAX98357A/MAX98357B "Tiny, Low-Cost, PCM Class D Amplifier with Class AB Performance", 19-6779 Rev 11, May 2018 (Maxim Integrated, now Analog Devices). Copy opened: the manufacturer document as mirrored by LCSC (<https://datasheet.lcsc.com/datasheet/pdf/9dd365a93d191d8d6f09766b0e3ea172.pdf>), sha256 `1509d795a016246625d8614df332b18ad85943c9c6cd1bf009291220d4b0d5c3`. The Analog Devices URL in `manifest.toml` timed out; whether it serves a later revision: **UNVERIFIED**.
- **Package of this order number:** 16-pin TQFN, 3 mm × 3 mm × 0.75 mm, −40 to +85 °C, tape and reel (Rev 11, Ordering Information, p. 34; package code T1633+4, outline 21-0136, p. 35)

## Summary

The MAX98357A is a mono filterless Class D amplifier with a PCM digital input (I2S for the A version, 8-slot TDM), no MCLK, five pin-selected gains, shutdown and channel selection on SD_MODE, and 2.5–5.5 V supply (Rev 11, pp. 1, 15–17). In the T1 it drives the internal speaker (BOM line 33) from VSYS, gated by SD_MODE; the speaker is rated 0.7 W, so gain and the OS limiter keep the output within that. BOM line 32.

## Absolute maximum ratings

Rev 11, p. 4.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VDD, LRCLK, BCLK, DIN to GND | −0.3 | +6 | V |
| All other pins to GND | −0.3 | VDD + 0.3 | V |
| Continuous current in/out of VDD, GND, OUT_ | — | ±1.6 | A |
| Continuous input current, other pins | — | ±20 | mA |
| OUT_ short to GND or VDD; OUTP to OUTN | Continuous | — | — |
| Continuous power dissipation, TQFN, TA = 70 °C (derate 20.8 mW/°C) | — | 1666 | mW |
| Junction temperature | — | +150 | °C |
| Operating temperature | −40 | +85 | °C |
| Storage temperature | −65 | +150 | °C |
| Reflow soldering temperature | — | +260 | °C |

SD_MODE is limited to VDD + 0.3 V; when SD_MODE is driven high directly from a logic supply above VDD, add about 2 kΩ in series (Rev 11, p. 17).

## Recommended operating conditions

VDD = 5 V, BCLK = 3.072 MHz, LRCLK = 48 kHz unless noted (Rev 11, Electrical Characteristics, pp. 4–7).

| Parameter | Condition | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| Supply voltage VDD | — | 2.5 | — | 5.5 | V |
| UVLO | — | 1.5 | 1.8 | 2.3 | V |
| Output power, THD+N 1 %, 12 dB | 8 Ω + 68 µH, VDD = 5 V | — | 1.4 | — | W |
| Output power, THD+N 1 %, 12 dB | 8 Ω + 68 µH, VDD = 3.7 V | — | 0.77 | — | W |
| Output power, THD+N 10 %, 12 dB | 8 Ω + 68 µH, VDD = 3.7 V | — | 0.93 | — | W |
| THD+N | 1 kHz, 0.5 W, 8 Ω + 68 µH | — | 0.013 | — | % |
| Output noise, A-weighted | 24/32-bit data | — | 22.8 | — | µVrms |
| Dynamic range, A-weighted | 8 Ω + 33 µH, 3.40 Vrms | — | 103.5 | — | dB |
| PSRR | 217 Hz, 200 mVpp | 60 | 77 | — | dB |
| Efficiency | 8 Ω + 68 µH, THD+N 10 %, 1 kHz | — | 92 | — | % |
| Current limit | — | — | 2.8 | — | A |
| Class D switching frequency | — | — | 300 | — | kHz |
| Spread-spectrum bandwidth | — | — | ±20 | — | kHz |
| Turn-on time | — | — | 7 | 7.5 | ms |
| Output offset | gain 15 dB, 25 °C | — | ±0.3 | ±2.5 | mV |

## Power by mode

Rev 11, p. 4 and p. 17.

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Active, quiescent | VDD = 5 V, 25 °C | 2.75 | 3.35 | mA |
| Active, quiescent | VDD = 3.7 V, 25 °C | 2.4 | 2.85 | mA |
| Standby (BCLK removed, outputs high-Z) | SD_MODE = 1.8 V, no BCLK, 25 °C | 340 | 400 | µA |
| Shutdown | SD_MODE = 0 V, 25 °C | 0.6 | 2 | µA |

Output-trace parasitic capacitance adds VDD × 300 kHz × C to the quiescent current (p. 33). Thermal, TQFN: θJA 48 °C/W, θJC 7 °C/W (p. 4).

## Pinout and package

16-pin TQFN, Rev 11, Pin Description, p. 15.

| Pin | Name | Function |
|---|---|---|
| 1 | DIN | Serial data input |
| 2 | GAIN_SLOT | Gain select (I2S/LJ) or TDM slot select |
| 3, 11, 15 | GND | Ground |
| 4 | SD_MODE | Shutdown and channel select |
| 5, 6, 12, 13 | N.C. | Not connected |
| 7, 8 | VDD | Supply |
| 9 | OUTP | Positive speaker output |
| 10 | OUTN | Negative speaker output |
| 14 | LRCLK | Frame clock |
| 16 | BCLK | Bit clock |
| EP | Exposed pad | Not internally connected; connect to a ground plane for heat |

Outline 21-0136 rev O, variant 16L 3×3, package code T1633+4 (Rev 11, pp. 36–37): body 2.90/3.00/3.10 mm; height 0.70/0.75/0.80 mm; pitch 0.50 mm; lead width b 0.20/0.25/0.30 mm; lead length L 0.30/0.40/0.50 mm; exposed pad D2 = E2 = 0.95/1.10/1.25 mm.

## Recommended footprint / land pattern

The datasheet names Maxim land pattern 90-0031 for the 16 TQFN (Rev 11, p. 35) but does not reproduce it. Land pattern 90-0031 dimensions: **UNVERIFIED** (document not opened). Until it is opened, derive pads from outline 21-0136 (above) to IPC-7351.

## Application circuit and required passives

- VDD bypass: 0.1 µF and 10 µF to GND; some applications need only the 10 µF; add bulk capacitance if the supply trace is long (Rev 11, p. 33).
- No output filter: filterless operation relies on the speaker inductance; use a speaker with series inductance above 10 µH (p. 33).
- GAIN_SLOT (I2S/LJ mode, Table 8, p. 28): 100 kΩ ±5 % to GND = 15 dB; GND = 12 dB; open = 9 dB; VDD = 6 dB; 100 kΩ ±5 % to VDD = 3 dB. Gain is referenced to a 2.1 dBV DAC full scale: output (dBV) = input (dBFS) + 2.1 dB + gain (p. 28). TDM mode fixes gain at 12 dB.
- SD_MODE (Table 5 and Table 6, p. 17; Figures 4–5, p. 18): internal pull-down 100 kΩ (92–108 kΩ, p. 7). Above B2 (1.245–1.5 V) selects left; between B1 (0.65–0.825 V) and B2 selects right; between B0 (0.08–0.355 V) and B1 selects (L+R)/2; below B0 is shutdown. With a 1.8 V logic supply, RSMALL = 69.8 kΩ (right) and RLARGE = 300 kΩ ((L+R)/2); RSMALL = 94.0 × VDDIO − 100 kΩ, RLARGE = 222.2 × VDDIO − 100 kΩ.
- Layout: wide low-resistance output, supply and ground traces; ground fill around signal traces (p. 33).

## Interfaces and timing

Rev 11, pp. 6–7 and 16.

- **Formats:** MAX98357A takes I2S (left channel when LRCLK is low, data clocked on the BCLK rising edge); 16/24/32-bit in I2S, 16/32-bit TDM with up to 8 slots. A frame-sync pulse on LRCLK selects TDM automatically.
- **Sample rates:** LRCLK 8, 16, 32, 44.1, 48, 88.2 and 96 kHz only; 11.025, 12, 22.05 and 24 kHz are not supported. Do not remove LRCLK while BCLK runs (risk of a large DC output) (p. 16).
- **BCLK:** 32, 48 or 64 × LRCLK, 0.2432–25.804 MHz; high and low time ≥ 15 ns. Setup and hold of DIN and LRCLK to BCLK ≥ 10 ns.
- **Jitter tolerance:** 0.5 ns RMS below 40 kHz, 12 ns RMS above (Table 1, p. 16).
- **Input levels:** VIH ≥ 1.3 V, VIL ≤ 0.6 V on the digital audio inputs, input capacitance 3 pF. A 1.8 V I2S bus meets these thresholds.
- **DC blocker:** −3 dB at 3.7 Hz (p. 16). Digital filter set automatically by LRCLK (Table 4, p. 17).
- **Pop behaviour:** start-up ramps from mute; there is no volume ramp-down on shutdown, so ramp the digital data down before shutdown (p. 28).

## Linux driver

- Mainline driver `sound/soc/codecs/max98357a.c`, compatibles `maxim,max98357a` and `maxim,max98360a` (mainline source checked 2026-10-22). Optional `sdmode-gpios` and `sdmode-delay`; the driver drives SD_MODE high on stream start and low on stop. Driver rates: 8, 16, 32, 44.1, 48, 88.2 and 96 kHz.
- Device-tree binding: `Documentation/devicetree/bindings/sound/maxim,max98357a.yaml` (present in mainline, checked 2026-10-22).
- BOM v1 line 32: driver path "mainline + Debian". The Debian config symbol name (`SND_SOC_MAX98357A`) and its state were not re-checked in this sheet: **UNVERIFIED**.

## Simulation models available

None listed in `manifest.toml`. Manufacturer models: **UNVERIFIED**. An evaluation kit exists (Rev 11, p. 1).

## Design notes for the T1

- Supply from VSYS: VDD range 2.5–5.5 V; VSYS minimum (3.5 V per ADR 0010) is inside it. Confirm the VSYS maximum stays at or below 5.5 V: **UNVERIFIED** here.
- Speaker rated 0.7 W (BOM line 33). At VDD = 3.7 V and 12 dB the amplifier gives 0.77 W at 1 % THD+N into 8 Ω (p. 5); the gain strap and the OS limiter must keep the speaker below its rating. Lower gain (3 or 6 dB) reduces the reachable level.
- SD_MODE from a 1.8 V GPIO: a direct high (1.8 V, above B2) selects the left channel; VDD (VSYS) is always above 1.8 V, so no series resistor is needed for the absolute-maximum limit (p. 17).
- If SD_MODE is not driven, removing BCLK still gives 340 µA standby, not the 0.6 µA shutdown (p. 17).
- The I2S lines are shared with no other device at 1.8 V on this amplifier; DIN, BCLK and LRCLK tolerate up to 6 V (p. 4).

## Sources

- Maxim Integrated (Analog Devices), MAX98357A/MAX98357B data sheet, 19-6779 Rev 11, May 2018; copy from <https://datasheet.lcsc.com/datasheet/pdf/9dd365a93d191d8d6f09766b0e3ea172.pdf>, sha256 `1509d795a016246625d8614df332b18ad85943c9c6cd1bf009291220d4b0d5c3`. Manifest URL: <https://www.analog.com/media/en/technical-documentation/data-sheets/MAX98357A-MAX98357B.pdf> (timed out on 2026-10-22).
- Linux mainline, `sound/soc/codecs/max98357a.c`, read 2026-10-22.
- OpenDAP board BOM v1, lines 32 and 33; board ADR 0010.
