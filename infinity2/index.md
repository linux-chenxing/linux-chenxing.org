# MSR620 / SSR621D

# Known Devices

## TL-NVR6108C-B

[internals etc](tlnvr6108cb/)

[vendor page](https://www.tp-link.com.cn/product_1497.html#tag)

# SSD201/SSD202

Seems to be all of the base stuff the other chips have with an extra ethernet
controller, a video decoder intead of encoder etc.

- Chip id: 0xf0

## SSD201

- [Data brief](SSD201_pb_S_v01.pdf)

## SSD202

- [Data brief](SSD202D_pb_S_v01.pdf)

## Known Devices

### SSD201_HT_V2

[see](ssd201_ht_v2/)

### [ido-som2d01](http://www.wireless-tag.cn/portfolio/ido-som2d01-2/)

### GW300

*probably*

http://myzr.com.cn/public/index/index/product/id/115.html

Cheap solder down IoT module.

### [widora](https://github.com/widora/SSD202)

Widora are apparently designing a board.

## Pinout

https://github.com/fifteenhex/linux-ssc325/blob/93240ba80ed1eff069eaca968e5b02be0fdaf273/drivers/sstar/gpio/infinity2m/mhal_pinmux.c

| #  | name         | #  | name        | #  | name      | alt functions | #   | name           |            |
|----|--------------|----|-------------|----|-----------|---------------|-----|----------------|------------|
| 1  | GPIO12       | 33 | PM_RESET    | 65 | TTL6      |               | 97  | SD_D2          |            |
| 2  | GPIO13       | 34 | PM_UART_RX  | 66 | TTL7      |               | 98  | VDDP_1         |            |
| 3  | GPIO14       | 35 | PM_UART_TX  | 67 | TTL8      |               | 99  | GPIO0          |            |
| 4  | VDD          | 36 | GPIO47      | 68 | TTL9      |               | 100 | GPIO1          |            |
| 5  | GPIO85       | 37 | GPIO48      | 69 | TTL10     |               | 101 | GPIO2          |            |
| 6  | GPIO86       | 38 | UART1_RX    | 70 | TTL11     |               | 102 | GPIO3          |            |
| 7  | DMIC_R       | 39 | UART1_TX    | 71 | TTL12     |               | 103 | PM_LED0        |            |
| 8  | DMIC_L       | 40 | VDDIO_DATA  | 72 | TTL13     |               | 104 | PM_LED1        |            |
| 9  | DMIC_CLK     | 41 | AVDDIO_DRAM | 73 | TTL14     |               | 105 | VDD            |            |
| 10 | GPIO90       | 42 | VDD         | 74 | TTL15     |               | 106 | AVDD_ETH       |            |
| 11 | VDDP_0       | 43 | VDDIO_DATA  | 75 | AVDD1     |               | 107 | ETH_RN         |            |
| 12 | VDD          | 44 | VDDIO_DATA  | 76 | VDDP_1    |               | 108 | ETH_RP         |            |
| 13 | AVDD_XTAL    | 45 | VDDIO_DATA  | 77 | VDD       |               | 109 | ETH_TN         |            |
| 14 | XTAL_IN      | 46 | AVDDIO_DRAM | 78 | VDD       |               | 110 | ETH_TP         |            |
| 15 | XTAL_OUT     | 47 | AVSSIO_DQ   | 79 | TTL16     | mdio?         | 111 | DP_P2          |            |
| 16 | SE_XTAL_OUT  | 48 | AVDD_PLL    | 80 | TTL17     | mdc?          | 112 | DM_P2          |            |
| 17 | AVDD_RTC     | 49 | DVDD_DDR    | 81 | TTL18     |               | 113 | AVDD_USB       |            |
| 18 | XTAL_IN_32K  | 50 | DVDD_DDR_RX | 82 | TTL19     |               | 114 | AVDD_AUD       |            |
| 19 | XTAL_OUT_32K | 51 | VDD         | 83 | TTL20     | rmii_rxd0?    | 115 | AUD_LINEOUT_R0 |            |
| 20 | SAR_GPIO2    | 52 | FUART_RX    | 84 | TTL21     | rmii_rxd1?    | 116 | AUD_LINEOUT_L0 |            |
| 21 | SAR_GPIO1    | 53 | FUART_TX    | 85 | TTL22     | rmii_txd0?    | 117 | AUD_MICCM0     |            |
| 22 | SAR_GPIO0    | 54 | FUART_CTS   | 86 | TTL23     | rmii_txd1?    | 118 | AUD_MICIN0     |            |
| 23 | AVDD_NODIE   | 55 | FUART_RTS   | 87 | TTL24     | rmii_txen?    | 119 | AUD_VRM_DAC    |            |
| 24 | GND_EFUSE    | 56 | TTL0        | 88 | TTL25     |               | 120 | AUD_VAG        |            |
| 25 | VDD          | 57 | TTL1        | 89 | TTL26     |               | 121 | GPIO4          |            |
| 26 | PM_SPI_CZ    | 58 | TTL2        | 90 | TTL27     |               | 122 | GPIO5          |            |
| 27 | PM_SPI_CK    | 59 | TTL3        | 91 | PM_SD_CDZ |               | 123 | GPIO6          |            |
| 28 | PM_SPI_DI    | 60 | TTL4        | 92 | SD_D1     |               | 124 | GPIO7          |            |
| 29 | PM_SPI_DO    | 61 | TTL5        | 93 | SD_D0     |               | 125 | UART2_RX       | spi0_mode5 |
| 30 | PM_SPI_HLD   | 62 | DP_P1       | 94 | SD_CLK    |               | 126 | UART2_TX       | spi0_mode5 |
| 31 | PM_SPI_WPZ   | 63 | DM_P1       | 95 | SD_CMD    |               | 127 | GPIO10         | spi0_mode5 |
| 32 | PM_IRIN      | 64 | AVDD_USB    | 96 | SD_D3     |               | 128 | GPIO11         | spi0_mode5 |
