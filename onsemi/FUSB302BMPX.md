# onsemi FUSB302BMPX

- **Function:** Programmable USB Type-C port controller with USB PD BMC physical layer (CC detection, Rp/Rd, VCONN switch, PD FIFOs over I2C)
- **T1 use:** board BOM v1 line 41 (Power), status Proposed
- **Datasheet:** FUSB302B Programmable USB Type-C Controller w/PD, FUSB302B/D Rev. 5 (August 2021), <https://www.onsemi.com/pdf/datasheet/fusb302b-d.pdf>
- **Package:** WQFN-14 (MLP) 2.5 × 2.5 mm, 0.5 mm pitch, exposed pad (onsemi case 510BR)

## Summary

The FUSB302B implements the analogue side of a USB Type-C port (attach, detach and orientation detection on CC1/CC2, host pull-up currents, device pull-down Rd, a VCONN switch with over-current limit) and the BMC physical layer of USB Power Delivery with 48-byte transmit and 80-byte receive FIFOs; the policy engine runs in host software over I2C (FUSB302B/D pp. 1, 6, 11). It supports source, sink and dual-role operation with autonomous DRP toggle and presents Rd when unpowered (dead-battery sink) (pp. 1, 11). In the T1 (board BOM v1 line 41) it is the Type-C/PD controller for the USB-C port: the T1 sinks power through PD (9 V requested, power tree §4.7) and sources 5 V in host mode, at Default current (Rp 80 µA) on battery. VDD comes from the always-on vcc3v3_pmu, I2C1 at 1.8 V, INT_N to GPIO0_C4 (BOM v1 line 41), driven by the Linux TCPM stack.

## Absolute maximum ratings

| Parameter | Min | Max | Unit | Source |
|---|---|---|---|---|
| VDD supply voltage | −0.5 | 6.0 | V | FUSB302B/D p. 13, Table 7 |
| CC pins (host, device or DRP) | −0.5 | 6.0 | V | p. 13, Table 7 |
| VBUS supply voltage | −0.5 | 28.0 | V | p. 13, Table 7 |
| Storage temperature | −65 | +150 | °C | p. 13, Table 7 |
| Junction temperature | — | +150 | °C | p. 13, Table 7 |
| Lead temperature (soldering, 10 s) | — | +260 | °C | p. 13, Table 7 |
| ESD, HBM (JS-001-2012) | 4 | — | kV | p. 13, Table 7 |
| ESD, CDM (JESD22-C101) | 1 | — | kV | p. 13, Table 7 |

## Recommended operating conditions

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| VBUS supply voltage | 4.0 | 5.0 | 21.0 | V | p. 13, Table 8 |
| VDD supply voltage (functional) | 2.7 | 3.3 | 5.5 | V | p. 13, Table 8 |
| VDD for all electrical specifications | 3.0 | — | — | V | p. 13, Table 8 note 3 |
| VCONN supply voltage | 2.7 | — | 5.5 | V | p. 13, Table 8 |
| VCONN supply current | — | — | 560 | mA | p. 13, Table 8 |
| Operating temperature (FUSB302BMPX) | −40 | — | +85 | °C | p. 13, Table 8; p. 2, Table 1 |
| I2C pull-up voltage | 1.71 | — | VDD | V | p. 17, Table 13 note 6; p. 30, Table 43 |

Selected characteristics (TA −40 to +85 °C):

| Parameter | Min | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| VCONN switch on-resistance (VCONN to CC1/CC2) | — | 0.4 | 1.2 | Ω | p. 15, Table 10 |
| VCONN OCP limit (OCPreg = 0Fh) | 600 | 800 | 1000 | mA | p. 15, Table 10 |
| Source CC current, Default (HOST_CUR = 01) | 64 | 80 | 96 | µA | p. 15, Table 10 |
| Source CC current, 1.5 A (HOST_CUR = 10) | 166 | 180 | 194 | µA | p. 15, Table 10 |
| Source CC current, 3 A (HOST_CUR = 11) | 304 | 330 | 356 | µA | p. 15, Table 10 |
| Device pull-down Rd (powered) | 4.6 | 5.1 | 5.6 | kΩ | p. 15, Table 10 |
| Sink pull-down voltage in dead battery | — | — | 2.18 | V | p. 15, Table 10 |
| VBUS threshold for I_VBUSOK | — | — | 4.0 | V | p. 15, Table 10 |
| Measure DAC step, CC / VBUS | — | 42 / 420 | — | mV | p. 15, Table 10 |
| VCONN switch thermal shutdown | — | 145 | — | °C | p. 15, Table 10 |

## Power by mode

| Mode | Conditions | Typ | Max | Unit | Source |
|---|---|---|---|---|---|
| Disabled | VDD 3.0–5.5 V, nothing attached, no I2C traffic | 0.37 | 5.0 | µA | p. 16, Table 11 |
| Unattached, DRP toggle (standby) | TOGGLE = 1, PWR = 1h, WAKE_EN = 0, TOG_SAVE_PWR = 01 | 25 | 40 | µA | p. 16, Table 11 |
| Attached, BMC PD standby | PD active, not sending or receiving, PWR = 7h | 40 | — | µA | p. 16, Table 11 |

The PWR register (0Bh) enables the bandgap/wake circuit, receiver and current references, measure block and internal oscillator separately (p. 23, Table 27); reset value 01h. Unpowered, the device presents Rd so a source can supply VBUS (p. 11).

## Pinout and package

FUSB302BMPX, top view (p. 5, Figure 5; Table 3):

| Pin | Name | Type | Function |
|---|---|---|---|
| 1 | CC2 | I/O | Type-C configuration channel 2 |
| 2 | VBUS | Input | VBUS sense for attach/detach as a sink; expected to be an OVP-protected input |
| 3 | VDD | Power | Supply input |
| 4 | VDD | Power | Supply input |
| 5 | INT_N | Open-drain output | Active-low interrupt |
| 6 | SCL | Input | I2C clock |
| 7 | SDA | Open-drain I/O | I2C data |
| 8 | GND | Ground | Ground |
| 9 | GND | Ground | Ground |
| 10 | CC1 | I/O | Type-C configuration channel 1 |
| 11 | CC1 | I/O | Type-C configuration channel 1 |
| 12 | VCONN | Power switch | VCONN input, switched to the unused CC pin |
| 13 | VCONN | Power switch | VCONN input |
| 14 | CC2 | I/O | Type-C configuration channel 2 |
| EP | — | — | Connect to GND for thermal |

Ordering (p. 2, Table 1): FUSB302BMPX, top mark UA, 14-lead MLP 2.5 × 2.5 mm 0.5 mm pitch, −40 to 85 °C, 3,000 per reel. Variants 01/10/11 differ only in I2C address; FUSB302BVMPX is the −40 to 105 °C automotive part. Case 510BR (p. 31): body 2.50 ± 0.05 mm square, 0.75 ± 0.05 mm height, exposed pad 1.45 ± 0.05 mm square, leads 0.24 ± 0.06 mm wide, 0.5 mm pitch, no JEDEC registration (drawing 98AON13629G).

## Recommended footprint / land pattern

Recommended land pattern (p. 31, case 510BR, 98AON13629G): pad-row outer extent 2.43 × 2.43 mm, centre thermal pad 1.45 × 1.45 mm, signal pads 0.30 mm wide on 0.50 mm pitch, pad length 0.58 mm (reference). Note D on the drawing: "land pattern recommendation is existing industry land pattern". Solder-mask and stencil openings are not given (**UNVERIFIED**).

## Application circuit and required passives

Reference schematic Figure 18 and Table 43 (p. 30):

| Position | Min | Typ | Max | Unit | Note |
|---|---|---|---|---|---|
| CRECV, CC1/CC2 receiver capacitance | 200 | — | 600 | pF | one per CC line, to GND |
| CBULK, VCONN source bulk | 10 | — | 220 | µF | only when VCONN is sourced |
| CVCONN, VCONN decoupling | — | 0.1 | — | µF | |
| CVDD1, VDD decoupling | — | 0.1 | — | µF | |
| CVDD2, VDD decoupling | — | 1.0 | — | µF | |
| RPU, I2C pull-ups | — | 4.7 | — | kΩ | |
| RPU_INT, INT_N pull-up | 1.0 | 4.7 | — | kΩ | |
| VPU, I2C pull-up voltage | 1.71 | — | VDD | V | |

The typical application (p. 3, Figure 2) places an OVP device between connector VBUS and the charger and shows the FUSB302B VBUS pin on the connector side. The device does not integrate BC1.2 detection (p. 11).

## Interfaces and timing

- **I2C address:** FUSB302BMPX, FUSB302BUCX and FUSB302BVMPX use 7-bit **0x22** (0100010); FUSB302B01MPX 0x23, FUSB302B10MPX 0x24, FUSB302B11MPX 0x25 (p. 18, Table 15). The Device ID register (01h) product-ID bits identify the variant (p. 19, Table 17).
- **I2C levels** (VDD 3.0–5.5 V): VIL 0.51 V max, VIH 1.32 V min, hysteresis 94 mV min, VOL 0.35 V max at 2 mA (pp. 16–17, Table 13). Pull-up voltage 1.71 V to VDD (Table 13 note 6). A 1.8 V bus with VDD = 3.3 V is within specification.
- **I2C speed:** Fast-mode Plus, fSCL 0–1000 kHz, bus capacitance up to 550 pF (p. 17, Table 14). The text notes that in low-power TOGGLE operation the slow internal clocking may not be fully compliant with 1 MHz operation (p. 12).
- **INT_N:** open drain, VOL 0.4 V max at 4 mA; ≥ 50 µs from global interrupt mask clear to INT_N low (p. 16, Table 13).
- **DRP toggle timing:** tTOG1 (sink) 30–60 ms, tTOG2 (source) 20–40 ms, optional disable time 0/40/80/160 ms between cycles (p. 15, Table 10).
- **PD timing:** tReceive 0.9–1.1 ms, tRetry ≤ 75 µs, tTransmit (GoodCRC) ≤ 195 µs, tSoftReset and tHardReset ≤ 5 ms (p. 16, Table 12). AUTO_CRC sends GoodCRC in hardware (p. 11; Switches1, p. 20).
- **BMC transmitter:** VOH 1.05–1.20 V, unit interval 3.03–3.70 µs (p. 14, Table 9).

## Linux driver

- Mainline driver `drivers/usb/typec/tcpm/fusb302.c`, Kconfig `CONFIG_TYPEC_FUSB302`, on top of the TCPM framework (`CONFIG_TYPEC_TCPM`); BOM v1 line 41 records it as "mainline + Debian".
- Compatible `fcs,fusb302`; the driver does not carry a separate FUSB302B compatible (**UNVERIFIED** against the current source). Mainline RK3399 boards with an FUSB302 use the same binding (**UNVERIFIED** which use the B variant).
- DT (binding `Documentation/devicetree/bindings/usb/fcs,fusb302.yaml`, **UNVERIFIED** against the current tree): `reg = <0x22>`, `interrupts` (INT_N, level low), `vbus-supply` (the regulator that switches the T1's source VBUS, here the TPS61088 + eFuse #C path behind `USB_SRC_ON`), and a `connector` child node with `compatible = "usb-c-connector"`, `power-role = "dual"`, `data-role`, `try-power-role`, `source-pdos`, `sink-pdos` and `op-sink-microwatt` (usb-connector binding).
- The TCPM charger link (setting BQ25895 IINLIM after negotiation) goes through the power-supply framework; the exact wiring for this board is **UNVERIFIED**.

## Simulation models available

None listed in `manifest.toml` for this part. IBIS or other onsemi models are **UNVERIFIED**: not checked in this session.

## Design notes for the T1

- **Address and 1.8 V I2C confirmed.** FUSB302BMPX is at 0x22 (p. 18); VIH 1.32 V min and a pull-up range from 1.71 V to VDD (pp. 16–17) allow the 1.8 V I2C1 bus with VDD = 3.3 V. This closes the BOM v1 line 41 **UNVERIFIED** note. Order the plain BMPX: the 01/10/11 variants change the address.
- **VDD at 3.3 V** (vcc3v3_pmu) meets the 3.0 V minimum for full electrical specification (p. 13, note 3).
- **Dead battery.** With the cell empty, vcc3v3_pmu (RK809 LDO6) is down and the FUSB302B is unpowered; it then presents Rd (≤ 2.18 V on CC, p. 15), so a Type-C source supplies 5 V and the BQ25895 can start charging. No extra dead-battery circuit is needed (p. 11).
- **VBUS pin:** absolute maximum 28 V, operating 4–21 V (p. 13); the datasheet expects an OVP-protected input (p. 5). On the T1 the pin senses connector VBUS behind the TVS2200; the 9 V PD contract stays well inside the range.
- **Source current on battery:** HOST_CUR = 01 advertises Default USB power (80 µA Rp, p. 21, Table 22), matching the 0.5 A battery budget (power tree §4.6).
- **CC capacitors:** fit 200–600 pF CRECV on each CC line (p. 30). Check that the CC ESD part (BOM v1 protection section) does not add capacitance beyond this window.
- **VCONN:** the T1's port is not expected to power e-marked cables or accessories (**UNVERIFIED**, a board decision). If VCONN is not sourced, CBULK is not needed; how to terminate unused VCONN pins is not stated in the datasheet (**UNVERIFIED**).
- **No BC1.2:** the FUSB302B does not detect BC1.2 chargers (p. 11); BC1.2 detection, if used, is the BQ25895's D+/D− function, which BOM v1 turns off.
- **Interrupt pull-up:** 1.0–4.7 kΩ to the 1.8 V host rail (p. 30).

## Sources

- onsemi FUSB302B datasheet FUSB302B/D Rev. 5 (August 2021), <https://www.onsemi.com/pdf/datasheet/fusb302b-d.pdf>, fetched 2026-10-22, sha256 `bdea0857f98f931f42d2522359e9df8a2b83da9e5525efe076cd2091d32ff66a` (not yet in manifest.toml). Page numbers are PDF page numbers (33 pages; pp. 31–33 are the mechanical case outlines).
- Board BOM v1 line 41 and power tree v0 §2, §4.6, §4.7 (`public/board/docs/specs/`).
- Linux driver notes from general knowledge of the mainline tree; not re-read in this session (marked **UNVERIFIED** where it matters).
