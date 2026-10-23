# BQ25798RQMR

- **Manufacturer:** Texas Instruments
- **Function:** I2C-controlled 1–4 cell, 5 A buck-boost battery charger with NVDC power path, dual-input selector, MPPT and backup mode
- **BOM v1 lines:** 39 (Power, charger and power path for the two-cell pack, qty 1; BOM v1.5, board ADR 0014, replaces the [BQ25895RTWR](BQ25895RTWR.md)); inductor on line 40 ([XAL4020-102MEC](../Coilcraft/XAL4020-102MEC.md)); passives on line 115
- **Package:** VQFN-HR-29 (RQM), 4.0 × 4.0 mm
- **Datasheet:** *BQ25798 I2C Controlled, 1- to 4-Cell, 5-A Buck-Boost Battery Charger with Dual-Input Selector, MPPT for Solar Panels and Fast Backup Mode*, SLUSDV2C, May 2020, revised June 2026, 152 pages. Cited below as "SLUSDV2C". File sha256 `163e45683f62f208545920e1470054b352b4a4b0cdc201e1f19fcb1007f1e222` (the copy read by the board 2S battery study and this sheet).
- **Status:** Partly UNVERIFIED

## Summary

The BQ25798 is a synchronous buck-boost charger for 1- to 4-cell Li-ion packs with a narrow-voltage-DC (NVDC) power path, an input range of 3.6–24 V, up to 5 A charge current, an integrated 11 mΩ battery FET, two input ports with external back-to-back FET drivers (ACDRV1/2), USB BC1.2 detection, MPPT for solar inputs, a backup mode that reverses the converter when the adapter is removed, OTG output 2.8–22 V, and an I2C interface (SLUSDV2C, pp. 1, 4–6). In the T1 it charges the two-cell pack and makes VSYS (6.0–8.8 V) for the VSYS_LV pre-regulator and the HAT/USB-C bucks (board BOM v1.5, power tree v0 §2, §4.7). Its OTG converter is not used, because it cannot run while charging (board 2S study §3.1).

## Absolute maximum ratings

SLUSDV2C, p. 7, §6.1. Voltages with respect to GND.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VAC1, VAC2 | −2 | 30 | V |
| VBUS (converter not switching) | −2 | 30 | V |
| PMID (converter not switching) | −0.3 | 30 | V |
| ACDRV1, ACDRV2, BTST1 | −0.3 | 32 | V |
| SYS (converter not switching) | −0.3 | 23 | V |
| BATP, BAT | −0.3 | 20 | V |
| BTST2 | −0.3 | 29 | V |
| SDRV | −0.3 | 26 | V |
| SW1 | −2 (50 ns) | 30 | V |
| SW2 | −2 (50 ns) | 23 | V |
| QON, D+, D−, CE, STAT, SCL, SDA, INT, ILIM_HIZ, PROG, TS, REGN | −0.3 | 6 | V |
| INT, STAT sink current | | 6 | mA |
| BTST1–SW1, BTST2–SW2, PMID–VBUS, SDRV–BAT (differential) | −0.3 | 6 | V |
| SYS–BAT (differential) | −0.3 | 16 | V |
| TJ | −40 | 150 | °C |
| Tstg | −55 | 150 | °C |

ESD (SLUSDV2C, p. 7, §6.2): HBM ±2000 V; CDM ±250 V.

## Recommended operating conditions

SLUSDV2C, pp. 7–8, §6.3.

| Parameter | Min | Max | Unit |
|---|---|---|---|
| VBUS input voltage | 3.6 | 24 | V |
| VBAT | | 18.8 | V |
| IVBUS input current | | 3.3 | A |
| ISW output current (SW) | | 5 | A |
| Fast charging current | | 5 | A |
| IBAT RMS discharge current, continuous | | 6 | A |
| IBAT peak discharge current, up to 1 s | | 10 | A |
| TA | −40 | 85 | °C |
| TJ | −40 | 125 | °C |
| Effective capacitance: VBUS / PMID / SYS / BAT | 2 / 4 / 6 / 3 | | µF |
| Effective PMID capacitance with backup mode | 70 | | µF |

Programmable ranges (SLUSDV2C, p. 10): VSYSMIN 2.5–16 V in 250 mV steps; charge voltage VREG 3–18.8 V; charge current 0.05–5 A; input current limit IINDPM 0.1–3.3 A (p. 12); OTG 2.8–22 V, 0.12–3.32 A (p. 15). With VBAT below VSYSMIN at 2S, VSYS regulates at 7.12 / 7.2 / 7.52 V (p. 10). Battery OCP (IBAT_OCP) 9.3 A minimum (p. 12). VBUS overvoltage 25.2 / 25.7 / 26.2 V rising (p. 9).

Thermal (SLUSDV2C, p. 8, §6.4): RθJA 44.2 °C/W, RθJC(top) 20.9 °C/W, RθJB 9.7 °C/W, ΨJT 0.5 °C/W, ΨJB 9.7 °C/W.

## Power by mode

SLUSDV2C, p. 8, §6.5 (VBAT = 8 V, TJ < 85 °C).

| Mode | Condition | Typ | Max | Unit |
|---|---|---|---|---|
| Battery only, BATFET on, ADC off | No VBUS, I2C enabled | 17 | 24 | µA |
| Battery only, BATFET on, ADC on | No VBUS | 540 | | µA |
| Ship mode | No VBUS, I2C enabled, ADC off | 11 | 16 | µA |
| Shutdown | No VBUS, I2C disabled | 0.5 | 0.7 | µA |
| Input quiescent, switching, charge disabled | VBUS 15 V, ISYS 0 A, OOA off / on | 3 / 5 | | mA |
| HIZ, no battery | VBUS 15 V, ACDRV off / on | 386 / 590 | | µA |
| OTG, switching | VBAT 8 V, VBUS 5 V, IVBUS 0 A, OOA off / on | 3 / 5 | | mA |

## Pinout and package

29-pin VQFN-HR (RQM), 4 × 4 mm (SLUSDV2C, p. 4, Figure 5-1; pp. 4–6, Table 5-1).

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | STAT | DO | Open-drain charge status; 10 kΩ pull-up |
| 2–3 | VBUS | P | Charger input; 2 × 10 µF + 0.1 µF |
| 4 | BTST1 | P | Q1 gate-drive bootstrap, 47 nF 10 V to SW1 |
| 5 | REGN | P | Internal LDO output, 4.7 µF 10 V |
| 6, 7 | D+, D− | AIO | USB BC1.2 detection on input 1 |
| 8, 9 | VAC2, VAC1 | P | Input detection; tie to VBUS when ACFET/RBFET are not fitted |
| 10, 11 | ACDRV2, ACDRV1 | P | Input FET drivers; tie to GND when not fitted |
| 12 | QON | DI | Ship-mode exit / system reset |
| 13 | CE | DI | Active-low charge enable; never floating |
| 14, 15 | SCL, SDA | DI, DIO | I2C; 10 kΩ pull-ups |
| 16 | TS | AI | NTC input (TI recommends a 103AT-2 10 kΩ) |
| 17 | ILIM_HIZ | AI | Input current limit / HIZ by divider |
| 18 | BATP | P | Battery voltage sense, 100 Ω series |
| 19 | BTST2 | P | Q4 bootstrap, 47 nF 10 V to SW2 |
| 20 | PROG | AI | Power-on defaults (switching frequency, charge profile) by resistor |
| 21 | INT | DO | Open-drain interrupt, 256 µs low pulse |
| 22–23 | BAT | P | Battery; 2 × 10 µF |
| 24 | SDRV | P | External ship-FET gate drive; 1 nF 50 V to GND when unused |
| 25 | SYS | P | System output; 5 × 10 µF + 0.1 µF |
| 26 | SW2 | P | Boost-side switch node |
| 27 | GND | P | Ground |
| 28 | SW1 | P | Buck-side switch node |
| 29 | PMID | P | Q1 drain; 3 × 10 µF + 0.1 µF |

Ordering (SLUSDV2C, package option addendum, p. 145): BQ25798RQMR, 3000 per 13″ reel, Sn, MSL 2 at 260 °C (1 year), −40 to 85 °C, marking BQ25798.

## Recommended footprint

TI package outline, land pattern and stencil for RQM: SLUSDV2C, pp. 148–150. Dimensions are not transcribed here: **UNVERIFIED** until the footprint is drawn against those pages. Layout guidance (SLUSDV2C, pp. 139–142): input, PMID, SYS and BAT capacitors close to the pins; the inductor connects SW1 and SW2 through vias under the IC.

## Application circuit and required passives

- Capacitors (SLUSDV2C, Table 5-1 and §8.2.2.3–§8.2.2.4, pp. 4–6, 134–135): VBUS 2 × 10 µF + 0.1 µF; PMID 3 × 10 µF + 0.1 µF, 25 V or higher for up to 20 V input (plus 2 × 33 µF POSCAP only for backup mode); SYS 5 × 10 µF + 0.1 µF, 16 V or higher at 2S; BAT 2 × 10 µF; REGN 4.7 µF 10 V; BTST1, BTST2 47 nF 10 V.
- **Inductor** (SLUSDV2C, §8.2.2.2, p. 133): 1 µH at 1.5 MHz or 2.2 µH at 750 kHz, and only those pairs. Saturation current above the converter's maximum current (input, charge, discharge or OTG) plus half the ripple, and at least 2 A for PFM pulses. The typical characteristics use a TDK SPM6530T-1R0M120 (1 µH) and a Würth WE-LHMI 74437346022 (2.2 µH) (§6.7, pp. 17–22).
- PROG resistor and ILIM_HIZ divider per §7.3.2 and pin 17 (pp. 4–6, 25).

## Interfaces and timing

- I2C target at 7-bit address **0x6B** (SLUSDV2C, §7.5, p. 54). VIH_SDA 1.3 V and VIL_SDA 0.4 V with a 1.8 V pull-up rail (p. 15), so the T1's 1.8 V I2C1 works without translation.
- INT: 256 µs active-low pulse on status and fault changes (pin 21).
- PWM switching frequency 1.5 MHz or 750 kHz, set by PROG at power-up and by register (p. 14; §7.3.2, p. 25).

## Linux driver

Mainline `drivers/mfd/bq257xx.c` and `drivers/power/supply/bq257xx_charger.c` bind only `ti,bq25703a` and `ti,bq25792`; the BQ25798 has no ID entry, and Debian leaves `MFD_BQ257XX` unset (board 2S study §3.1). Board ADR 0014 item 5: add the BQ25798 ID upstream after confirming its register map against the BQ25792 support, and ship it through DKMS meanwhile (blackbird-os ADR 0007, OS-023). Register compatibility with the BQ25792 is **UNVERIFIED**.

## Simulation models

None named in the datasheet. TI's product page tools were not checked: **UNVERIFIED**. No manifest entry beyond the datasheet.

## Design notes for the T1

- **2S settings:** VREG 8.40 V for 4.2 V cells; LiHV packs at up to 2 × 4.40 V sit inside the 3–18.8 V range in 10 mV steps (board ADR 0008). Charge current per the quoted pack (board BOM line 46).
- **Margins (BRD-049, board power tree §4.10):** battery discharge 2.4 A at the full output budget = 40 % of 6 A; IINLIM 2.0 A = 61 % of 3.3 A; ISW on adapter ≤ 2.25 A (15 W input cap at VSYS 6.0 V) = 45 % of 5 A. IBAT_OCP (9.3 A minimum) sits above the 4 A board fuse, so the fuse and the pack PCM are the protections that act first.
- **Input topology:** VAC1 and VAC2 tied to VBUS and ACDRV1/2 to GND; the TPS2121 stays the input mux (board BOM line 45). The dual-input selector is not used.
- **OTG:** not used; HAT_5V and the USB-C source come from a TPS62903 buck (board BOM line 91).
- **TS:** takes the pack NTC through the battery connector; the TS window must match the NTC type fixed in the pack specification (**UNVERIFIED** until then).
- **Thermal:** TA rated only to 85 °C (p. 7); check the charger's neighbourhood in the board thermal model.

## Sources

- TI, BQ25798 datasheet, SLUSDV2C (June 2026): <https://www.ti.com/lit/ds/symlink/bq25798.pdf>
- OpenDAP board ADR 0014 and BOM v1.5, lines 39–40, 115; power tree v0 §2, §4.7, §4.10; board 2S battery study §3.1, §4.4 (`public/board/docs/`).
- Mainline Linux `drivers/mfd/bq257xx.c` (read through the board 2S study).
