# Third-party notices

This repository and its release files contain work by OpenSourceSDRLab together with third-party software. The Apache License 2.0 in [LICENSE](LICENSE) applies **only** to the files created by OpenSourceSDRLab:

- `docs/`, `hardware/`, `images/`, `README.md`
- in each `vivado/<carrier>/` folder:
  - `FMC_ADRV9009_PL/FMC_ADRV9009_PL.srcs/sources_1/new/axi_lite_drv.v`
  - `FMC_ADRV9009_PL/FMC_ADRV9009_PL.srcs/sources_1/new/jesd204_transport_layer.v`
  - `FMC_ADRV9009_PL/FMC_ADRV9009_PL.srcs/sources_1/new/jesd204b_adc_dac_top.v`
  - `FMC_ADRV9009_PL/FMC_ADRV9009_PL.srcs/constrs_1/new/IO_planning.xdc`
  - `FMC_ADRV9009_PL/FMC_ADRV9009_PL.srcs/sim_1/imports/new/tb_jesd204b_adc_dac_top.v`
  - `FMC_ADRV9009_PS/src/app/rf_config.c`, `rf_config.h`
  - `FMC_ADRV9009_PS/src/devices/adi_hal/`: `change_rfpll.*`, `common.h`, `io_control.h`, `spi_ctrl.*`

All other files keep their original copyright notices and licences, which have not been changed:

| Component | Files | Owner | Licence |
|---|---|---|---|
| ADRV9009 (Talise) API and ADI HAL | `FMC_ADRV9009_PS/src/devices/talise/` and the files in `devices/adi_hal/` that carry an Analog Devices copyright header | Analog Devices, Inc. | ADI Source Code Software License Agreement, see `LICENSE.txt` in `devices/talise/` and `devices/adi_hal/` |
| Talise application and configuration | `FMC_ADRV9009_PS/src/app/headless.c`, `talise_config.c`, `talise_config.h` | Analog Devices, Inc. | as stated in each file header |
| Talise ARM and stream firmware (object code inside the prebuilt application `.elf` in Releases) | Releases only | Analog Devices, Inc. | AD937X Software License Agreement (20180301-AD937X-CTSLA) |
| ADI HDL modules | `FMC_ADRV9009_PL/.../sources_1/new/ad_iobuf.v`, `up_axi.v` | Analog Devices, Inc. | as stated in each file header |
| Xilinx/AMD IP cores, block design and generated files | `FMC_ADRV9009_PL/` (`.xci`, `.xcix`, `.bd` and generated files), and the Xilinx parts of the prebuilt `.bit`, `.xsa` and `fsbl.elf` in Releases | Xilinx, Inc. / AMD | Xilinx/AMD licence terms |
| SD evaluation image and evaluation boot files | Releases | Analog Devices, Inc. | Analog Devices licence terms |

Files and software that are **not** included and must be obtained from Analog Devices:

- the Talise firmware headers `talise_arm_binary.h` and `talise_stream_binary.h` (version 6.0.2), needed to build the application from source. Their licence only allows distribution as object code inside a product. Download instructions and checksums: `vivado/<carrier>/FMC_ADRV9009_PS/src/firmware/README.md`;
- the ADRV9009 Transceiver Evaluation Software: <https://www.analog.com/en/products/adrv9009.html>.

"Analog Devices", "ADRV9009", "Xilinx", "Zynq" and "Vivado" are trademarks of their respective owners. They are used here only to describe compatibility and do not imply endorsement.
