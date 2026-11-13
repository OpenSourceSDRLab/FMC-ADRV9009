---
title: FMC-ADRV9009 Quick Start Guide
product: FMC-ADRV9009
doc_id: OSSDRLAB-FMC-ADRV9009-QSG
version: 1.0
date: 2026-11-12
repo: https://github.com/OpenSourceSDRLab/FMC-ADRV9009
---

<!-- ossl:header -->
<p><a href="https://www.opensourcesdrlab.com"><img src="../images/OpenSourceSDRLab-banner.jpg" alt="OpenSourceSDRLab" width="100%"></a></p>

# FMC-ADRV9009 Quick Start Guide

| Product | Document | Version | Date |
|---|---|---|---|
| FMC-ADRV9009 | OSSDRLAB-FMC-ADRV9009-QSG | 1.0 | 2026-11-12 |
<!-- /ossl:header -->

## 1. Overview

The FMC-ADRV9009 is an FPGA Mezzanine Card (FMC, HPC connector) built around the Analog Devices ADRV9009 RF transceiver and the AD9528 clock generator. It brings the transceiver's two transmit, two receive and two observation-receive channels out to SMA connectors and connects to the carrier FPGA through JESD204B.

This guide shows how to bring the board up on a Xilinx ZC706 carrier with the ADRV9009 Transceiver Evaluation Software, and where to find the bare-metal reference designs in this repository.

## 2. What you need

| Item | Notes |
|---|---|
| FMC-ADRV9009 board | |
| Carrier board | Xilinx ZC706 (used in this guide), or the XC7Z100 "7100" carrier |
| microSD card | 16 GB or larger |
| Ethernet cable and USB-UART cable | for the ZC706 network and serial console |
| Windows PC | runs the evaluation software and the SD-card writer |
| SD evaluation image | `ADRV9009-eval-SD-image-20161130.img.xz` from the [Releases](../../../releases) page |
| Boot files and test configuration | `FMC-ADRV9009_eval-boot-files.zip` from the [Releases](../../../releases) page |
| ADRV9009 Transceiver Evaluation Software | download from Analog Devices: <https://www.analog.com/en/products/adrv9009.html> |
| SD-card writing tool | any image writer, for example Win32 Disk Imager or balenaEtcher |

## 3. Board connectors

| Connector | Function |
|---|---|
| TX1, TX2 | transmit outputs |
| RX1, RX2 | receive inputs |
| ORX1, ORX2 | observation-receiver inputs |
| REF_IN | external reference clock input |
| EXT_LO | external local-oscillator input |
| FMC (HPC) | JESD204B data, SPI control and power from the carrier |

See `hardware/FMC-ADRV9009_Schematic.pdf` for the full schematic.

## 4. Bring-up with the evaluation software (ZC706)

1. Decompress `ADRV9009-eval-SD-image-20161130.img.xz` (for example with 7-Zip) and write the `.img` file to the microSD card with your SD-card writer.

2. When writing has finished, open the card's **BOOT** partition and copy every file from the `zc706_update` folder of `FMC-ADRV9009_eval-boot-files.zip` into it, replacing the existing files.

3. Insert the card into the ZC706 and set the boot-mode switches to **SD card boot**.

4. Fit the FMC-ADRV9009 on the ZC706 **HPC** FMC connector, connect the Ethernet cable and the USB-UART cable, then power on.

5. On the serial console, give the board an IP address:

        ifconfig eth0 192.168.1.10

    Set your PC to an address in the same subnet, for example `192.168.1.100`.

6. Start the ADRV9009 Transceiver Evaluation Software, connect to `192.168.1.10`, and update the firmware when the software asks you to.

7. Load the test configuration `ADRV9009_Test_MAX.xml` (included in `FMC-ADRV9009_eval-boot-files.zip`).

8. Set the transmit waveform and check the received waveform.

> **Tip:** if the received spectrum shows many spurious signals, reduce the receiver gain.

## 5. Reference designs in this repository

| Folder | Carrier | Contents |
|---|---|---|
| `vivado/ZC706/` | Xilinx ZC706 (XC7Z045) | Vivado 2021.1 project (PL) and bare-metal application source (PS) |
| `vivado/7100/` | XC7Z100 "7100" carrier | Vivado 2021.1 project (PL) and bare-metal application source (PS) |

The repository holds the project sources. Prebuilt files for each carrier (bitstream, hardware platform `.xsa`, FSBL and application `.elf`) are attached to the [Releases](../../../releases) page.

To rebuild from source:

1. Open `FMC_ADRV9009_PL/FMC_ADRV9009_PL.xpr` in Vivado 2021.1, generate the bitstream and export the hardware (`.xsa`).

2. Download the two Talise firmware headers from Analog Devices into `FMC_ADRV9009_PS/src/firmware/`. They are not part of this repository; `src/firmware/README.md` gives the links (ADI no-OS, branch `2021_R1`, firmware 6.0.2) and the SHA-256 values to check.

3. In Vitis 2021.1, create a platform from the `.xsa` (standalone, `ps7_cortexa9_0`), then an empty bare-metal C application, and import everything in `FMC_ADRV9009_PS/src` (including `lscript.ld`).

4. In the application's C/C++ build settings, add these include directories (ARM v7 gcc compiler > Directories):

        src/app
        src/devices
        src/devices/adi_hal
        src/devices/talise
        src/firmware

    The linker libraries are the Vitis defaults (`-Wl,--start-group,-lxil,-lgcc,-lc,--end-group`).

5. Build the application, then program the bitstream and run the `.elf` over JTAG, or create `BOOT.bin` with the FSBL, bitstream and application to boot from the SD card.

## 6. Support

- Product page: <https://opensourcesdrlab.com/products/opensourcesdrlab-new-fmc-adrv9009-board-high-performance-board>
- Email: support@opensourcesdrlab.com
- Forum: <https://forum.opensourcesdrlab.com>
- Discord: <https://discord.gg/nnxY6DkmvT>

<!-- ossl:footer -->
---
<sub>© 2026 OpenSourceSDRLab. All rights reserved. · <a href="https://www.opensourcesdrlab.com">www.opensourcesdrlab.com</a></sub>
<!-- /ossl:footer -->
