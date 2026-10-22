# BQ25895RTWR

- **Manufacturer:** Texas Instruments
- **Function:** I2C-controlled single-cell 5 A buck charger with NVDC power path, integrated BATFET and 4.5–5.5 V boost (OTG)
- **BOM v1 lines:** 39 (Power, charger and power-path controller), status Proposed; related lines 40 (charger inductor, Coilcraft XAL4020-102MEC) and 48 (board NTC, Murata NCP15XH103F03RC, on TS)
- **BOM v1.5:** removed from line 39 by board ADR 0014 (two-cell battery); replaced by the [BQ25798RQMR](BQ25798RQMR.md). Kept for traceability.
- **Package:** WQFN-24 (RTW), 4 × 4 mm, 0.5 mm pitch, 0.8 mm maximum height, exposed PowerPAD
- **Datasheet:** BQ25895 I2C Controlled Single Cell 5-A Fast Charger with MaxCharge for High Input Voltage and Adjustable Voltage 3.1-A Boost Operation, SLUSC88C (March 2015, revised October 2022), <https://www.ti.com/lit/ds/symlink/bq25895.pdf>
- **Status:** Partly UNVERIFIED

## Summary

The BQ25895 is a 1.5 MHz synchronous buck charger for one Li-ion or Li-polymer cell with narrow-VDC (NVDC) power-path management: an internal BATFET separates SYS from BAT and SYS is held at or above SYS_MIN even with a depleted cell (SLUSC88C p. 1, §3; p. 19, §8.2.6.1). It accepts 3.9–14 V on VBUS, charges at up to 5 A, regulates 3.840–4.608 V in 16 mV steps, includes a 7-bit ADC battery monitor, a TS thermistor input, ship mode and a 3.1 A boost from the battery to PMID (pp. 6–10). In the T1 (board BOM v1 line 39) it is the charger and power-path controller: VBUS_CHG from the TPS2121 mux feeds VBUS, SYS is VSYS for the whole board, BAT goes to the Adafruit 328 pack through the JST PH header, and the host talks to it on I2C1 (1.8 V) at 0x6A. Its boost (OTG) mode is not used; HAT and USB-C 5 V come from a separate TPS61088 boost (power tree v0 §1 finding 9).

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| VBUS (converter not switching) | −2 | 22 | V | SLUSC88C p. 6, §7.1 |
| PMID (converter not switching) | −0.3 | 22 | V | p. 6, §7.1 |
| STAT, DSEL, BTST | −0.3 | 20 | V | p. 6, §7.1 |
| SW | −2 | 16 | V | p. 6, §7.1 |
| SW, peak for 10 ns | −3 | 16 | V | p. 6, §7.1 |
| BAT, SYS (converter not switching) | −0.3 | 6 | V | p. 6, §7.1 |
| SDA, SCL, INT, OTG, REGN, TS, CE, QON | −0.3 | 7 | V | p. 6, §7.1 |
| D+, D− | −0.3 | 7 | V | p. 6, §7.1 |
| BTST to SW | −0.3 | 7 | V | p. 6, §7.1 |
| PGND to GND | −0.3 | 0.3 | V | p. 6, §7.1 |
| ILIM | −0.3 | 5 | V | p. 6, §7.1 |
| Output sink current, INT, STAT | — | 6 | mA | p. 6, §7.1 |
| Output sink current, DSEL | — | 6 | mA | p. 6, §7.1 |
| Junction temperature | −40 | 150 | °C | p. 6, §7.1 |
| Storage temperature | −65 | 150 | °C | p. 6, §7.1 |
| ESD, HBM (JS-001) | — | ±2000 | V | p. 6, §7.2 |
| ESD, CDM (JESD22-C101) | — | ±250 | V | p. 6, §7.2 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| VIN, input voltage | 3.9 | — | 14 | V | p. 6, §7.3 |
| IIN, input current (VBUS) | — | — | 3.25 | A | p. 6, §7.3 |
| ISYS, output current (SW) | — | — | 5 | A | p. 6, §7.3 |
| VBAT, battery voltage | — | — | 4.608 | V | p. 6, §7.3 |
| IBAT, fast charging current | — | — | 5 | A | p. 6, §7.3 |
| IBAT, discharging through internal MOSFET, continuous | — | — | 6 | A | p. 6, §7.3 |
| IBAT, discharging, peak (≤ 1 s) | — | — | 9 | A | p. 6, §7.3 |
| TA, operating free-air temperature | −40 | — | 85 | °C | p. 6, §7.3 |

Selected electrical characteristics (TJ = −40 to 125 °C):

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| VBUS over-voltage (ACOV), rising | — | 14 | 14.6 | V | p. 7, §7.5 |
| VSYS(MIN), SYS_MIN = 3.5 V, ISYS = 0 | 3.50 | 3.65 | — | V | p. 7, §7.5 |
| VSYS(MAX), VBAT = 4.35 V | — | 4.40 | 4.42 | V | p. 7, §7.5 |
| Charge voltage range (16 mV step) | 3.840 | — | 4.608 | V | p. 8, §7.5 |
| Charge voltage accuracy (4.208 / 4.352 V, TJ −40 to 85 °C) | −0.5 | — | 0.5 | % | p. 8, §7.5 |
| Fast charge current range (64 mA step) | 0 | — | 5056 | mA | p. 8, §7.5 |
| Fast charge current accuracy, ICHG = 1792 mA | −5 | — | 5 | % | p. 8, §7.5 |
| Input current limit range (50 mA step) | 100 | — | 3250 | mA | p. 8, §7.5 |
| KILIM (IINMAX = KILIM / RILIM), at 1.5 A | 320 | 355 | 390 | A·Ω | p. 9, §7.5 |
| BATFET on-resistance, TJ = 25 °C | — | 11 | 13 | mΩ | p. 8, §7.5 |
| RBFET / HSFET / LSFET on-resistance, TJ −40 to 85 °C | — | 27 / 27 / 16 | 38 / 39 / 24 | mΩ | p. 8, §7.5 |
| Battery over-voltage, % of VBAT(REG) | — | 104 | — | % | p. 9, §7.5 |
| System over-current (BATFET) threshold | 9 | — | — | A | p. 9, §7.5 |
| Thermal shutdown, rising | — | 160 | — | °C | p. 9, §7.5 |
| PWM switching frequency | 1.32 | — | 1.68 | MHz | p. 9, §7.5 |
| REGN output, VBUS = 9 V, 40 mA | 5.6 | 6 | 6.4 | V | p. 10, §7.5 |
| RθJA (RTW) | — | 31.8 | — | °C/W | p. 7, §7.4 |
| RθJC(bot) | — | 2.0 | — | °C/W | p. 7, §7.4 |

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Battery only, BATFET on (REG09[5] = 0), battery monitor off | High-Z, no VBUS, TJ < 85 °C, from BAT | 32 | 60 | µA | p. 7, §7.5 |
| Ship mode, BATFET off (REG09[5] = 1), battery monitor off | High-Z, no VBUS, TJ < 85 °C, from BAT | 12 | 23 | µA | p. 7, §7.5 |
| Leakage BAT to VBUS | VBAT = 4.2 V, VBUS < UVLO | — | 5 | µA | p. 7, §7.5 |
| HIZ, from VBUS | VBUS = 5 V, no battery, monitor off | 15 | 35 | µA | p. 7, §7.5 |
| HIZ, from VBUS | VBUS = 12 V, no battery, monitor off | 25 | 50 | µA | p. 7, §7.5 |
| Buck, not switching, from VBUS | VBUS > UVLO, VBUS > VBAT | 1.5 | 3 | mA | p. 7, §7.5 |
| Buck, switching, from VBUS | VBAT = 3.2 V or 3.8 V, ISYS = 0 | — | 3 | mA | p. 7, §7.5 |
| Boost, from BAT | VBAT = 4.2 V, I(VBUS) = 0, switching | — | 5 | mA | p. 7, §7.5 |

When the battery monitor (ADC) is active, REGN is enabled and the quiescent current rises; in battery-only mode the monitor only runs when VBAT > SYS_MIN (p. 24, §8.2.8). The ADC rise is not tabulated (**UNVERIFIED**).

## Pinout and package

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | VBUS | P | Charger input; RBFET between VBUS and PMID. 1 µF ceramic to PGND, close to the IC |
| 2 | D+ | AIO | USB D+ for BC1.2 / MaxCharge detection |
| 3 | D− | AIO | USB D− for BC1.2 / MaxCharge detection |
| 4 | STAT | DO | Open-drain charge status; low = charging, high = done or disabled, 1 Hz blink on fault; 10 kΩ pull-up |
| 5 | SCL | DI | I2C clock; 10 kΩ pull-up to the logic rail |
| 6 | SDA | DIO | I2C data; 10 kΩ pull-up to the logic rail |
| 7 | INT | DO | Open-drain interrupt, active-low 256 µs pulse; 10 kΩ pull-up |
| 8 | OTG | DI | Boost enable: boost runs when OTG_CONFIG = 1, OTG high and no input source |
| 9 | CE | DI | Active-low charge enable; must be pulled high or low |
| 10 | ILIM | AI | Resistor to ground sets IINMAX = KILIM / RILIM (regulates 0.8 V); also an input current monitor below 0.8 V; < 500 mA not supported |
| 11 | TS | AI | NTC thermistor input, divider from REGN to TS to GND |
| 12 | QON | DI | BATFET enable / system reset; internal pull-up |
| 13, 14 | BAT | P | Battery positive; 10 µF close to the pins |
| 15, 16 | SYS | P | System output; 20 µF close to the pins |
| 17, 18 | PGND | P | Power ground |
| 19, 20 | SW | P | Switch node to the inductor; 47 nF bootstrap to BTST |
| 21 | BTST | P | High-side driver supply; 47 nF from SW |
| 22 | REGN | P | Low-side driver supply and TS bias; 4.7 µF (10 V) to analog GND |
| 23 | PMID | DO | Boost output / RBFET-HSFET node; ≥ 8.2 µF if OTG is not used |
| 24 | DSEL | DO | Open-drain D+/D− mux select; 10 kΩ pull-up |
| PAD | PowerPAD | P | Solder to the board; vias to PGND and the ground plane |

Source: SLUSC88C pp. 4–5, Figure 6-1, Table 6-1. Package option addendum (p. 57): BQ25895RTWR, WQFN (RTW) 24, 3000 per reel, NiPdAu, MSL Level-2-260C-1 YEAR, −40 to 85 °C, marking BQ25895. Generic package view RTW 24, 4 × 4 mm, 0.5 mm pitch, 0.8 mm maximum height, drawing 4224801/A (p. 61).

## Recommended footprint

The package outline and example land pattern are on pp. 62–64 (RTW0024A) as drawings only; the text layer carries no dimensions. Pad sizes, the thermal-pad opening and the via pattern must be taken from those drawings when the KiCad footprint is drawn (**UNVERIFIED** here). Layout rules (p. 55, §11.1): input capacitor tight to PMID and GND; short, narrow SW trace on a single layer; output capacitor near the inductor and the IC; analog ground routed separately and joined to power ground at the PowerPAD (or through 0 Ω); the PowerPAD soldered with enough thermal vias to the ground plane.

## Application circuit and required passives

From the pin table (pp. 4–5) and the design procedure (§9.2.2, p. 50):

| Position | Value | Note | Source |
|---|---|---|---|
| VBUS to PGND | 1 µF ceramic | close to the IC | p. 4, Table 6-1 |
| PMID to PGND (buck input) | ≥ 8.2 µF, 25 V or higher, X5R/X7R | 8.2 µF is the minimum when OTG is not used; 40 µF (2.4 A) or 60 µF (3.1 A) when OTG is used | p. 5, Table 6-1; p. 50, §9.2.2.2 |
| SYS to PGND | ≥ 20 µF, 6 V or higher, X5R/X7R | with a 1 µH inductor, for loop stability | p. 5; p. 50, §9.2.2.3 |
| BAT to PGND | 10 µF | close to BAT | p. 5, Table 6-1 |
| SW to BTST | 47 nF | bootstrap | p. 5, Table 6-1 |
| REGN to AGND | 4.7 µF, 10 V | close to the IC | p. 5, Table 6-1 |
| Inductor | 1 µH | Isat ≥ ICHG + ½·IRIPPLE; IRIPPLE = VBUS·D·(1−D) / (fs·L), D = VBAT / VBUS | p. 50, §9.2.2.1, Eq. 5–6 |
| ILIM to GND | RILIM = KILIM / IINMAX | KILIM 355 A·Ω typ | p. 4; p. 9 |
| TS divider | RT1 (REGN–TS), RT2 (TS–GND), NTC | Equation 2; example for 103AT, 0–45 °C: RT1 5.21 kΩ, RT2 29.87 kΩ | p. 23, §8.2.7.5.1 |
| STAT, INT, SCL, SDA, DSEL pull-ups | 10 kΩ | to the logic rail | p. 4, Table 6-1 |

The typical application (Figure 9-1, p. 49) uses a 2.2 µH inductor, 40 µF on PMID for 2.4 A OTG and a VREF pull-up rail of 1.8–3.3 V (Table 9-1). The 1 µH figure above is the stated recommendation for loop stability in §9.2.2.3; BOM v1 line 40 follows it.

## Interfaces and timing

- **I2C:** target address **0x6A** (7-bit; p. 28, §8.2.16), registers REG00–REG14. fSCL up to 400 kHz (p. 11, §7.6).
- **I2C thresholds** with a 1.8 V pull-up rail: VIH 1.3 V min, VIL 0.4 V max, VOL 0.4 V at 5 mA, leakage 1 µA (p. 10, §7.5). The same thresholds apply to OTG, CE and QON. A 1.8 V bus is supported.
- **INT:** active-low 256 µs pulse on status or fault (p. 4, Table 6-1; §8.2.9.2).
- **Watchdog:** default 40 s (REG07 WATCHDOG = 01, p. 39); on expiry the device returns to default mode and the watchdog-reset registers go back to their defaults (p. 31, §8.3.1). tWDT for setting 11: 136–160 s (p. 11).
- **QON / ship mode:** QON low 1.25–2.25 s exits ship mode; 12–18 s gives a full system reset (BATFET off 350–550 ms); ship-mode entry delay 10–15 s (p. 11, §7.6).
- **ADC (battery monitor):** 7-bit; VBAT and VSYS in 20 mV steps, VBUS in 100 mV steps, charge current in 50 mA steps, TS as % of REGN; one-shot or 1 s continuous; conversion ≤ 1 s (pp. 10–11; §8.2.8, p. 24).
- **Register defaults relevant to the T1:** VREG 4.208 V (REG06, p. 38); ICHG 2048 mA (REG04, p. 36); IINLIM 500 mA with ILIM pin enabled (REG00, p. 32); SYS_MIN 3.5 V (REG03, p. 35); OTG_CONFIG = 1 and CHG_CONFIG = 1 (REG03, p. 35); AUTO_DPDM_EN = 1, HVDCP and MaxCharge enabled (REG02, p. 34); TREG 120 °C (REG08, p. 40); fast-charge timer 12 h (REG07, p. 39); BATFET_DIS = 0 (REG09, p. 41).

## Linux driver

- Mainline driver `drivers/power/supply/bq25890_charger.c`, Kconfig `CONFIG_CHARGER_BQ25890`; the BOM records it as enabled in Debian (BOM v1 line 39, "mainline + Debian").
- Compatible `ti,bq25895` (the driver also matches `ti,bq25890`, `ti,bq25892`, `ti,bq25896`; list from memory, **UNVERIFIED** against the current source).
- DT properties known from the binding `Documentation/devicetree/bindings/power/supply/bq25890.yaml` (**UNVERIFIED** against the current tree): `ti,battery-regulation-voltage`, `ti,charge-current`, `ti,termination-current`, `ti,precharge-current`, `ti,minimum-sys-voltage`, `ti,boost-voltage`, `ti,boost-max-current`, `ti,use-ilim-pin`, `ti,thermal-regulation-threshold`, `ti,ibatcomp-micro-ohms`, `ti,ibatcomp-clamp-microvolt`, `interrupts`.
- Whether the driver disables the watchdog or kicks it, and whether a DT property exists to clear AUTO_DPDM_EN, is **UNVERIFIED**; check the source before relying on either (see design notes).

## Simulation models

None listed in `manifest.toml` for this part. Vendor models (PSpice or SIMPLIS transient model, EVM files) are **UNVERIFIED**: not checked on ti.com in this session.

## Design notes for the T1

- **OTG is not used, so tie OTG low.** Boost needs OTG_CONFIG = 1 **and** the OTG pin high **and** no input source (§8.2.5, p. 19); OTG_CONFIG resets to 1 (p. 35), so the pin is what keeps the boost off. Condition 2 of §8.2.5 (VBUS below BAT + VSLEEP) confirms that boost cannot run while an input is present, which is the reason for the separate TPS61088 (BOM v1 line 91).
- **PMID:** with OTG unused, ≥ 8.2 µF from PMID to PGND (p. 5), 25 V class because PMID follows VBUS up to the 14 V operating limit (p. 50).
- **SYS:** ≥ 20 µF and a 1 µH inductor (p. 50, §9.2.2.3). The inductor carries system load as well as charge current. Example: VBUS = 9 V, VBAT = 3.8 V, L = 1 µH, fs = 1.5 MHz gives D = 0.42 and IRIPPLE ≈ 1.46 A (Eq. 6, calculated here); at the 3.5 A adapter-powered VSYS budget (power tree §3) the peak is about 4.2 A, inside the ≥ 5 A saturation rating BOM v1 line 40 asks for. Confirm against the XAL4020-102MEC sheet.
- **TS window has no warm/cool (JEITA) registers.** Charge is allowed to start between VLTF (73.25 % of REGN) and VHTF (48.25 %) and continues until VTCO (44.75 %) (p. 9, §7.5; p. 22, §8.2.7.5.1). These are fixed thresholds; the temperature window is set only by the RT1/RT2 divider (Equation 2, p. 23). The only register-selectable thermal limits are the boost-mode BHOT/BCOLD bits (REG01, p. 33), which do not apply because boost is unused. To meet the pack's 0–40 °C charge window (Adafruit 328 sheet), size RT1/RT2 for the Murata NCP15XH103F03RC (B = 3380 K, not the 103AT the datasheet assumes) so that the cut-off point VTCO, not only VHTF, falls at or below 40 °C. The NTC resistance values at 0 °C and 40 °C must come from the Murata R-T table (**UNVERIFIED**, Murata datasheet not downloaded).
- **Watchdog defaults.** If the watchdog expires, ICHG returns to 2048 mA and VREG to 4.208 V (pp. 36, 38). 2048 mA is above the T1 target of 1.2 A but below the pack's 1C (2.5 A); OpenDAP OS must either keep the watchdog serviced or disable it (WATCHDOG = 00, p. 31). For LiHV packs (ADR 0008) a reset falls back to 4.208 V, the safe direction.
- **AUTO_DPDM.** AUTO_DPDM_EN, HVDCP and MaxCharge default to enabled (REG02, p. 34). With AUTO_DPDM_EN = 0 the D+/D− detection is bypassed and IINLIM is used (p. 16, §8.2.3.3). Whether D+/D− connect to the USB 2 lines at all is a board decision; if they do, the device drives D+/D− during detection (DSEL low), so keep detection off unless a mux is fitted.
- **Input current.** The effective input limit is the lower of the ILIM-pin setting and IINLIM (p. 4). IINLIM defaults to 500 mA; TCPM must raise it after PD negotiation. RILIM is not yet chosen (**UNVERIFIED**); for the 3.25 A maximum, RILIM = 355 / 3.25 ≈ 109 Ω (calculated from KILIM typ).
- **VBUS ratings.** ACOV stops switching at 14–14.6 V; absolute maximum 22 V (pp. 6–7). The TPS2121 OV1 setting (≈ 13.7 V, BOM v1 line 45) sits below ACOV.
- **I2C at 1.8 V** is supported (VIH 1.3 V min, p. 10), which closes the BOM v1 line 39 **UNVERIFIED** note. Address 0x6A confirmed (p. 28).
- **Battery-only quiescent** 32 µA typ / 60 µA max, ship mode 12 µA typ / 23 µA max (p. 7); the power tree §4.7 figures match the typical values.
- **Thermal:** RθJA 31.8 °C/W on the reference board (p. 7). Charging at 1.2 A in a sealed 25 mm body needs the thermal vias of §11.1; TREG defaults to 120 °C.

## Sources

- TI BQ25895 datasheet SLUSC88C (March 2015, revised October 2022), <https://www.ti.com/lit/ds/symlink/bq25895.pdf>, sha256 `2667a8d185cbf9138aed63f47616d35c0d0d29da877702b32b301caa55f8d404` (manifest.toml). Page numbers are PDF page numbers (65 pages; pp. 57–64 are the package addenda and drawings).
- Board BOM v1 lines 39, 40, 48 and power tree v0 §1, §3, §4.7 (`public/board/docs/specs/`).
- Linux driver notes from general knowledge of the mainline tree; not re-read in this session (marked **UNVERIFIED** where it matters).
