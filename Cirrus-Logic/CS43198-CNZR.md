# CS43198-CNZR

- **Manufacturer:** Cirrus Logic
- **Function:** Stereo 32-bit audio DAC with pseudodifferential headphone-capable outputs
- **BOM v1 lines:** 18 (Audio, dual-mono DACs), quantity 2
- **Package:** 40-pin 5 mm × 5 mm QFN, tape and reel (DS1156F2, Table 12-1, p. 136)
- **Datasheet:** CS43198 "130-dB, 32-Bit High-Performance DAC with Pseudodifferential Outputs", DS1156F2, December 2022 (manifest sha256 `e2da18e0…dd351d`, verified against the cached copy)
- **Status:** Partly UNVERIFIED

## Summary

The CS43198 is a stereo 32-bit audio DAC with integrated pseudodifferential headphone-capable outputs, a two-mode Class H output stage with internal charge pumps, a PCM serial port (I2S, left/right-justified, TDM, DoP), a dedicated DSD input, a fractional-N PLL and an I2C control port up to 1 MHz (DS1156F2, pp. 1–2). In the T1 two CS43198 run as dual mono (mono mode, one device per channel; DS1156F2, §4.2.3, p. 28), clock master on the serial bus, and drive the OPA1622 headphone amplifiers (BOM line 19). BOM line 18; decided family in board ADR 0001.

## Absolute maximum ratings

GNDD = GNDA = GNDCP = 0 V (DS1156F2, Table 3-3, p. 13).

| Parameter | Symbol | Min | Max | Unit |
|---|---|---|---|---|
| Analog supply | VA | −0.3 | 2.33 | V |
| Battery supply | VP | −0.3 | 6.3 | V |
| Charge-pump supply | VCP | −0.3 | 2.33 | V |
| Filtered charge pump, positive | VCP_FILT+ | −0.3 | 3.3 | V |
| Filtered charge pump, negative | VCP_FILT− | −3.3 | 0.3 | V |
| Digital interface supply | VL | −0.3 | 2.33 | V |
| Digital internal supply | VD | −0.3 | 2.33 | V |
| Input current, any pin except supplies | Iin | — | ±10 | mA |
| Ambient operating temperature (power applied) | TA | −50 | +115 | °C |
| Storage temperature | Tstg | −65 | +150 | °C |

Transient currents up to ±100 mA on the analog input pins do not cause SCR latch-up (DS1156F2, Table 3-3 note 1, p. 13).

## Recommended operating conditions

DS1156F2, Table 3-2, p. 12.

| Parameter | Condition | Min | Max | Unit |
|---|---|---|---|---|
| VA | — | 1.66 | 1.94 | V |
| VCP | — | 1.66 | 1.94 | V |
| VCP_FILT+ (external VCP_FILT mode) | EXT_VCPFILT = 1 | 2.85 | 3.15 | V |
| VCP_FILT− (external VCP_FILT mode) | EXT_VCPFILT = 1 | −3.15 | −2.85 | V |
| VP | HV_EN = 0, EXT_VCPFILT = 0 | 3.0 | 5.25 | V |
| VP | HV_EN = 1, EXT_VCPFILT = 0 | 3.3 | 5.25 | V |
| VP | EXT_VCPFILT = 1 | 3.3 | 5.25 | V |
| VL | — | 1.66 | 1.94 | V |
| VD | — | 1.66 | 1.94 | V |
| Voltage on HP_DETECT | — | −0.3 − VCP_FILT− | VP + 0.3 | V |
| Voltage on VL-domain pins | — | −0.3 | VL + 0.3 | V |
| Voltage on VA-domain pins | — | −0.3 | VA + 0.3 | V |
| Voltage on VP-domain pins | — | −0.3 | VP + 0.3 | V |
| Ambient temperature | TA | −20 | +70 | °C |

With +1dB_EN = 1 the minimum VCP_FILT+ becomes 3.0 V and the maximum VCP_FILT− becomes −3.0 V (Table 3-2 note 2). HV_EN = 1 (VP_LDO = 3.0 V) is required for the 1.7 Vrms full-scale output and needs VP > 3.3 V; HV_EN = 0 (VP_LDO = 2.6 V) limits full scale to 1.4 Vrms (DS1156F2, §4.3 and Table 4-1, p. 29).

Selected analog performance, PCM/DSD processor mode, HV_EN = 1, VP = 3.6 V, TA = 25 °C, 20 Hz–20 kHz (DS1156F2, Table 3-4, pp. 13–14):

| Parameter | Condition | Min | Typ | Max | Unit |
|---|---|---|---|---|---|
| Dynamic range, A-weighted | 24/32-bit, DSD, RL = 10 kΩ or 600 Ω | 124 | 130 | — | dB |
| THD+N | 24/32-bit, 0 dB, +1dB_EN = 0 | — | −115 | −109 | dB |
| Idle channel noise, A-weighted | 24/32-bit, DSD | — | 0.55 | — | µV |
| Full-scale output | +1dB_EN = 0 | 4.66 | 4.90 | 5.14 | Vpp |
| Full-scale output | +1dB_EN = 1 | 5.42 | 5.70 | 5.99 | Vpp |
| Interchannel isolation | 1 kHz | — | 120 | — | dB |
| Output offset, mute | — | — | ±50 | ±100 | µV |
| Load resistance RL | — | 600 | — | — | Ω |
| Load capacitance CL | — | — | — | 1 | nF |
| Turn-on time | — | — | — | 12 | ms |

PSRR, 100 mVpp on the supply, 1 kHz: VA 75 dB, VCP 80 dB, VP 100 dB typical; at 20 kHz: 70, 60 and 80 dB (DS1156F2, Table 3-15, p. 20). Typical PSRR can be about 6 dB below these values (Table 3-15 note 1, p. 21).

## Power by mode

VA = VCP = VD = VL = 1.8 V, VP = 3.6 V, TA = 25 °C, 44.1 kHz mode, +1dB_EN = 1, RL = 600 Ω, CL = 1 nF, no signal (DS1156F2, Table 3-17, p. 21). Currents in µA.

| Mode | iVCP | iVA | iVD | iVL | iVP | Total power |
|---|---|---|---|---|---|---|
| Off (RESET low, VA = VD = VL = VCP = 0 V, VP = 3.6 V) | 0 | 0 | 0 | 0 | 6 | 11 µW |
| Standby (RESET high, HPDETECT enabled, RCO as MCLK) | 0 | 0 | 256 | 0 | 32 | 576 µW |
| Playback quiescent (external MCLK 22.5792 MHz, I2S/DoP, ASP slave, PDN_XTAL = 1) | 3808 | 7835 | 2786 | 0 | 28 | 26 074 µW |

The BOM figure of 26.1 mW per DAC is this quiescent playback row; it excludes current delivered to the load.

Thermal, JEDEC 2s2p board, QFN: θJA 32.7 °C/W, θJB 8.8 °C/W, θJC 0.92 °C/W (DS1156F2, Table 11-1, p. 136).

## Pinout and package

40-pin QFN, 5 mm × 5 mm, 0.4 mm pitch, exposed pad (DS1156F2, Figure 1-1, p. 4; Table 10-1, p. 134). Pin functions from DS1156F2, Table 1-1, pp. 6–7.

| Pin | Name | Domain | Function |
|---|---|---|---|
| 1 | SCL | VL | I2C clock |
| 2 | SDIN1 | VL | ASP serial data in |
| 3 | TSO | — | Test output |
| 4 | VD | — | Internal digital supply, 1.8 V |
| 5 | FILT+ | VA | Positive DAC reference |
| 6 | FILT− | VA | Negative DAC reference |
| 7 | VA | — | Analog supply, 1.8 V |
| 8 | GNDA | — | Analog ground |
| 9 | −VA | VA | Negative charge-pump output for the DAC rail |
| 10 | FLYP_VA | VA | −VA charge-pump flying capacitor, positive node |
| 11 | FLYN_VA | VA | −VA charge-pump flying capacitor, negative node |
| 12, 15, 19 | GNDCP | — | Charge-pump ground |
| 13 | REFA | VCP_FILT± | Output reference, channel A |
| 14 | AOUTA | VCP_FILT± | Audio output A |
| 16 | AOUTB | VCP_FILT± | Audio output B |
| 17 | REFB | VCP_FILT± | Output reference, channel B |
| 18 | VCP_FILT− | VCP/VP | Negative output-stage rail (filter capacitor or external supply) |
| 20 | FLYN_VCP | VCP_FILT± | Output charge pump, flying capacitor negative node |
| 21 | VCP_FILT+ | VCP/VP | Positive output-stage rail |
| 22 | HP_DETECT | VP | Headphone detect input |
| 23 | FLYC_VCP | VCP/VP | Output charge pump, flying capacitor centre node |
| 24 | FLYP_VCP | VCP/VP | Output charge pump, flying capacitor positive node |
| 25 | VCP | — | Charge-pump supply, 1.8 V |
| 26 | VP | — | Battery supply for the Class H circuit |
| 27 | INT | VP | Interrupt, open drain, active low |
| 28 | RESET | VP | Reset, active low |
| 29 | DSDB/LRCK2 | VL | DSD data B / XSP word clock |
| 30 | ADR | VL | I2C address select |
| 31 | VL | — | Interface supply, 1.8 V |
| 32 | DSDCLK/SCLK2 | VL | DSD clock / XSP bit clock |
| 33 | CLKOUT | VL | Clock output |
| 34 | SCLK1 | VL | ASP bit clock |
| 35 | GNDD | — | Digital ground |
| 36 | XTO | VL | Crystal output |
| 37 | XTI/MCLK | VL | Crystal input or external MCLK input |
| 38 | LRCK1 | VL | ASP word clock |
| 39 | SDA | VL | I2C data |
| 40 | DSDA/SDIN2 | VL | DSD data A / XSP serial data in |
| EP | Thermal pad | — | Connect to ground (GNDA in split-ground systems) |

GNDA, GNDCP and GNDD must meet in a common ground area under the chip (DS1156F2, Table 1-1, p. 7). The digital inputs have weak pull-downs of 550–2450 kΩ (Table 3-11, p. 19).

Package dimensions (DS1156F2, Table 10-1, p. 134): body 5 × 5 mm BSC; height 0.70/0.75/0.80 mm; pitch 0.4 mm; lead width b 0.15/0.20/0.25 mm; lead length L 0.35/0.40/0.45 mm; exposed pad J × K 3.4/3.5/3.6 mm.

## Recommended footprint

DS1156F2 gives package dimensions (Table 10-1, p. 134) but no recommended land pattern. The thermal pad must mate with a copper pad connected to ground through a via array to inner ground planes (DS1156F2, §8.4, p. 121). Land dimensions, paste-mask segmentation of the exposed pad and via count: **UNVERIFIED** (to be derived from Table 10-1 to IPC-7351 in `kicad-lib`).

## Application circuit and required passives

From DS1156F2, Figure 2-1 (p. 10) and Figure 2-2 (mono mode, p. 11). Values are nominal. "*" capacitors are low-ESR X7R/X5R; crystal load capacitors are C0G.

| Node | Part | Note |
|---|---|---|
| VL | 0.1 µF | 1.8 V |
| VD | 0.1 µF | 1.8 V |
| VP | 0.1 µF + 4.7 µF | 3.0–5.25 V |
| VA | 2.2 µF | 1.8 V |
| FILT+ | 15 µF to VA side | — |
| FILT− | 15 µF to −VA side | — |
| −VA | 2.2 µF | — |
| FLYP_VA – FLYN_VA | 2.2 µF flying capacitor | — |
| VCP (EXT_VCPFILT = 0) | 2.2 µF | 1.8 V |
| VCP_FILT+, VCP_FILT− (EXT_VCPFILT = 0) | 2.2 µF each to GNDCP | Internal charge pump |
| FLYP_VCP – FLYC_VCP, FLYC_VCP – FLYN_VCP (EXT_VCPFILT = 0) | 2.2 µF each | — |
| VCP_FILT± (EXT_VCPFILT = 1) | external ±3.0 V, 2.2 µF each; FLYN_VCP not connected; one 2.2 µF FLYP–FLYC | External-rail mode |
| SDA, SCL, INT | Pull-ups RP to VL | RP ≥ 350 Ω at VL = 1.8 V (Table 3-20, p. 23); INT sink 825 µA at VOL 0.3 V (Table 3-11, p. 19) |
| ADR | 0 Ω or 4.99 kΩ (5 %) to VL or GND | Sets the two LSBs of the I2C address (Table 4-12, p. 52) |

Layout rules (DS1156F2, §8, p. 121): VA and VCP on independent clean supplies, VL and VD may share the system logic supply; smallest capacitor closest to the pin on the same side; keep clocks away from FILT+ and FILT−; FILT+ capacitor path short to VA, FILT− to −VA; VCP_FILT± capacitors short to GNDCP; route REFA and REFB independently to the headphone connector ground pin.

Power sequencing (DS1156F2, §5.2, p. 55): VP first; the other supplies in any order before RESET is released. Power-down: assert RESET, remove VA/VCP/VL/VD in any order, VP last. RESET low pulse ≥ 1000 µs (Table 3-11, p. 19); I2C is available tPUD ≥ 1500 µs after RESET is released (Table 3-20, p. 23).

## Interfaces and timing

- **MCLK:** external MCLK on XTI/MCLK must be 22.5792 or 24.576 MHz, duty cycle 45–55 %, and meet the phase-noise mask of Figure 4-11 (DS1156F2, §4.5.1, p. 35). Read from Figure 4-11: about −95 dBc/Hz at 100 Hz falling to about −116 dBc/Hz at 100 kHz and flat above (values read from the plot, not tabulated). Other reference frequencies (11.2896, 12.288, 9.6, 19.2, 12, 24, 13, 26 MHz) need the PLL, reference jitter ≤ 50 ps, lock time 620 µs typical, 1000 µs maximum (Table 3-13, p. 20). XTI/MCLK is a VL-domain input: VIH ≥ 0.7·VL, VIL ≤ 0.3·VL (Table 3-11, p. 19), absolute limit VL + 0.3 V (Table 3-2, p. 12).
- **Crystal option (unused in T1):** 22.57–24.58 MHz, CL 5–8 pF, ESR ≤ 100 Ω, start-up ≤ 6.5 ms (Table 3-14, p. 20).
- **ASP (PCM, DoP):** 32–384 kHz; I2S, left/right-justified, TDM (p. 2). Slave mode: SCLK ≤ 24.58 MHz, SCLK high/low ≥ 16 ns, setup 10 ns, hold 5 ns. Master mode: SCLK ≤ fMCLK_INT, FSYNC delay ≤ 10 ns after the launching edge (Table 3-18, pp. 21–22).
- **DSD input (XSP pins):** DSD64/128/256; DSDCLK maximum fMCLK_INT/8, /4, /2; setup and hold 10 ns; DSDCLK duty cycle 40–60 % (Table 3-19, pp. 22–23).
- **I2C:** standard, fast and fast-mode-plus, fSCL ≤ 1000 kHz (Table 3-20, p. 23). 7-bit address 0b01100 followed by AD1 AD0 from the ADR strap, i.e. 0x30–0x33 (Figure 4-29 and Table 4-12, p. 52). Register addresses are 24-bit (three MAP bytes, p. 52).
- **Logic levels (VL, non-I2C):** VOH ≥ 0.9·VL at −100 µA, VOL ≤ 0.1·VL (Table 3-11, p. 19).
- **HP_DETECT:** VIH ≥ 0.93·VP, VIL ≤ 2.0 V (Table 3-11, p. 19).

## Linux driver

- Mainline driver `sound/soc/codecs/cs43130.c` (`SND_SOC_CS43130`), which matches `cirrus,cs43130`, `cirrus,cs4399`, `cirrus,cs43131` and `cirrus,cs43198` (checked in the mainline source on 2026-10-22).
- Device-tree binding: `Documentation/devicetree/bindings/sound/cs43130.txt` — required `reg`, `VA-supply`, `VP-supply`, `VL-supply`, `VCP-supply`, `VD-supply`; optional `reset-gpios`, `cirrus,xtal-ibias`, `cirrus,dc-measure`, `cirrus,ac-measure`, `cirrus,dc-threshold`, `cirrus,ac-freq` (checked in the mainline source on 2026-10-22).
- The driver exposes ASP PCM, ASP DoP and XSP DoP DAIs, 1–2 channels. PCM rates are constrained to 32, 44.1, 48, 88.2, 96, 176.4, 192, 352.8 and 384 kHz; DoP rates to 176.4 and 352.8 kHz, i.e. DSD64 and DSD128 (mainline source, 2026-10-22). This is the DSD128 cap noted in opendap-os ADR 0006.
- Debian: `SND_SOC_CS43130` is not enabled in the trixie-backports arm64 config, so the T1 builds it through DKMS (BOM v1 line 18; opendap-os ADR 0007).
- Mono-mode (one device per channel) configuration through the driver: **UNVERIFIED**.

## Simulation models

No IBIS, SPICE or other model is listed in `manifest.toml` for this part. Availability of an IBIS model from Cirrus Logic: **UNVERIFIED**.

## Design notes for the T1

- Dual mono: one CS43198 per channel in mono mode (DS1156F2, §4.2.3, p. 28; Figure 2-2, p. 11); mono enable and disable sequences are in §5.11 (p. 64).
- All of VA, VCP, VD and VL are 1.8 V parts (1.66–1.94 V). VA has its own low-noise LDO per DAC (BOM line 29, TPS7A2018); VL and VD can share the logic rail (DS1156F2, §8.1, p. 121).
- XTI/MCLK is a 1.8 V VL input. The T1 drives it from 3.3 V NDK NSC5083D oscillators through a passive attenuator (board ADR 0010); the attenuated edge must respect VIH ≥ 0.7·VL and the VL + 0.3 V limit (Tables 3-11, 3-2).
- The I2C pins are VL-domain (1.8 V); the DACs share the 1.8 V PMUIO2 bus. Give the two DACs different ADR straps.
- RESET and INT are VP-domain pins (Table 1-1); the RESET driver and INT pull-up levels against VP and VL: **UNVERIFIED** for the T1 netlist.
- VP must come up first and go down last (§5.2); Popguard and the power-up/down sequences in §5.5–5.7 (pp. 56–58) govern pop behaviour together with OPA1622 EN sequencing (BOM line 100).
- Exposed pad to GNDA with a via array (§8.4).

## Sources

- Cirrus Logic, CS43198 data sheet, DS1156F2, December 2022, <https://www.cirrus.com/docs/ds/cs43198-datasheet.pdf>, sha256 `e2da18e07a5683ee9eb134154a31ac7f8a197587c01c250c42286ea604dd351d`.
- Linux mainline, `sound/soc/codecs/cs43130.c` and `Documentation/devicetree/bindings/sound/cs43130.txt`, read 2026-10-22.
- OpenDAP board BOM v1, line 18; board ADR 0001, ADR 0010; opendap-os ADR 0006, ADR 0007.
