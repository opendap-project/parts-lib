# LBES5PL2EL-923

- **Manufacturer:** Murata
- **Function:** Murata Type 2EL, pre-certified Wi-Fi 6 + Bluetooth 5.4 module, NXP IW612 (BOM v1 line 55)
- **BOM v1 lines:** 55 (module), 56 (U.FL antenna connectors), 57 (antennas), 58 (matching networks), 103 (item tracking baseline)
- **Package:** LGA module; dimensions, pad count and pinout **UNVERIFIED**
- **Datasheet:** Not in the cache; revision and sha256 unknown
- **Status:** Datasheet not downloaded: every field UNVERIFIED. The manifest URL (Murata product page, now redirecting to `pim.murata.com`) returned no datasheet in this session; Murata's module datasheets were not reachable without an account. Every value below comes from the BOM or is marked **UNVERIFIED**.

## Summary

Murata Type 2EL is a pre-certified wireless module built on the NXP IW612 (BOM v1 line 55). In the T1 it provides Wi-Fi 6 over SDIO 3.0 on the SoC's `sdmmc1` (VCCIO4, 1.8 V) and Bluetooth over UART1 M0 with RTS/CTS. Bluetooth audio runs over HCI (board ADR 0006). The BOM's VBAT supply is RK809 SWOUT1 at 3.3 V (supply range **UNVERIFIED**) and VIO is 1.8 V. The BOM also names IW612 BLE advertising in suspend as the baseline for item tracking (line 103), with feasibility and current draw **UNVERIFIED**.

## Absolute maximum ratings

**UNVERIFIED** (no datasheet).

## Recommended operating conditions

| Parameter | Value | Status |
|---|---|---|
| VBAT supply | 3.3 V from RK809 SWOUT1 | BOM v1 line 55; module range **UNVERIFIED** |
| VIO | 1.8 V (VCCIO4) | BOM v1 line 55; module range **UNVERIFIED** |
| Operating temperature | — | **UNVERIFIED** |

## Power by mode

**UNVERIFIED** (no datasheet): Wi-Fi TX/RX, power save, BT/BLE advertising and deep sleep currents are all unknown. The suspend-mode BLE draw the BOM line 103 baseline needs is among them.

## Pinout and package

**UNVERIFIED.** The number of RF pins (one shared or separate Wi-Fi/BT antenna ports) is not confirmed. BOM line 56 provisions two U.FL connectors, "one per module antenna pin".

## Recommended footprint

**UNVERIFIED.** Take it only from Murata's datasheet or hardware design guide for Type 2EL. Keep-out and ground requirements under the module are unknown.

## Application circuit and required passives

From the BOM only:

- RF: per antenna, a U.FL-R-SMT-1(10) connector (line 56), a Molex 146187-0050 FPC antenna (line 57) and a 3-element π matching network in 0402 C0G parts, DNP by default and tuned on the final enclosure (line 58).
- Decoupling, reset/power-down control, sleep clock and strap pins: **UNVERIFIED**.

## Interfaces and timing

| Interface | Connection in the T1 | Status |
|---|---|---|
| Wi-Fi host | SDIO 3.0 on `sdmmc1`, 1.8 V (VCCIO4) | BOM v1 line 55, §4.2 |
| Bluetooth host | UART1 M0 with RTS/CTS, 1.8 V | BOM v1 line 55 |
| Bluetooth audio | HCI (no PCM/I2S path) | BOM v1 line 55, board ADR 0006 |
| Sleep clock, wake lines | — | **UNVERIFIED** |

SDIO bus speed modes and UART baud rates supported by the module: **UNVERIFIED**.

## Linux driver

- Wi-Fi: NXP `nxpwifi` driver. Per BOM v1 line 55 it arrives in mainline with 7.3 and is built as DKMS for the 7.2 Debian kernel. Exact kernel version and firmware file names **UNVERIFIED** here.
- Bluetooth: mainline `btnxpuart` (Kconfig `BT_NXPUART`), not set in Debian's trixie-backports 7.2 config, so DKMS (BOM v1 §3). Devicetree compatible for IW612 under `btnxpuart` **UNVERIFIED**.
- Firmware: NXP firmware blobs for IW612 (`linux-firmware` packaging **UNVERIFIED**).

## Simulation models

None listed in `manifest.toml`.

## Design notes for the T1

- Get the Murata Type 2EL datasheet and hardware design guide before layout. Supply ranges, the RF pin count, footprint, keep-out and power-sequencing rules are all open.
- Keeping the pre-certification depends on following Murata's reference RF design and antenna list. Whether the Molex 146187 antenna is on the module's certified antenna list is **UNVERIFIED**.
- Antenna placement depends on the case material (metal or polymer) (BOM v1 line 57).
- BOM v1 lists stock as Digi-Key 938, Mouser 2,820, LCSC 0 (2026-10-21/22). Second source: u-blox MAYA-W271-00B with the same chip (line 55), pin compatibility **UNVERIFIED**.

## Sources

- OpenDAP board, `docs/specs/bom-v1.md`, lines 55–58, 103, §3, §4.2
- Manifest URL: <https://www.murata.com/en-us/products/productdetail?partno=LBES5PL2EL-923> (no datasheet retrieved)
