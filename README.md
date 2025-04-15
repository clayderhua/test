AIM-Linux Developer Center


# Introduction

How to compile Yocto 5.1 on the new Advantech NXP BSP?

Based on NXP Yocto 5.1-6.12.3 version + Advantech Meta Layer

## Step 1: Initialize Yocto Environment

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "Your Email"
$ git config --list

$ mkdir imx-yocto-bsp
$ cd imx-yocto-bsp
$ repo init -u https://github.com/nxp-imx/imx-manifest -b imx-linux-styhead -m imx-6.12.3-1.0.0.xml
$ repo sync
```

Check sources folders:

```
sources/
├── base
├── meta-arm
├── meta-browser
├── meta-clang
├── meta-freescale
├── meta-freescale-3rdparty
├── meta-freescale-distro
├── meta-imx
├── meta-nxp-connectivity
├── meta-nxp-demo-experience
├── meta-openembedded
├── meta-qt6
├── meta-security
├── meta-timesys
├── meta-virtualization
└── poky
```

## Step 2: Get Advantech Meta Layer

```bash
$ cd sources
$ git clone https://AIM-Linux@dev.azure.com/AIM-Linux/meta-advantech-nxp/_git/meta-advantech-nxp -b styhead-6.12.3-next
$ mv meta-advantech-nxp meta-advantech
```

Updated sources folder:

```
sources/
├── base
├── meta-advantech
├── meta-arm
├── meta-browser
├── meta-clang
├── meta-freescale
├── meta-freescale-3rdparty
├── meta-freescale-distro
├── meta-imx
├── meta-nxp-connectivity
├── meta-nxp-demo-experience
├── meta-openembedded
├── meta-qt6
├── meta-security
├── meta-timesys
├── meta-virtualization
└── poky
```

## Step 3: Compile Yocto

Example for XWayland and imx8mprsb3720a2 board:

```bash
$ MACHINE=imx8mprsb3720a2 DISTRO=fsl-imx-xwayland source ./imx-setup-release.sh -b rsb3720
```

### Enabling the Advantech BSP Layer

To enable the layer, add the following line to the end of `conf/bblayers.conf`:

```bash
BBLAYERS += "${BSPDIR}/sources/meta-advantech"
```

Then start the build:

```bash
$ bitbake imx-image-core
```

---

## The Advantech Meta Layer Tree Structure

```
meta-advantech/
├── conf
│   ├── layer.conf
│   └── machine
│       └── imx8mprsb3720a2.conf
├── recipes-bsp
│   └── u-boot
│       ├── u-boot-imx
│       │   ├── board
│       │   │   ├── 0001-change-debug-port-uart3.patch
│       │   │   ├── 0001-support_eth0_eth1_MAC_address_from_spi.patch
│       │   │   ├── change_debug_port_uart3.inc
│       │   │   └── support_ethernet_MAC_address.inc
│       │   ├── drivers
│       │   │   └── spi
│       │   │       ├── 0001-spi_controller_not_support_advanced_features.patch
│       │   │       └── spi_controller_not_support_advanced_features.inc
│       │   └── imx8mprsb3720a2
│       │       ├── imx8mp-rsb3720-a2.dts
│       │       ├── imx8mprsb3720a2.inc
│       │       ├── imx8mp-rsb3720-a2-u-boot.dtsi
│       │       └── lpddr4_timing_rsb3720a2_6G.c
│       └── u-boot-imx_2024.04.bbappend
├── recipes-kernel
│   └── linux
│       ├── linux-imx
│       │   ├── drivers
│       │   │   ├── 0001-ewm-c109f601e_3g_module.patch
│       │   │   ├── ewm-c109f601e_3g_module.inc
│       │   │   ├── watchdog_advantech.c
│       │   │   └── watchdog_advantech.inc
│       │   ├── imx8mprsb3720a2
│       │   │   ├── imx8mp-rsb3720-a2.dts
│       │   │   ├── imx8mprsb3720a2.inc
│       │   │   └── rtc-support.cfg
│       │   ├── rom2620-ed91
│       │   │   ├── lt9211-driver-fixup.patch
│       │   │   ├── lvds-support.cfg
│       │   │   ├── rom2620-ed91.dts
│       │   │   └── rom2620-ed91.inc
│       │   ├── rom2820-ed93
│       │   │   ├── rom2820-ed93.dts
│       │   │   └── rom2820-ed93.inc
│       │   └── rom5722-db2510
│       │       ├── rom5722-db2510.dts
│       │       ├── rom5722-db2510.inc
│       │       └── rtc-support.cfg
│       └── linux-imx_6.%.bbappend
```



## RSB-3720 測試狀態表  
✅ pass ｜ ❌ fail ｜ ⚠️ Not Tested

| Device    | Status | Comment                                           |
|-----------|--------|---------------------------------------------------|
| SDHC2     | ✅     | eMMC                                              |
| SDHC1     | ✅     | SD Card                                           |
| ETH0      | ✅     | Link pass 1Gbps                                   |
| ETH0 Mac  | ✅     | Mac address                                       |
| ETH1      | ✅     | Link pass 1Gbps                                   |
| ETH1 Mac  | ✅     | Mac address                                       |
| USB1-1    | ✅     | USB 3.2                                           |
| USB1-2    | ✅     | USB 2.0                                           |
| HDMI      | ✅     |                                                   |
| MIPI-DSI  | ❌     |                                                   |
| MIPI-CSI  | ❌     |                                                   |
| UART1     | ❌     | COM2, M2(2/4-wire) not tested                     |
| UART2     | ❌     | COM3, UIO expansion (2-wire)                      |
| UART3     | ❌     | COM1, console (not tested)                        |
| UART4     | ❌     | COM4, UIO expansion (2-wire)                      |
| LPI2C0    | ✅     | PMIC(0x25) WDT(0x29) TPM(0X2e)                     |
| LPI2C1    | ⚠️     | Not tested - Camera1 0x3c                         |
| LPI2C2    | ⚠️     | Not tested - Camera2 0x3c                         |
| LPI2C3    | ✅     | EEPROM 0X50 on UIO40xx                            |
| LPI2C6    | ⚠️     | Not tested                                        |
| NPU       | ⚠️     | Not tested                                        |
| PWM 2     | ⚠️     | Not tested                                        |
| PWM 3     | ⚠️     | Not tested                                        |
| GPIO      | ⚠️     | Not tested                                        |
| PCI-E     | ⚠️     | Not tested                                        |
| CAN0      | ⚠️     | Not tested                                        |
| CAN1      | ⚠️     | Not tested                                        |
| RTC0      | ✅     | External I2C RTC (S35390)                         |
| RTC1      | ✅     | Internal RTC, supports timer wake events          |
| Watchdog0 | ✅     | Internal watchdog                                 |
| Watchdog1 | ✅     | External I2C Advantech watchdog (MSP430-based)    |
| 3G        | ⚠️     | Not tested                                        |
| WIFI      | ⚠️     | Not tested                                        |
| M.2       | ⚠️     | Not tested                                        |
| ETH2      | ✅     | UIO 4032 1Gbps                                    |
| ETH2 Mac  | ✅     | UIO 4032 Mac address                              |
| USB1-1    | ✅     | USB 3.2                                           |
| USB1-2    | ✅     | USB 2.0                                           |




The one-stop resource hub for Advantech Arm-based embedded computing and IoT solutions.

To simplify development and deployment to our customers, Advantech provides the comprehensive developer resources and documentations with stable long term support for mainstream distributions.

https://ess-wiki.advantech.com.tw/view/RISC

![nxp](https://github.com/clayderhua/test/blob/main/nxp.png)

|  NXP i.mx                   |  Repository                                                                    |
|:----------------------------|:-------------------------------------------------------------------------------|
|  u-boot                     |  [uboot-imx](https://github.com/ADVANTECH-Corp/uboot-imx)                      |
|  Linux kernel               |  [linux-imx](https://github.com/ADVANTECH-Corp/linux-imx)                      |
|  Yocto source download      |  [adv-arm-yocto-bsp](https://github.com/ADVANTECH-Corp/adv-arm-yocto-bsp)      |
|  Yocto Advantech meta layer |  [meta-advantech2](https://github.com/ADVANTECH-Corp/meta-advantech2)          |
