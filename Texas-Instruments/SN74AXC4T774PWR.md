# SN74AXC4T774PWR

- **Manufacturer:** Texas Instruments
- **Function:** 4-bit dual-supply bus transceiver with an independent direction pin per bit, 0.65–3.6 V on each port, tri-state outputs
- **BOM v1 lines:** 95 (I2S-A path)
- **Package:** TSSOP-16 (PW), 0.65 mm pitch
- **Datasheet:** SN74AXC4T774, SCES898C (July 2019, revised May 2022), `sn74axc4t774.pdf`, sha256 `d2dffb7067c38d8602b5f66acd639269564b1abae4e9e4794f022cef620cb430` (downloaded 2026-10-22 from <https://www.ti.com/lit/ds/symlink/sn74axc4t774.pdf>). The `manifest.toml` entry for this MPN currently points at the SN74AXC8T245 datasheet (sha256 `6cf4003c438c…`)
- **Status:** Partly UNVERIFIED

## Summary

The SN74AXC4T774 is a 4-bit non-inverting translator with independent supplies VCCA and VCCB (each 0.65–3.6 V) and one direction pin per bit (DIR1–DIR4). OE (active low) puts both ports in high impedance. The control pins are referenced to VCCA (SCES898C §7.1, Table 4-1, Table 7-1, pp. 3, 20–21). Outputs are glitch-free in any supply order, and both ports go to high impedance when either supply is below 100 mV (§7.3.4, §7.3.6, pp. 20–21). In the T1 it carries the HAT I2S-A BCLK, FS, DIN and DOUT between the SoC's 1.8 V VCCIO6 bank and the HAT's 3.3 V side, with the direction of each bit set separately (BOM v1 line 95).

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, VCCA, VCCB | — | −0.5 | 4.2 | V | SCES898C p. 4, §5.1 |
| Input voltage, VI (A port, B port, control) | — | −0.5 | 4.2 | V | p. 4 |
| Output voltage, high-impedance or power-off state | A or B port | −0.5 | 4.2 | V | p. 4 |
| Output voltage, high or low state | A port / B port | −0.5 | VCCA + 0.2 / VCCB + 0.2 | V | p. 4 |
| Input clamp current, IIK | VI < 0 | −50 | — | mA | p. 4 |
| Output clamp current, IOK | VO < 0 | −50 | — | mA | p. 4 |
| Continuous output current, IO | — | −50 | 50 | mA | p. 4 |
| Continuous current through VCC or GND | — | −100 | 100 | mA | p. 4 |
| Junction temperature | — | — | 150 | °C | p. 4 |
| Storage temperature | — | −65 | 150 | °C | p. 4 |
| ESD, HBM | JS-001 | — | ±8000 | V | p. 4, §5.2 |
| ESD, CDM | JESD22-C101 | — | ±1000 | V | p. 4, §5.2 |

## Recommended operating conditions

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VCCA, VCCB | — | 0.65 | 3.6 | V | p. 5, §5.3 |
| VIH, data inputs | VCCI 1.1–1.95 V | 0.65 × VCCI | — | V | p. 5 |
| VIH, data inputs | VCCI 3–3.6 V | 2 | — | V | p. 5 |
| VIL, data inputs | VCCI 1.1–1.95 V | — | 0.35 × VCCI | V | p. 5 |
| VIL, data inputs | VCCI 3–3.6 V | — | 0.8 | V | p. 5 |
| VIH / VIL, control (DIRx, OE) | VCCA 1.1–1.95 V | 0.65 × VCCA | 0.35 × VCCA | V | p. 5 |
| Input voltage, VI | — | 0 | 3.6 | V | p. 5 |
| Output voltage, active / tri-state | — | 0 | VCCO / 3.6 | V | p. 5 |
| Input transition rate, Δt/Δv | — | — | 10 | ns/V | p. 5 |
| Operating free-air temperature | — | −40 | 125 | °C | p. 5 |

Inputs are overvoltage tolerant up to the 3.6 V VI limit (§7.3.5, p. 20). Unused inputs must be held at VCC or GND (§5.3 note 2, p. 5).

### Electrical characteristics (selected, −40 to 85 °C)

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VOH | IOH = −8 mA, VCC = 1.65 V | 1.2 | — | V | p. 6, §5.5 |
| VOH | IOH = −12 mA, VCC = 3 V | 2.3 | — | V | p. 6 |
| VOL | IOL = 8 mA, VCC = 1.65 V | — | 0.45 | V | p. 6 |
| VOL | IOL = 12 mA, VCC = 3 V | — | 0.7 | V | p. 6 |
| Control input leakage | VI = VCCA or GND | −0.5 | 0.5 | µA | p. 6 |
| Data input leakage | VI = VCCI or GND | −4 | 4 | µA | p. 6 |
| Ioff, A or B port | Own supply at 0 V | −4 | 4 | µA | p. 6 |
| IOZ, A or B port | OE = VIH | −4 | 4 | µA | p. 6 |
| Ci, control / Cio, data | VCC = 3.3 V | — | 4.5 / 6.5 typ | pF | p. 6 |

Integrated static pull-down on every data I/O, 71 kΩ typical; an external pull-up, if any, must be ≤ 7 kΩ (§7.3.9, p. 21). Thermal (PW): RθJA 118.2 °C/W (p. 5, §5.4).

## Power by mode

Static supply current, VI = VCCI or GND, IO = 0 (p. 6, §5.5):

| Condition | VCCA | VCCB | Max, −40 to 85 °C | Max, −40 to 125 °C | Unit |
|---|---|---|---|---|---|
| ICCA, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 15 | 27 | µA |
| ICCB, both supplies on | 0.65–3.6 V | 0.65–3.6 V | 15 | 27 | µA |
| ICCA + ICCB | 0.65–3.6 V | 0.65–3.6 V | 21 | 40 | µA |
| ICCB, VCCA off | 0 V | 3.6 V | 10 | 18 | µA |
| ICCA, VCCB off | 3.6 V | 0 V | 10 | 18 | µA |

Dynamic power: power-dissipation capacitance per transceiver at 25 °C in §5.14 (pp. 15–16); only equal-supply cases (VCCA = VCCB) are tabulated.

## Pinout and package

PW pin numbers (Figure 4-1, Table 4-1, p. 3):

| Pin | Name | Description |
|---|---|---|
| 1 | DIR1 | Direction of bit 1, referenced to VCCA |
| 2 | DIR2 | Direction of bit 2, referenced to VCCA |
| 3–6 | A1–A4 | A-port I/Os, referenced to VCCA |
| 7 | DIR3 | Direction of bit 3, referenced to VCCA |
| 8 | DIR4 | Direction of bit 4, referenced to VCCA |
| 9 | OE | Output enable, active low; high puts all outputs in tri-state; referenced to VCCA |
| 10 | GND | Ground |
| 11–14 | B4–B1 | B-port I/Os (B4 on 11 … B1 on 14), referenced to VCCB |
| 15 | VCCB | B-port supply, 0.65–3.6 V |
| 16 | VCCA | A-port supply, 0.65–3.6 V |

Outline PW0016A (drawing 4220204/B, p. 36): body 4.9–5.1 × 4.3–4.5 mm, lead span 6.2–6.6 mm, 0.65 mm pitch, leads 0.17–0.30 mm, 1.2 mm maximum height; JEDEC MO-153. MSL Level-1-260C-UNLIM, NiPdAu or Sn, −40 to 125 °C, reel 2000 (p. 28).

## Recommended footprint

PW0016A example board layout (p. 37, drawing 4220204/B, scale 10:1): 16 pads 1.5 × 0.45 mm (reference), 0.65 mm pitch, 5.8 mm between pad-row centres (reference); non-solder-mask-defined preferred, 0.05 mm maximum mask clearance. Stencil example on p. 38.

## Application circuit and required passives

- Bypass on VCCA and VCCB close to the device: 0.1 µF recommended; 1 µF and 0.1 µF in parallel improve transient response (§8.4.1, p. 25; Figure 8-1, p. 23).
- OE pulled up so the device stays disabled during power-up, or tied to GND to keep it enabled (Figure 8-1 note, p. 23).
- DIRx pins driven or strapped to valid levels; pins configured as inputs must not float (Table 7-1 note 2, p. 21). Data pins have internal pull-downs.
- Supplies: ground first; no ramp-order or ramp-rate requirement (§8.3, p. 24).

## Interfaces and timing

Function table, per transceiver (Table 7-1, pp. 20–21):

| OE | DIRx | A port | B port | Direction |
|---|---|---|---|---|
| L | L | Output | Input (Hi-Z) | B → A |
| L | H | Input (Hi-Z) | Output | A → B |
| H | X | Input (Hi-Z) | Input (Hi-Z) | Isolation |

Up to 310 Mbps from 1.8 V to 3.3 V (§7.3.10, p. 21).

Switching, VCCA = 1.8 V ± 0.15 V, VCCB = 3.3 V ± 0.3 V, maximum (§5.11, p. 12):

| Parameter | −40 to 85 °C | −40 to 125 °C | Unit |
|---|---|---|---|
| tpd, A → B | 7 | 7 | ns |
| tpd, B → A | 5 | 6 | ns |
| tdis, OE → A | 17 | 18 | ns |
| tdis, OE → B | 18 | 18 | ns |
| ten, OE → A | 19 | 20 | ns |
| ten, OE → B | 18 | 19 | ns |

Minimum tpd in all cases is 0.5 ns.

## Linux driver

None.

## Simulation models

None listed in `manifest.toml` (and the manifest datasheet entry for this MPN points at the wrong document, see header). Whether TI publishes an IBIS model is **UNVERIFIED**.

## Design notes for the T1

- **Per-bit direction.** BOM v1 uses this part for I2S-A BCLK, FS, DIN and DOUT "with per-bit direction". With A = 1.8 V (SoC) and B = 3.3 V (HAT): DOUT is A → B (DIRx = H); DIN is B → A (DIRx = L); BCLK and FS take the direction of whichever side is clock master. If the clock master is fixed in hardware, strap those DIR pins; if it must change at run time, drive them from 1.8 V GPIOs (control inputs are referenced to VCCA, p. 5). The strap-or-GPIO choice is a schematic decision, **UNVERIFIED**.
- **Pull-downs.** The 71 kΩ internal pull-downs (§7.3.9, p. 21) keep floating inputs low when the HAT is absent; any external pull-up on these nets must be ≤ 7 kΩ or it is defeated.
- **Isolation.** OE high, or either supply below 100 mV, puts both ports in high impedance (§7.3.4, p. 20); Ioff ±4 µA (p. 6). Supply order is free and glitch-free (§7.3.6, p. 21).
- **Stock.** BOM v1 flags SN74AXC4T774 stock as thin; its listed alternative SN74AXC4T774RSVR is UQFN-16 with a different pin order (RSV column of Table 4-1, p. 3), so it needs its own footprint.
- **Timing.** 7 ns A → B and 5 ns B → A worst case (p. 12): the BCLK and data paths cross the device in different directions when the HAT is the receiver; the resulting skew against the SoC's I2S setup and hold at the highest sample rate is **UNVERIFIED**.

## Sources

- TI, *SN74AXC4T774 4-Bit Dual-Supply Bus Transceiver with Independent Direction Control, Configurable Voltage Translation, and Tri-State Outputs*, SCES898C, revised May 2022, <https://www.ti.com/lit/ds/symlink/sn74axc4t774.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 95, §4.2
