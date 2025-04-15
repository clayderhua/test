AIM-Linux Developer Center
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
