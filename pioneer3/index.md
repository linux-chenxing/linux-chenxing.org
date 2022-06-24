# Pioneer3

This seems to be a family that have both video capture hardware and display hardware.

## SDK

The SDK family is `ikayaki`.

## Flash Layout

### SPI NAND

0x0000000 - cis
0x0000800 - partition table
0x0001000 - flash table
0x0014000 - IPL copy 0
0x0034000 - IPL copy 1
0x0054000 - IPL copy 2

## SSD210

- Dual Cortex A7
- 64MB DDR2
- 64KB SRAM (based on usb loader IPL size)
- .35mm pitch (?) 68 (+ exposed pad) pin QFN
- xx KB Boot ROM with support for booting from SPI NOR, SPI NAND, USB 

### QFN 68 Pinout

[pad mux table](https://github.com/linux-chenxing/linux-ssc325/blob/e53dccbcd926a883a2859695a6b8839e12daf321/drivers/sstar/gpio/pioneer3/mhal_pinmux.c#L441)

| #  | name           | alt functions           | power domain | #  | name        | alt functions                                | power domain | #  | name        | alt functions                              | power domain | #  | name        | alt functions | power domain |
|----|----------------|-------------------------|--------------|----|-------------|----------------------------------------------|--------------|----|-------------|--------------------------------------------|--------------|----|-------------|---------------|--------------|
| 1  | AUD_LINEOUT_L0 |                         |              | 18 | SR_IO09     | bt656_dout[6] </br> pspi1_clk                | VDDP_1       | 35 | TTL6        | ttl_dout[13]</br>ttl_dout[8]</br>spi0_mosi | VDDP_2       | 52 | VDD         |               |              |
| 2  | PM_SPI_CZ      |                         |              | 19 | SR_IO10     | bt656_dout[7]</br>pspi1_mosi</br>ttl_dout[0] | VDDP_1       | 36 | TTL7        | ttl_dout[12]</br>ttl_dout[9]</br>spi0_miso | VDDP_2       | 53 | USB2_DP     |               |              |
| 3  | PM_SPI_CK      |                         |              | 20 | SR_IO11     | bt656_ck</br>pspi1_miso</br>ttl_dout[1]      | VDDP_1       | 37 | TTL8        | uart1_tx                                   | VDDP_2       | 54 | USB2_DM     |               |              |
| 4  | PM_SPI_DI      |                         |              | 21 | DVDD_DDR_RX |                                              |              | 38 | GND_EFUSE?  |                                            |              | 55 | AVDD3P3_USB |               |              |
| 5  | PM_SPI_DO      |                         |              | 22 | AVDD_PLL    |                                              |              | 39 | TTL11       | uart1_rx                                   | VDDP_2       | 56 | VDD         |               |              |
| 6  | PM_SPI_HLD     |                         |              | 23 | AVDDIO_DRAM |                                              |              | 40 | VDDP_2_3318 |                                            |              | 57 | RESET       |               |              |
| 7  | PM_SPI_WPZ     |                         |              | 24 | VDDIO_DATA  |                                              |              | 41 | TTL12       | eth0_mdio, uart2_tx                        | VDDP_2       | 58 | PM_UART_TX  |               |              |
| 8  | VDD            |                         |              | 25 | AVDDIO_DRAM |                                              |              | 42 | TTL13       | eth0_mdc, uart2_rx                         | VDDP_2       | 59 | PM_UART_RX  |               |              |
| 9  | SR_IO00        |                         | VDDP_1       | 26 | VDD         |                                              |              | 43 | TTL14       | eth0_txd1                                  | VDDP_2       | 60 | SAR_GPIO2   |               |              |
| 10 | SR_IO01        |                         | VDDP_1       | 27 | VDDIO_MCLK  |                                              |              | 44 | TTL15       | eth0_txd0                                  | VDDP_2       | 61 | SAR_GPIO1   |               |              |
| 11 | SR_IO02        | bt656_dout[0]           | VDDP_1       | 28 | AVDDIO_DRAM |                                              |              | 45 | TTL16       | eth0_tx_en                                 | VDDP_2       | 62 | SAR_GPIO0   |               |              |
| 12 | SR_IO03        | bt656_dout[1]           | VDDP_1       | 29 | TTL0        | ttl_de</br>ttl_dout[2]                       | VDDP_2       | 46 | TTL17       | eth0_tx_clk                                | VDDP_2       | 63 | AVDD_XTAL   |               |              |
| 13 | SR_IO04        | bt656_dout[2]           | VDDP_1       | 30 | TTL1        | ttl_vsync</br>ttl_dout[3]                    | VDDP_2       | 47 | TTL18       | i2c0_scl, eth0_col                         | VDDP_2       | 64 | XTAL_IN     |               |              |
| 14 | SR_IO05        | bt656_dout[3]           | VDDP_1       | 31 | TTL2        | ttl_hsync</br>ttl_dout[4]                    | VDDP_2       | 48 | TTL19       | i2c0_sda, eth0_rxd0                        | VDDP_2       | 65 | XTAL_OUT    |               |              |
| 15 | SR_IO06        | bt656_dout[4]           | VDDP_1       | 32 | TTL3        | ttl_ck</br>ttl_dout[5]                       | VDDP_2       | 49 | TTL20       | i2c1_scl0, eth0_rxd1                       | VDDP_2       | 66 | AVDD_AUD    |               |              |
| 16 | SR_IO07        | bt656_dout[5], pspi1_cs | VDDP_1       | 33 | TTL4        | ttl_dout[15]</br>ttl_dout[6]</br>spi0_cz     | VDDP_2       | 50 | TTL21       | i2c1_sda0                                  | VDDP_2       | 67 | AUD_VAG     |               |              |
| 17 | VDDP_1_3318    |                         |              | 34 | TTL5        | ttl_dout[14]</br>ttl_dout[7]</br>spi0_ck     | VDDP_2       | 51 | VDD         |                                            |              | 68 | AUD_VRM_DAC |               |              |

## Boot strap pins

| USB bootloader        | PM_SPI_HLD              |
|-----------------------|-------------------------|
| USB bootloader        | 0 - boot device ignored |
| Normal boot           | 1                       |

| boot device           | PM_SPI_DO               | PM_SPI_CK |
|-----------------------|-------------------------|-----------|
| SPI NAND or SD        | 0                       | 1         |
| SPI NAND only         | 0                       | 0         |
| SPI NOR or SD         | 1                       | 0         |
| SPI NOR only          | 1                       | 1         |

Yes, the PM_SPI_CK seems weird.

| secure boot           | PM_SPI_DI               |
|-----------------------|-------------------------|
| on                    | 0                       |
| off                   | 1                       |

| boot mode             | PM_SPI_WPZ              |
|-----------------------|-------------------------|
| ???                   | 0                       |
| ROM                   | 1                       |

# Known devices

- [Widora](https://sns.widora.io/topic/767/ssd210-demo%E6%9D%BF-%E4%B8%8B%E4%B8%80%E6%AD%A5%E5%87%86%E5%A4%87%E7%82%B9%E5%B1%8F)
- [qfn68demo](qfn68demo)

## SSD212

- [pinout](SSD212_pinout.png)
- [sv50pd](sv50pd)

## SSC9211

- [Local notes](ssc9211.md)

### Known devices

- [qfn68demo](qfn68demo)
