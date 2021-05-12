# Infinity 6 pinouts

[vendor pinmux table](https://github.com/linux-chenxing/linux-ssc325/blob/mijia_camera_mstar323/drivers/sstar/gpio/infinity6/mhal_pinmux.c)

## 88 pin QFN

* Note: This is very close to the 88 pin QFN for i3. Only pin 60 and 61 seem to differ.

| #  | Name           | #  | Name       | #  | Name           | #  | Name        |
|----|----------------|----|------------|----|----------------|----|-------------|
| 1  | AUD_MICIN0     | 23 | PM_UART_TX | 45 | FUART_CTS      | 67 | VDD         |
| 2  | AUD_MICCM0     | 24 | GND_EFUSE  | 46 | FUART_RTS      | 68 | VDD         |
| 3  | AUD_LINEOUT_L0 | 25 | PM_GPIO4   | 47 | VDD            | 69 | VDDP_3      |
| 4  | AVDDIO_DRAM    | 26 | PM_SPI_CZ  | 48 | I2C1_SCL       | 70 | SPI0_CZ     |
| 5  | VDDIO_CMD      | 27 | PM_SPI_DI  | 49 | I2C1_SDA       | 71 | SPI0_CK     |
| 6  | VDD            | 28 | PM_SPI_WPZ | 50 | VDDP_2         | 72 | SPI0_DI     |
| 7  | AVDDIO_DRAM    | 29 | PM_SPI_DO  | 51 | SR_IO02        | 73 | SPI0_DO     |
| 8  | VDDIO_DATA     | 30 | PM_SPI_CK  | 52 | SR_IO03        | 74 | PWM0        |
| 9  | VDDIO_DATA     | 31 | PM_SPI_HLD | 53 | SR_IO04        | 75 | PWM1        |
| 10 | AVDD_PLL       | 32 | PM_LED0    | 54 | SR_IO05        | 76 | VDD         |
| 11 | DVDD_DDR_RX    | 33 | PM_LED1    | 55 | SR_IO06        | 77 | SD_CLK      |
| 12 | SAR_GPIO3      | 34 | AVDD_XTAL  | 56 | SR_IO07        | 78 | SD_CMD      |
| 13 | SAR_GPIO2      | 35 | XTAL_IN    | 57 | SR_IO08        | 79 | SD_D0       |
| 14 | SAR_GPIO1      | 36 | XTAL_OUT   | 58 | SR_IO09        | 80 | SD_D1       |
| 15 | SAR_GPIO0      | 37 | AVDD_ETH   | 59 | SR_IO10        | 81 | SD_D2       |
| 16 | DVDD_NODIE     | 38 | ETH_RN     | 60 | PAD_AUD_MICIN1 | 82 | SD_D3       |
| 17 | AVDD_NODIE     | 39 | ETH_RP     | 61 | PAD_AUD_MICCM1 | 83 | AVDD_USB    |
| 18 | AVDDIO_DRAM    | 40 | ETH_TN     | 62 | SR_IO13        | 84 | USB_DM      |
| 19 | PM_SD_CDZ      | 41 | ETH_TP     | 63 | SR_IO14        | 85 | USB_DP      |
| 20 | PM_IRIN        | 42 | VDDP_1     | 64 | SR_IO15        | 86 | AVDD_AUD    |
| 21 | PM_RESET       | 43 | FUART_RX   | 65 | SR_IO16        | 87 | AUD_VAG     |
| 22 | PM_UART_RX     | 44 | FUART_TX   | 66 | SR_IO17        | 88 | AUD_VRM_ADC |

| boot device           | PM_SPI_DO               | PM_SPI_CK |
|-----------------------|-------------------------|-----------|
| SPI NAND or SD        | 0                       | 1         |
| SPI NAND only         | 0                       | 0         |
| SPI NOR or SD         | 1                       | 0         |
| SPI NOR only          | 1                       | 1         |
