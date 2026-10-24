# LBES5PL2EL-923

- **Manufacturer:** Murata
- **Function:** Murata Type 2EL, shielded Wi-Fi 6 (802.11a/b/g/n/ac/ax, 2.4 and 5 GHz, 1×1) + Bluetooth 5.4 BR/EDR/LE + IEEE 802.15.4 module on the NXP IW612
- **BOM v1 lines:** 55 (module), 56 (U.FL antenna connectors), 57 (antennas), 58 (matching networks), 103 (item tracking baseline)
- **Package:** LGA, 8.8 × 7.7 mm outline, 107 pads (pins 1–80 signal and ground, 81–107 ground), 1.3 mm high (product brief)
- **Datasheet:** Murata's *Type 2EL Datasheet* was not obtained: the product page links it at `https://pim.murata.com/asset/pim4/wifiBluetoothModule/TYPE2EL_PDF`, which answered 403 to every non-browser fetch on 2026-10-24. The values below come from Murata's design documents listed here and are cited by their document numbers:
  - *Type 2EL/2DL Hardware Application Note*, E2B-09-1413 Rev. 9.0, 2026-05-21, 36 pages, sha256 `aade44c588030b5bc4e9e436b6fe01d5ad21826d369849ede8dae6b3b27476ea`. Cited as "E2B-09-1413".
  - *Type 2EL/2DL/2LL/2KL Unified Design Guide*, E2B-54-1953 Rev. 2.0, 2025-08-21, 19 pages, sha256 `eaecfe5d476c7027f4fc3718bb13f727348346eb084c44eb97724ebe447b0443`. Cited as "E2B-54-1953".
  - *Type 2EL Radio Law Certification Application Note*, CER-0248 Rev. 6.0, 2025-03-04, 75 pages, sha256 `f37a17254d420bedec628e284cc12ac83c48141589ba0de03ce573973e7a69ed`. Cited as "CER-0248".
  - *Type 2EL Product Brief*, March 2023, sha256 `73077ec9d01d6661796ac6cf67f796e707f6fad08a4b61156d52323e4b4eb598`.
  - Module footprint, top view (DXF, 2023-07-13), sha256 `b9979fee8cb0ad645944f82bdc85baac4b92061e385d450f8130526bcb4c4970`; RF trace to u.FL layout (DXF, 2023-07-13), sha256 `a8387fa54dba76e6f73c261cad7df9bc927cd30fae8b5daa2cf5d9fcd38754f3`.
  - Secondary (a carrier board, not the module): Embedded Artists *2EL / 2DL M.2 Module Datasheet*, rev PA4, 2024-08-05, "Preliminary", sha256 `b5b0ce7c22855e326151b4923e6a334d0d7eefc48b1558f17c94f1b3c41b4308`. Cited as "EA M.2 PA4".
- **Availability (2026-10-21/22, from BOM v1 line 55):** Digi-Key 938; Mouser 2,820; LCSC 0; prices not recorded. Second source per the BOM: u-blox MAYA-W271-00B (same chip).
- **Status:** Partly UNVERIFIED. Without the module datasheet, the absolute maximum ratings, supply ranges, power sequencing, pin electrical levels and the recommended land pattern dimensions are **UNVERIFIED**.

## Summary

Type 2EL is an IW612-based module with Wi-Fi 802.11a/b/g/n/ac/ax 1×1 in the 2.4 and 5 GHz bands (20/40/80 MHz, up to 600 Mbps PHY), Bluetooth 5.4 BR/EDR/LE and IEEE 802.15.4 (E2B-09-1413 §2, §2.1). There is no 6 GHz band (block diagrams, E2B-09-1413 Figures 1–2; brief "2.4 and 5 GHz"). Host interfaces: SDIO 3.0 for Wi-Fi; HCI UART, PCM and I2S for Bluetooth; SPI for 802.15.4 (E2B-09-1413 §2.1). The module takes three supply groups: AVDD33 (3.3 V), AVDD18 (1.8 V) and the I/O rails VIO and SD_VIO (E2B-09-1413 Figure 1). In the T1 it provides Wi-Fi over SDIO on `sdmmc1` (VCCIO4, 1.8 V) and Bluetooth over UART1 M0 with RTS/CTS; Bluetooth audio runs over HCI (BOM v1 line 55, board ADR 0006).

What changes the board compared with BOM v1:

- **AVDD18 is a power rail, not only I/O.** Bluetooth and 802.15.4 transmit draw 323–390 mA typical from AVDD18 alone (E2B-09-1413 Tables 20–21), and Wi-Fi 5 GHz transmit 255 mA from AVDD18 plus 210–240 mA from AVDD33 (Table 19). The BOM names only a 3.3 V supply and a 1.8 V VIO.
- **Two RF pins plus a Bluetooth input:** ANT0 (pin 15), ANT1 (pin 23) and BT_15.4_IN (pin 18). The two-U.FL layout of BOM line 56 is Murata's "dedicated Bluetooth/802.15.4 antenna" configuration (E2B-09-1413 §2.2, §3.1).
- **The modular approval is for mobile use (≥ 20 cm from the body) in the USA and Canada.** A handheld T1 needs a Class II (FCC) / Class 4 (ISED) permissive change with SAR testing of the final product (CER-0248 pp. 26–27, 35).
- **The Molex 146187 is not on the FCC or ISED antenna lists.** It appears only in the additional Japan list, with a "50 mm or more" cable; the -0050's cable is 43.3 mm (CER-0248 p. 68; E2B-09-1413 Table 4; Molex drawing 1461870050).

## Absolute maximum ratings

**UNVERIFIED** (module datasheet not obtained).

Secondary, for the Embedded Artists M.2 carrier only (its single 3.3 V input feeds AVDD33 directly and an on-board buck for the 1.8 V rails): 0.0 V to 3.63 V on the carrier supply (EA M.2 PA4, p. 8). This is not a module rating.

## Recommended operating conditions

| Parameter | Value | Reference |
|---|---|---|
| AVDD33 | 3.3 V (test condition of every Murata measurement) | E2B-09-1413 §5 conditions |
| AVDD18 | 1.8 V (test condition) | E2B-09-1413 §5 conditions |
| VIO, SD_VIO | 1.8 V (test condition; "SDIO Signal Level = 1.8V") | E2B-09-1413 §5.1.1, §5.3.1 |
| Interface voltage | "1.8 or 3.3" V | Product brief, specification table |
| Operating temperature | −40 to +85 °C | Product brief, specification table |
| Supply ranges (min/max per rail) | **UNVERIFIED** (datasheet) | — |

The T1 runs VIO and SD_VIO at 1.8 V (BOM v1 line 55, VCCIO4). The BOM's 3.3 V source is RK809 SWOUT1; its capability for the module's current is **UNVERIFIED** here.

## Power by mode

Typical, AVDD18 = 1.8 V, AVDD33 = 3.3 V, SD_VIO/VIO = 1.8 V (E2B-09-1413 §5).

| Mode | AVDD18 | AVDD33 | Reference |
|---|---|---|---|
| Wi-Fi 2.4 GHz TX, 11b 1 Mbps, 18 dBm | 150 mA | 235 mA | Table 18, p. 28 |
| Wi-Fi 2.4 GHz TX, 11ax HE40 MCS0, 15 dBm | 170 mA | 190 mA | Table 18, p. 28–29 |
| Wi-Fi 2.4 GHz RX (20/40 MHz) | 100 / 110 mA | 0.2 mA | Table 18 |
| Wi-Fi 5 GHz TX, 11a 6 Mbps, 16 dBm | 250 mA | 240 mA | Table 19, p. 29 |
| Wi-Fi 5 GHz TX, 11ax HE80 MCS0, 14 dBm | 255 mA | 210 mA | Table 19, p. 29 |
| Wi-Fi 5 GHz RX, 80 MHz | 170 mA | 0.2 mA | Table 19 |
| Bluetooth BR TX (1DH5), 13 dBm | 323 mA | 0.2 mA | Table 20, p. 30 |
| Bluetooth LE 2M TX, 13 dBm | 345 mA | 0.2 mA | Table 20 |
| Bluetooth RX | 125 mA | 0.2 mA | Table 20 |
| 802.15.4 TX, 13 dBm | 390 mA | 0.2 mA | Table 21, p. 30 |
| Wi-Fi chip deep sleep (SD clock 25 MHz, off / on) | 0.6 / 0.7 mA | 0.05 mA | Table 22, p. 31 |
| Wi-Fi IEEE power save, 5 GHz, DTIM3 (25 MHz, clock off) | 1.1 mA | 0.05 mA | Table 22 |
| Bluetooth and 802.15.4 deep sleep | 0.25 mA | — | Table 23, p. 31 |
| Bluetooth LE advertising, 1.28 s interval | 0.32 mA | — | Table 24, p. 32 |
| Bluetooth LE scan, 1.28 s interval | 0.46 mA | — | Table 24 |
| Bluetooth ACL sniff, 1.28 s | 0.35 mA | — | Table 24 |

Sleep figures were measured on an NXP 8MMINILPD4-EVKB with firmware 18.99.1.p154.72 (§5.3). The item-tracking baseline of BOM line 103 (BLE advertising in suspend) corresponds to the 0.32 mA row, plus whatever the host keeps powered.

Peak current: on the EA carrier, "Peak current 1050 mA max … typically during the startup calibration", and both AVDD33 and the 1.8 V rail "can be above 1 Amp in peak" (EA M.2 PA4, pp. 8, 22). Module-level peak per rail: **UNVERIFIED** (datasheet).

## Pinout and package

Pin assignment, identical for Types 2EL, 2DL, 2LL and 2KL (pin-to-pin compatible family; E2B-54-1953 §3.2, Table 3):

| Pins | 2EL function |
|---|---|
| 1, 2, 9, 11, 14, 16, 17, 19–22, 28, 29, 32, 39, 41, 43, 53, 62, 67, 68, 71, 81–107 | GND |
| 3, 77–80 | NC |
| 4–8 | SPI_FRM, SPI_INT, SPI_RXD, SPI_TXD, SPI_CLK (802.15.4) |
| 10 | PDn |
| 12, 13 | AVDD33_1, AVDD33_2 |
| 15 | ANT0 |
| 18 | BT_15.4_IN |
| 23 | ANT1 |
| 24, 25, 26, 27 | RF_CNTL4, RF_CNTL3/CONFIG_XOSC_SEL, RF_CNTL1, RF_CNTL0 |
| 30, 31 | AVDD18_2, AVDD18_1 |
| 33–36, 65, 66 | Reserved |
| 37, 38 | RST_IND, IND_RST_15.4 |
| 40 | SD_VIO |
| 42, 44, 45–48 | SD_CMD, SD_CLK, SD_DAT[1], SD_DAT[3], SD_DAT[2], SD_DAT[0] |
| 49–52 | UART_TX, UART_CTS, UART_RX, UART_RTS |
| 54 | VIO |
| 55, 56 | CONFIG_HOST[0], CONFIG_HOST[1] |
| 57–61 | PCM_CLK, PCM_MCLK, PCM_DOUT, PCM_DIN, PCM_SYNC |
| 63, 64 | IND_RST_WL, IND_RST_BT |
| 69, 70 | WCI-2_SIN, WCI-2_SOUT (coexistence) |
| 72–76 | SD_INT, WL_WAKE_OUT, WL_WAKE_IN, BT15.4_WAKE_IN, BT15.4_WAKE_OUT |

There is no sleep-clock (32.768 kHz) input pin on the module (E2B-54-1953 Table 3); the block diagram shows only a 40 MHz reference inside the module (E2B-09-1413 Figure 1).

RF topology (E2B-09-1413 §2.2, Figures 1–2): ANT0 carries Wi-Fi 5 GHz and, through a diplexer and SPDT switch, Wi-Fi 2.4 GHz. In the **shared** configuration, Bluetooth and 802.15.4 also use ANT0; pin 18 must be tied to pin 23 externally through a 10 pF capacitor (E2B-54-1953 §4.3.3). In the **dedicated** configuration, ANT1 carries Bluetooth and 802.15.4 to its own antenna (Figure 2, Figure 10), and Linux must load `WlanCalData_ext_dANT.conf` (E2B-09-1413 §4.4, Table 10).

Package: 8.8 × 7.7 mm outline (footprint DXF, layer `ProductsBoradOutline`), 1.3 mm high (product brief).

## Recommended footprint

The footprint DXF (top view) holds 107 rectangular pads, all 0.55 × 0.25 mm (75 in one orientation, 32 rotated), on a 0.5 mm pitch, inside the 8.8 × 7.7 mm outline (parsed from the DXF, layer `NC_Work2`). Whether these are the module's terminals or the recommended PCB lands, and the solder-mask and stencil openings, are defined in the datasheet: **UNVERIFIED** (E2B-09-1413 §3.4 refers to the datasheet for dimensions and to the DXF).

Ground under the module, via rules under the LGA and a keep-out under the module body: not stated in E2B-09-1413 or E2B-54-1953; **UNVERIFIED** (datasheet).

## Application circuit and required passives

From the reference schematic for the u.FL configuration (E2B-09-1413 Figure 5, p. 10), with the note "Must copy Murata's reference circuitry and layout":

- Decoupling: 10 µF (GRM15) on AVDD33 (pins 12–13), on AVDD18 (pins 30–31) and on SD_VIO (pin 40). VIO (pin 54) decoupling is not drawn.
- SDIO: series damping resistors on SD_CLK, SD_CMD and SD_DAT0–3, value "according to the design on the user's board" (note *3). Internal SDIO pull-ups/pull-downs are 70–140 kΩ, 100 kΩ typical (E2B-09-1413 Table 2, p. 14).
- Straps: CONFIG_HOST[0] = 1 and CONFIG_HOST[1] = 1 select the default host interfaces (WLAN SDIO, Bluetooth UART, 802.15.4 SPI); every other combination is reserved (Figure 5, note *2).
- Unused GPIO[0…31] and RF_CNTL0, 1, 3, 4 may float (E2B-09-1413 §3.3).
- RF, shared antenna: ANT0 to the u.FL through the matching positions (0 Ω fitted, shunts DNP) and a 10 pF capacitor between pins 18 and 23 (Figure 5, Figure 9). Dedicated antenna: ANT1 to a second u.FL through its own matching positions; BT_15.4_IN is then terminated per Figure 10 (component values in the figure; **UNVERIFIED** as transcribed from a drawing). Matching parts are 0603-size in Murata's design ("Size: 0603 LQP03 / GRM03 / Resistor", Figures 9–10); the BOM's 0402 parts (line 58) differ from Murata's reference.

Power sequencing: not in the Murata documents read. On the EA carrier: supply rise (10–90 %) not faster than 40 µs nor slower than 100 ms, and PD_N held low for at least 1 ms after the supply is in specification (EA M.2 PA4 §3.1, p. 8). Module-level sequencing between AVDD33, AVDD18 and VIO: **UNVERIFIED** (datasheet).

### Antenna and RF layout rules for the Murata certification

- **FCC antennas** (CER-0248 Table 20, p. 26): Molex 146153 (3.2 / 4.25 dBi), Molex 219611 (2.67 / 3.67 dBi), Unictron WT32D1-KX (3.0 / 4.0 dBi), Inventek W24P-U (3.2 dBi, 2.4 GHz only), Murata Type2EL_Antenna trace antenna (3.6 / 4.6 dBi, ANT0 only). ISED lists the same set (Table 36, p. 53; 146153 "50 mm cable").
- **Molex 146187** (3.2 / 4.25 dBi, cable "50 mm or more") is only in "Additional Registered Antennas in Japan Radio Law certification" (E2B-09-1413 Table 4, p. 15; CER-0248 Table 56, p. 68). For the USA, Canada and EU, an unlisted antenna of equivalent type and lower gain needs a Class I permissive change approved by Murata (E2B-09-1413 §3.5.1, p. 14; CER-0248 p. 28: "the gain is the same or lower").
- **EU**: Murata provides conducted test reports only (EN 300 328, EN 301 893, EN 300 440, EN 62311); radiated data must be acquired on the final product, and the CE declaration is the product maker's (CER-0248 §2.3, p. 59).
- **RF exposure**: FCC and ISED approvals are for mobile equipment (antenna ≥ 20 cm from the body). Portable use needs SAR testing of the final product and a Class II (FCC) or Class 4 (ISED) permissive change through Murata, except Bluetooth-only use for FCC (CER-0248 §2.1.3.6, pp. 26–27; ISED p. 35).
- **Microstrip from pin 15 or 23 to the u.FL** (CER-0248 §2.1.6.2, pp. 31–33): 50 Ω over a solid layer-2 ground; FR4 dielectric 8–15 mil; width W = 1.8 × H; length longer than 7 mm, recommended 7–25 mm; never over a region without the same dielectric and ground.
- **Copy rules** (E2B-09-1413 §3.5.1, p. 15): copy the RF trace from Murata's u.FL layout file; trace width within ±0.25 mm; stack height between the GND layer and the RF trace 230–240 µm; passive locations as in Murata's design; keep the "keep out" area around the u.FL.
- **Under the u.FL**: "Do not place any conductors such as GND, signal traces, power lines from bottom of the connector as much as possible (Recommended for 800um or more)" (E2B-09-1413 Figure 13, p. 21).
- **Regulatory configuration in Linux**: Wi-Fi TX-power files `txpower_{US,CA,EU,JP}.bin`, `rutxpower_*.bin`, `ed_mac.bin` and the regulatory `db.txt`; Bluetooth TX-power scripts per region run at 3 Mbaud; 802.15.4 TX power via `ot-ctl` (E2B-09-1413 §4.1–4.3, pp. 23–25).

## Interfaces and timing

| Interface | Detail | Reference |
|---|---|---|
| Wi-Fi host | SDIO 3.0, 4-bit; "isometric zero delay routing with 50Ω impedance" | E2B-09-1413 §2.1, §3.2 |
| SDIO speed modes | Brief: "SDIO v3.0 DDR50". EA carrier: SDR12, SDR25, SDR50 (100 MHz), DDR50 (50 MHz). Murata sleep table lists a 200 MHz SD clock. Maximum mode **UNVERIFIED** (datasheet) | Product brief; EA M.2 PA4 p. 7; E2B-09-1413 Table 22 |
| Bluetooth host | 4-wire HCI UART; 4 Mbaud on the EA carrier; Murata's TX-power scripts assume 3,000,000 baud | E2B-09-1413 §2.1, §4.2; EA M.2 PA4 p. 7 |
| Bluetooth audio | PCM/I2S available (pins 57–61); the T1 uses HCI audio and leaves PCM unused | E2B-09-1413 §2.1; BOM v1 line 55, board ADR 0006 |
| 802.15.4 host | SPI (pins 4–8) | E2B-09-1413 §2.1 |
| Wake and reset | WL_WAKE_IN/OUT, BT15.4_WAKE_IN/OUT, SD_INT, IND_RST_WL/BT/15.4, PDn | E2B-54-1953 Table 3 |

The T1 connection (BOM v1 line 55): SDIO on `sdmmc1` at 1.8 V (VCCIO4), Bluetooth on UART1 M0 with RTS/CTS.

## Linux driver

Checked on 2026-10-24 against `torvalds/linux` (`v7.3`, released 2026-10-18, and `master`) and `linux-firmware` (GitLab `kernel-firmware/linux-firmware`).

- **Wi-Fi, mainline `nxpwifi`**: `drivers/net/wireless/nxp/nxpwifi`, added by commit `73b01e57ed3e` "wifi: nxp: add nxpwifi driver for IW61x" (authored 2026-06-05, committed 2026-07-15), present in v7.3 and absent from v7.2. Kconfig `NXPWIFI_SDIO` ("NXP WiFi Driver for IW61x", module `nxpwifi_sdio`); SDIO only; SDIO IDs 0x0471:0x0205 (IW61x) and 0x0471:0x0215 (IW610); suspend and resume hooks present. Firmware `nxp/sd_w61x_v1.bin.se`, added to linux-firmware on 2026-06-22. Fixes were still landing on 2026-10-14.
- **Wi-Fi, `mwifiex`**: no IW61x support in mainline; an IW61x patch to `mwifiex` was posted in March 2025 marked "do not merge".
- **Murata's regulatory files under `nxpwifi`**: the mainline driver loads `nxp/cal_data.conf` (main.c); no loader for Murata's per-country `txpower_*.bin` / `rutxpower_*.bin` was found in `main.c`, `init.c`, `sta_cmd.c` or `cfg80211.c`. Applying Murata's certified TX-power tables with the mainline driver is **UNVERIFIED**; they target NXP's out-of-tree `moal`/`mlan` driver (E2B-09-1413 §4.1 refers to Murata's Linux user guide).
- **Bluetooth, `btnxpuart`** (Kconfig `BT_NXPUART`): recognises IW612 by chip ID 0x7601 and loads `uartspi_n61x_v1.bin.se` (in linux-firmware since 2023-03-20). Devicetree binding `nxp,88w8987-bt.yaml` lists only `nxp,88w8987-bt` and `nxp,88w8997-bt`; the IW612 is identified at runtime. Optional properties include `max-speed` (3000000 or 4000000), `device-wakeup-gpios`, `reset-gpios`, `vcc-supply`, `firmware-name`.
- **802.15.4**: Murata configures it with `ot-ctl` (OpenThread); a mainline kernel driver for the IW612 802.15.4 radio was not searched for. The T1 does not wire the SPI (BOM v1 line 55).
- Packaging for Blackbird OS: BOM v1 line 55 plans DKMS for the 7.2 Debian kernel until 7.3 is used.

## Simulation models

None published by Murata among the documents read.

## Design notes for the T1

- Supply: provide AVDD18 as a power rail sized for at least 390 mA typical transmit plus the startup-calibration peak, and AVDD33 for about 240 mA typical transmit (tables above); the module-level peak is **UNVERIFIED** until the datasheet. VIO and SD_VIO at 1.8 V can share the AVDD18 source (as on the EA carrier), subject to noise and the datasheet.
- RF: the two U.FL connectors of BOM line 56 match the dedicated configuration (ANT0 Wi-Fi, ANT1 Bluetooth/802.15.4). The shared configuration needs only one U.FL plus the 10 pF link between pins 18 and 23. Keep the 10 pF position in the layout so either can be fitted.
- RF trace stack: Murata asks for 230–240 µm between the RF trace and its ground (E2B-09-1413) or 8–15 mil (CER-0248). The T1's HDI stackup uses about 50 µm dielectrics (constraints PCB-S-05), so the RF microstrip needs inner-layer cut-outs to reference a deeper ground, and the trace length must stay within 7–25 mm.
- Certification (BRD-025): pre-certification alone does not cover the T1. Handheld use triggers SAR testing and a permissive change; the Molex 146187 is outside the FCC/ISED lists and its 43.3 mm cable is shorter than the "50 mm or more" registered in Japan. Either pick a listed antenna (Molex 146153 or 219611) or plan the Class I permissive change with Murata. Note (2026-10-24): board ADR 0018 picks one Molex [146153-0050](../Molex/146153-0050.md) in the shared configuration; the "43.3 mm" of the 146187-0050 is most likely Molex's drawn bare cable of its 50 mm length class (see the [146187-0050](../Molex/146187-0050.md) note).
- Footprint and keep-out: take land, mask, stencil and any keep-out under the module from the datasheet once obtained (constraints PCB-R-01).
- Second sources: Murata Type 2DL (IW611, no 802.15.4) is pin-compatible (E2B-54-1953 §3.2). Pin compatibility with u-blox MAYA-W271-00B: **UNVERIFIED**.

## Sources

- Murata Type 2EL product page: <https://www.murata.com/en-us/products/connectivitymodule/wi-fi-bluetooth/overview/lineup/type2el>
- E2B-09-1413, E2B-54-1953, CER-0248, product brief, footprint and u.FL DXF files: URLs in `manifest.toml`
- Embedded Artists 2EL / 2DL M.2 Module Datasheet PA4 (LCSC mirror): URL in `manifest.toml`
- Linux: <https://github.com/torvalds/linux/tree/v7.3/drivers/net/wireless/nxp/nxpwifi>, <https://github.com/torvalds/linux/blob/v7.3/drivers/bluetooth/btnxpuart.c>, <https://github.com/torvalds/linux/blob/v7.3/Documentation/devicetree/bindings/net/bluetooth/nxp%2C88w8987-bt.yaml>, linux-firmware `nxp/` (<https://gitlab.com/kernel-firmware/linux-firmware/-/tree/main/nxp>), the `mwifiex` IW61x "do not merge" posting (<https://lkml.iu.edu/hypermail/linux/kernel/2503.3/06985.html>)
- Molex 146187-0050 drawing: [146187-0050](../Molex/146187-0050.md)
- OpenDAP board, `docs/specs/bom-v1.md`, lines 55–58, 103; `docs/specs/pcb-design-constraints.md` PCB-S-05, PCB-R-01
