# TCA6416ARTWR

- **Manufacturer:** Texas Instruments
- **Function:** 16-bit I2C GPIO expander with two supply rails (I2C side VCCI, port side VCCP), interrupt output and reset input
- **BOM v1 lines:** 93 (GPIO expander: slow enables, detects, HAT spare GPIOs)
- **Package:** WQFN-24 (RTW), 4 × 4 mm, 0.5 mm pitch, exposed thermal pad
- **Datasheet:** TCA6416A, SCPS194F (May 2009, revised January 2023), sha256 `a7deab846f35…` in `manifest.toml`
- **Status:** Partly UNVERIFIED

## Summary

The TCA6416A is a 16-bit I/O expander on an I2C bus up to 400 kHz, with separate supplies for the I2C side (VCCI) and the port side (VCCP), so it translates between the two levels (SCPS194F §8.3.1, Table 8-1, p. 19). Every port powers up as an input (Table 5-1, p. 4). In the T1 it drives the slow enables, reads the detects and provides the HAT spare GPIOs (BOM v1 line 93). VCCI is on the 1.8 V I2C2 bus, VCCP is 3.3 V, and the address is 0x21.

## Absolute maximum ratings

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| Supply voltage, VCCI | — | −0.5 | 6.5 | V | SCPS194F p. 5, §6.1 |
| Supply voltage, VCCP | — | −0.5 | 6.5 | V | p. 5 |
| Input voltage, VI | — | −0.5 | 6.5 | V | p. 5 |
| Output voltage, VO | — | −0.5 | 6.5 | V | p. 5 |
| Input clamp current, IIK (ADDR, RESET, SCL) | VI < 0 | — | ±20 | mA | p. 5 |
| Output clamp current, IOK (INT) | VO < 0 | — | ±20 | mA | p. 5 |
| I/O clamp current, IIOK (P port) | VO < 0 or VO > VCCP | — | ±20 | mA | p. 5 |
| I/O clamp current, IIOK (SDA) | VO < 0 or VO > VCCI | — | ±20 | mA | p. 5 |
| Continuous output low current, IOL (P port) | VO = 0 to VCCP | — | 50 | mA | p. 5 |
| Continuous output low current, IOL (SDA, INT) | VO = 0 to VCCI | — | 25 | mA | p. 5 |
| Continuous output high current, IOH (P port) | VO = 0 to VCCP | — | 50 | mA | p. 5 |
| Continuous current through GND | — | — | 200 | mA | p. 5 |
| Continuous current through VCCP | — | — | 160 | mA | p. 5 |
| Continuous current through VCCI | — | — | 10 | mA | p. 5 |
| Junction temperature, TJ | VCC ≤ 3.6 V | — | 130 | °C | p. 5 |
| Junction temperature, TJ | 3.6 V < VCC ≤ 5.5 V | — | 90 | °C | p. 5 |
| Storage temperature, Tstg | — | −65 | 150 | °C | p. 5 |
| ESD, HBM | ANSI/ESDA/JEDEC JS-001 | — | ±2000 | V | p. 5, §6.2 |
| ESD, CDM | JESD22-C101 | — | ±1000 | V | p. 5, §6.2 |

## Recommended operating conditions

| Parameter | Condition | Min | Max | Unit | Reference |
|---|---|---|---|---|---|
| VCCI | −40 °C ≤ TA ≤ 85 °C | 1.65 | 5.5 | V | p. 6, §6.3 |
| VCCI | 85 °C < TA ≤ 125 °C | 1.65 | 3.6 | V | p. 6 |
| VCCP | −40 °C ≤ TA ≤ 85 °C | 1.65 | 5.5 | V | p. 6 |
| VCCP | 85 °C < TA ≤ 125 °C | 1.65 | 3.6 | V | p. 6 |
| VIH, SCL and SDA | — | 0.7 × VCCI | VCCI | V | p. 6 |
| VIH, RESET | — | 0.7 × VCCI | 5.5 | V | p. 6 |
| VIH, ADDR and P17–P00 | — | 0.7 × VCCP | 5.5 | V | p. 6 |
| VIL, SCL, SDA, RESET | — | −0.5 | 0.3 × VCCI | V | p. 6 |
| VIL, ADDR and P17–P00 | — | −0.5 | 0.3 × VCCP | V | p. 6 |
| IOH, P17–P00 | — | — | 10 | mA | p. 6 |
| IOL, P17–P00 | TJ ≤ 65 °C / 85 °C / 105 °C / 125 °C / 135 °C | — | 25 / 18 / 9 / 4.5 / 3.5 | mA | p. 6 |
| Operating free-air temperature, TA | 1.65 V ≤ VCC ≤ 3.6 V | −40 | 125 | °C | p. 6 |
| Operating free-air temperature, TA | 3.6 V < VCC ≤ 5.5 V | −40 | 85 | °C | p. 6 |

SCL and SDA must not sit above VCCI, or supply current rises (p. 6, note 1). The orderable TCA6416ARTWR is listed for −40 to 85 °C in the package option addendum (p. 34), narrower than the −40 to 125 °C of §6.3.

### Electrical characteristics (selected)

| Parameter | Condition | Min | Typ | Max | Unit | Reference |
|---|---|---|---|---|---|---|
| Power-on reset voltage, VPOR (on VCCP) | VI = VCCP or GND, IO = 0 | — | 1 | 1.4 | V | p. 7, §6.5 |
| P-port VOH | IOH = −8 mA, VCCP = 3 V | 2.6 | — | — | V | p. 7 |
| P-port VOL | IOL = 8 mA, VCCP = 3 V, −40 to 125 °C | — | — | 0.25 | V | p. 7 |
| SDA IOL | VOL = 0.4 V | 3 | — | — | mA | p. 7 |
| INT IOL | VOL = 0.4 V | 3 | 15 | — | mA | p. 7 |
| Input leakage, SCL, SDA, RESET, ADDR | VI = VCC or GND | — | — | ±0.1 | µA | p. 7 |
| Input capacitance, SCL | — | — | 6 | 7 | pF | p. 7 |
| I/O capacitance, SDA / P port | — | — | 7 / 7.5 | 8 / 8.5 | pF | p. 8 |

Thermal (RTW): RθJA 43.6 °C/W, RθJC(bot) 10.7 °C/W (p. 6, §6.4).

## Power by mode

ICC = ICCI + ICCP, I/Os as inputs, IO = 0; typical values at VCCP = VCCI = 3.3 V, 25 °C (p. 7, §6.5 and note 1):

| Mode | Condition | VCCP | Typ | Max | Unit |
|---|---|---|---|---|---|
| Operating | fSCL = 400 kHz, −40 to 85 °C | 2.3–3.6 V | 6.5 | 15 | µA |
| Operating | fSCL = 400 kHz, −40 to 85 °C | 1.65–2.3 V | 4 | 9 | µA |
| Standby | fSCL = 0, −40 to 85 °C | 2.3–3.6 V | 1 | 3.2 | µA |
| Standby | fSCL = 0, −40 to 85 °C | 1.65–2.3 V | 0.5 | 1.7 | µA |
| Standby | fSCL = 0, 85 to 125 °C | 2.3–3.6 V | — | 10 | µA |

Extra supply current with an input 0.6 V below its rail: ΔICCI up to 25 µA (SCL, SDA, ADDR) and 55 µA (RESET); ΔICCP up to 80 µA per P-port input at VCCP − 0.6 V (p. 7). A P-port input left between rails costs current (§9.2.2.1, p. 27).

## Pinout and package

RTW pin numbers from Table 5-1 (p. 4):

| Pin | Name | Description |
|---|---|---|
| 1–8 | P00–P07 | Port 0 I/O, push-pull; input at power-on |
| 9 | GND | Ground |
| 10–17 | P10–P17 | Port 1 I/O, push-pull; input at power-on |
| 18 | ADDR | Address input; connect directly to VCCP or GND |
| 19 | SCL | Serial clock; pull-up to VCCI |
| 20 | SDA | Serial data; pull-up to VCCI |
| 21 | VCCP | Port-side supply |
| 22 | INT | Interrupt output, open-drain; pull-up to VCCI or VCCP |
| 23 | VCCI | I2C-side supply; connect to the controller's supply |
| 24 | RESET | Active-low reset; pull-up to VCCI or VCCP if not driven |
| 25 | Thermal pad | Exposed pad (Figure 5-2, p. 3; land 25 on p. 43) |

Outline RTW0024B (drawing 4219135/B, p. 42): body 3.85–4.15 mm square, 0.8 mm maximum height, 0.5 mm pitch, terminals 0.18–0.30 mm wide and 0.3–0.5 mm long, exposed pad 2.45 ± 0.1 mm square. MSL Level-2-260C-1 YEAR, NiPdAu or Sn finish; reel 3000 (p. 34).

## Recommended footprint

RTW0024B example board layout (p. 43, drawing 4219135/B, scale 20:1):

- 24 pads, 0.6 × 0.24 mm (reference), 0.5 mm pitch; pad-row centre spacing 3.8 mm (reference) in both axes.
- Centre pad 25: 2.45 mm square (reference), with five Ø0.2 mm vias shown (centre and ±0.97 mm on each axis).
- Non-solder-mask-defined pads preferred, 0.07 mm maximum mask clearance.
- Stencil: example on p. 44.

## Application circuit and required passives

From Figure 9-1 (p. 26) and §9.2.2 (p. 27):

- Pull-ups on SCL and SDA to VCCI, sized with Rp(min) = (VCC − VOL(max)) / IOL and Rp(max) = tr / (0.8473 × Cb), tr = 300 ns at 400 kHz; total bus capacitance ≤ 400 pF (Equations 1 and 2, p. 27). Figure 9-1 shows 10 kΩ.
- Pull-up on INT (open-drain) and on RESET if it is not driven (Table 5-1).
- Resistors on P-port inputs that may float; outputs need none (Figure 9-1 note E, p. 27).
- Decoupling on VCCP close to the device, a larger and a smaller capacitor (§11.1, p. 31). The datasheet gives no capacitor values (**UNVERIFIED** value; use the usual 100 nF per rail as a design choice).

## Interfaces and timing

I2C target, 7-bit address 0b010000x (Figure 8-6, Table 8-3, p. 21): ADDR = L → 0x20, ADDR = H → 0x21.

Registers (Table 8-4, p. 22): 0x00/0x01 input ports, 0x02/0x03 output ports (default 0xFF), 0x04/0x05 polarity inversion, 0x06/0x07 configuration (1 = input).

I2C timing (§6.6, p. 9):

| Parameter | Standard mode | Fast mode | Unit |
|---|---|---|---|
| fSCL | 0–100 | 0–400 | kHz |
| SCL high, tsch (min) | 4 | 0.6 | µs |
| SCL low, tscl (min) | 4.7 | 1.3 | µs |
| Spike suppression, tsp (max) | 50 | 50 | ns |
| Data setup, tsds (min) | 250 | 100 | ns |
| Data hold, tsdh (min) | 0 | 0 | ns |
| Bus free, tbuf (min) | 4.7 | 1.3 | µs |
| Valid data, tvd(data) (max) | 1 | 0.9 | µs |

Reset (§6.7, p. 9): pulse width tW ≥ 4 ns, recovery tREC 0 ns, time to reset tRESET 600 ns.

Switching (§6.8, p. 9, CL ≤ 100 pF): interrupt valid tIV 4 µs maximum, interrupt reset tIR 4 µs maximum, output data valid tPV 400 ns maximum, input setup tPS 0 ns, input hold tPH 300 ns.

Power-on reset (§10.1, Table 10-1, p. 29): rise and fall rates 0.1–2000 ms; re-ramp after a drop to GND or to VPOR(min) − 50 mV ≥ 1 µs; VCCP may glitch to 1.2 V for ≤ 10 µs without disruption. TI recommends ramping VCCP before VCCI so SDA is not held low (§10.1, p. 29).

Interrupt: any input edge asserts INT after tIV; it clears when the port returns to its original state or when the input register that caused it is read. An output pin never asserts INT; switching a pin from output to input can give a false interrupt (§8.3.3, p. 19).

## Linux driver

Mainline `drivers/gpio/gpio-pca953x.c` (`CONFIG_GPIO_PCA953X`), device-tree compatible `"ti,tca6416"`, with `gpio-controller`, `#gpio-cells = <2>`, and optional `interrupt-controller` on INT. The compatible string is from the mainline driver's match table to the best of this sheet's knowledge; the exact binding text and whether Debian's trixie-backports config enables `GPIO_PCA953X` are **UNVERIFIED** (BOM v1 §3 lists it as not re-checked).

## Simulation models

None listed in `manifest.toml`. Whether TI publishes an IBIS model for this device is **UNVERIFIED**.

## Design notes for the T1

- **Power-up defaults and BRD-019.** All ports are high-impedance inputs after power-on reset (Table 5-1, p. 4; Figure 8-1 note A, p. 18), so the expander itself drives nothing. Each enable it controls needs an external pull-down (or the load's own default) to stay off until software configures it. The output registers default to 0xFF (Table 8-6, p. 22): software must write the output register to 0 before switching a pin to output in the configuration register, or the enable is briefly driven high.
- **Levels.** VCCI 1.8 V with VCCP 3.3 V is a listed combination (Table 8-1, p. 19). P-port VIH is 0.7 × VCCP = 2.31 V at 3.3 V: any 1.8 V-only signal read through a P port will not register high. Detects and spares must be at the 3.3 V level or open-drain with a 3.3 V pull-up.
- **Address.** 0x21 per BOM v1 requires ADDR tied to VCCP (Table 8-3, p. 21).
- **Supply sequencing.** TI recommends VCCP (3.3 V) before VCCI (1.8 V) (§10.1, p. 29). Whether the T1 power tree brings vcc_1v8 up before the 3.3 V rail is **UNVERIFIED** against the power tree; check it before freezing.
- **Temperature.** The RTW orderable is rated −40 to 85 °C (p. 34), enough for a handheld.
- **Current.** At 3.3 V the per-pin limit is 10 mA source and up to 25 mA sink (p. 6); enables and LEDs fit easily. 160 mA total through VCCP (p. 5).

## Sources

- TI, *TCA6416A Low-Voltage 16-Bit I2C and SMBus I/O Expander With Voltage Translation, Interrupt Output, Reset Input, and Configuration Registers*, SCPS194F, revised January 2023, <https://www.ti.com/lit/ds/symlink/tca6416a.pdf>
- OpenDAP board, `docs/specs/bom-v1.md`, line 93, §3, §4.2
