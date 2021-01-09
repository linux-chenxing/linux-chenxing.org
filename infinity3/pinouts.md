# Infinity3 pinouts

https://github.com/fifteenhex/linux-ssc325/blob/93240ba80ed1eff069eaca968e5b02be0fdaf273/drivers/sstar/gpio/infinity3/mhal_pinmux.c

## 80 pin QFN

| #  | Name                                       | #  | Name       | alt functions    | #  | Name     | #  | Name                                             | alt functions |
|----|--------------------------------------------|----|------------|------------------|----|----------|----|--------------------------------------------------|---------------|
| 1  | AUD_MICCM0                                 | 21 | PM_GPIO4   |                  | 41 | I2C1_SCL | 61 | VDD                                              |               |
| 2  | AUD_LINEOUT_L0                             | 22 | PM_SPI_CZ  |                  | 42 | I2C1_SDA | 62 | VDDP_3                                           |               |
| 3  | AVDDIO_DRAM                                | 23 | PM_SPI_DI  |                  | 43 | VDDP_2   | 63 | [SPI0_CZ](/ip/commonpins.md#spi0_cz)<sup>1</sup> |               |
| 4  | VDDIO_CMD                                  | 24 | PM_SPI_WPZ |                  | 44 | SR_IO02  | 64 | [SPI0_CK](/ip/commonpins.md#spi0_ck)<sup>1</sup> |               |
| 5  | VDD                                        | 25 | PM_SPI_DO  |                  | 45 | SR_IO03  | 65 | [SPI0_DI](/ip/commonpins.md#spi0_di)<sup>1</sup> |               |
| 6  | VDDIO_DATA                                 | 26 | PM_SPI_CK  |                  | 46 | SR_IO04  | 66 | [SPI0_DO](/ip/commonpins.md#spi0_d0)<sup>1</sup> |               |
| 7  | AVDD_PLL                                   | 27 | AVDD_XTAL  |                  | 47 | SR_IO05  | 67 | VDD                                              |               |
| 8  | DVDD_DDR_RX                                | 28 | XTAL_IN    |                  | 48 | SR_IO06  | 68 | SD_CLK                                           |               |
| 9  | SAR_GPIO3                                  | 29 | XTAL_OUT   |                  | 49 | SR_IO07  | 69 | SD_CMD                                           |               |
| 10 | SAR_GPIO2                                  | 30 | AVDD_ETH   |                  | 50 | SR_IO08  | 70 | SD_D0                                            |               |
| 11 | SAR_GPIO1                                  | 31 | ETH_RN     |                  | 51 | SR_IO09  | 71 | SD_D1                                            |               |
| 12 | SAR_GPIO0                                  | 32 | ETH_RP     |                  | 52 | SR_IO10  | 72 | SD_D2                                            |               |
| 13 | DVDD_NODIE                                 | 33 | ETH_TN     |                  | 53 | SR_IO11  | 73 | SD_D3                                            |               |
| 14 | AVDD_NODIE                                 | 34 | ETH_TP     |                  | 54 | SR_IO12  | 74 | AVDD_USB                                         |               |
| 15 | PM_SD_CDZ                                  | 35 | VDDP_1     |                  | 55 | SR_IO13  | 75 | USB_DM                                           |               |
| 16 | PM_IRIN                                    | 36 | FUART_RX   | spi0<sup>3</sup> | 56 | SR_IO14  | 76 | USB_DP                                           |               |
| 17 | [PM_RESET](/ip/commonpins.md#pm_reset)     | 37 | FUART_TX   | spi0<sup>3</sup> | 57 | SR_IO15  | 77 | AVDD_AUD                                         |               |
| 18 | [PM_UART_RX](/ip/commonpins.md#pm_uart_rx) | 38 | FUART_CTS  | spi0<sup>3</sup> | 58 | SR_IO16  | 78 | AUD_VAG                                          |               |
| 19 | [PM_UART_TX](/ip/commonpins.md#pm_uart_tx) | 39 | FUART_RTS  | spi0<sup>3</sup> | 59 | SR_IO17  | 79 | AUD_VRM_ADC                                      |               |
| 20 | GND_EFUSE                                  | 40 | VDD        |                  | 60 | VDD      | 80 | AUD_MICIN0                                       |               |

## 88 pin QFN

| #  | Name                                       | #  | Name                                       | #  | Name      | #  | Name        |
|----|--------------------------------------------|----|--------------------------------------------|----|-----------|----|-------------|
| 1  | AUD_MICIN0                                 | 23 | [PM_UART_TX](/ip/commonpins.md#pm_uart_tx) | 45 | FUART_CTS | 67 | VDD         |
| 2  | AUD_MICCM0                                 | 24 | GND_EFUSE                                  | 46 | FUART_RTS | 68 | VDD         |
| 3  | AUD_LINEOUT_L0                             | 25 | PM_GPIO4                                   | 47 | VDD       | 69 | VDDP_3      |
| 4  | AVDDIO_DRAM                                | 26 | PM_SPI_CZ                                  | 48 | I2C1_SCL  | 70 | SPI0_CZ     |
| 5  | VDDIO_CMD                                  | 27 | PM_SPI_DI                                  | 49 | I2C1_SDA  | 71 | SPI0_CK     |
| 6  | VDD                                        | 28 | PM_SPI_WPZ                                 | 50 | VDDP_2    | 72 | SPI0_DI     |
| 7  | AVDDIO_DRAM                                | 29 | PM_SPI_DO                                  | 51 | SR_IO02   | 73 | SPI0_DO     |
| 8  | VDDIO_DATA                                 | 30 | PM_SPI_CK                                  | 52 | SR_IO03   | 74 | PWM0        |
| 9  | VDDIO_DATA                                 | 31 | PM_SPI_HLD                                 | 53 | SR_IO04   | 75 | PWM1        |
| 10 | AVDD_PLL                                   | 32 | [PM_LED0](/ip/commonpins.md#pm_led0)       | 54 | SR_IO05   | 76 | VDD         |
| 11 | DVDD_DDR_RX                                | 33 | [PM_LED1](/ip/commonpins.md#pm_led1)       | 55 | SR_IO06   | 77 | SD_CLK      |
| 12 | SAR_GPIO3                                  | 34 | AVDD_XTAL                                  | 56 | SR_IO07   | 78 | SD_CMD      |
| 13 | SAR_GPIO2                                  | 35 | XTAL_IN                                    | 57 | SR_IO08   | 79 | SD_D0       |
| 14 | SAR_GPIO1                                  | 36 | XTAL_OUT                                   | 58 | SR_IO09   | 80 | SD_D1       |
| 15 | SAR_GPIO0                                  | 37 | AVDD_ETH                                   | 59 | SR_IO10   | 81 | SD_D2       |
| 16 | DVDD_NODIE                                 | 38 | ETH_RN                                     | 60 | SR_IO11   | 82 | SD_D3       |
| 17 | AVDD_NODIE                                 | 39 | ETH_RP                                     | 61 | SR_IO12   | 83 | AVDD_USB    |
| 18 | AVDDIO_DRAM                                | 40 | ETH_TN                                     | 62 | SR_IO13   | 84 | USB_DM      |
| 19 | PM_SD_CDZ                                  | 41 | ETH_TP                                     | 63 | SR_IO14   | 85 | USB_DP      |
| 20 | PM_IRIN                                    | 42 | VDDP_1                                     | 64 | SR_IO15   | 86 | AVDD_AUD    |
| 21 | [PM_RESET](/ip/commonpins.md#pm_reset)     | 43 | FUART_RX                                   | 65 | SR_IO16   | 87 | AUD_VAG     |
| 22 | [PM_UART_RX](/ip/commonpins.md#pm_uart_rx) | 44 | FUART_TX                                   | 66 | SR_IO17   | 88 | AUD_VRM_ADC |
