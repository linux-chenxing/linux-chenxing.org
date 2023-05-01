# Pioneer3

This seems to be a family that have both video capture hardware and display hardware.

## SDK

The SDK family is `ikayaki`.

## Flash Layout

### SPI NAND

- 0x0000000 - cis
- 0x0000800 - partition table
- 0x0001000 - flash table
- 0x0140000 - IPL copy 0
- 0x0340000 - IPL copy 1
- 0x0540000 - IPL copy 2

- 0x01a0000 - IPLN copy 0
- 0x01c0000 - IPLN copy 1
- 0x01e0000 - IPLN copy 2

- 0x0200000 - u-boot 0
- 

## SSD210

- Dual Cortex A7
- 64MB DDR2
- 57KB SRAM (Previously thought this was 64KB based on the USB loader binary size and the i2m having 64KB, seems they made it even smaller!!)
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



# DDR RE

Original  IPL output:

```
IPL g6b146fc
D-06
HW Reset
49104282 00871044
Resume? N, addr 00871044
miupll_200MHz
SPI 54M
64MB
BIST0_0001-OK
SPI 108M
[BBT] Found table @ 0x00020000
 
Checksum OK

IPL_CUST gd2b1bc7
[FLASH] SNI not match device, need to find correct SNI!
[FLASH] bad block 0x0000
[FLASH] Not found device id in SNI.
[FLASH] top/buttom = 0x0004
[FLASH] block = 0x0000
[FLASH] SRP0 = 0x0000
[FLASH] SRP1 = 0x0000
[FLASH] Found ext SNI @ 0xa0007850
[SPINAND] RFC use command 0xeb with 0x04 dummy clock.
[SPINAND] Setup timeout 0x0000c350 us.
[FLASH] Unlock all block.
Got BBT
load part: UBOOT00
load part: UBOOT00
Load BL from flash
total time 87358 us, size:280452 bytes 


U-Boot 2015.01farts (Jun 25 2022 - 09:24:27)

Version: P3g#######
I2C:   ready
DRAM:  
WARNING: Caches not enabled
SPINAND_I:  [FLASH] Found SNI in block 0.
[FLASH] dev_id = 0xee
[FLASH] mfr_id = 0xcd, dev_id= 0xea id_len = 0x3
[SPINAND] RFC ues command 0xeb with 0x04 dummy clock.
[FLASH] Unlock all block.
[FLASH] Use BDMA.
128 MiB
MMC:   MStar SD/MMC: 0
ENV: offset = 0x440000 size = 0x60000
ENV1: offset = 0x0 size = 0x0
ENV1 partition size set error!
*** Warning - ENV1 size error, using default environment

In:    serial
Out:   serial
Err:   serial
Net:   MAC Address 00:30:1B:BA:02:DB
Auto-Negotiation...
AN failLink Status Speed:10 Full-duplex:0
Status Error!
sstar_emac
Warning: sstar_emac using MAC address from net device

SigmaStar # 
```

MIU settings in vendor u-boot: 

```
SigmaStar # md.w 0x1f202000 0x200
1f202000: 0001 0000 aaaa 0000 0000 0000 0000 0000    ................
1f202010: 003f 0000 1100 0000 0000 0000 008f 0000    ?...............
1f202020: 0000 0000 0000 0000 0000 0000 0200 0000    ................
1f202030: 0000 0000 8000 0000 0020 0000 6005 0000    ........ ....`..
1f202040: 4020 0000 0004 0000 0000 0000 0000 0000     @..............
1f202050: 8000 0000 0000 0000 0114 0000 1122 0000    ............"...
1f202060: 8000 0000 0029 0000 2004 0000 0400 0000    ....).... ......
1f202070: 0077 0000 7070 0000 9111 0000 1111 0000    w...pp..........
1f202080: 0000 0000 0000 0000 0000 0000 8800 0000    ................
1f202090: 0077 0000 7070 0000 0011 0000 0011 0000    w...pp..........
1f2020a0: 1111 0000 0000 0000 4000 0000 0000 0000    .........@......
1f2020b0: 0a0a 0000 aaaa 0000 aaaa 0000 aaaa 0000    ................
1f2020c0: b3c8 0000 007f 0000 f000 0000 0044 0000    ............D...
1f2020d0: 2020 0000 2020 0000 0808 0000 0808 0000      ..  ..........
1f2020e0: 0800 0000 8801 0000 0404 0000 0404 0000    ................
1f2020f0: 0001 0000 0000 0000 0000 0000 0000 0000    ................
1f202100: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202110: 0011 0000 0001 0000 0000 0000 0000 0000    ................
1f202120: f0f1 0000 0000 0000 1516 0000 0000 0000    ................
1f202130: 0000 0000 0000 0000 ff00 0000 007f 0000    ................
1f202140: bcdc 0000 cddc 0000 3232 0000 4311 0000    ........22...C..
1f202150: 1111 0000 1111 0000 1111 0000 1111 0000    ................
1f202160: 3802 0000 000e 0000 0000 0000 0000 0000    .8..............
1f202170: 1111 0000 0111 0000 0111 0000 0111 0000    ................
1f202180: 001f 0000 0000 0000 0000 0000 0000 0000    ................
1f202190: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2021a0: 4444 0000 4444 0000 4444 0000 4444 0000    DD..DD..DD..DD..
1f2021b0: 0044 0000 0000 0000 0000 0000 0000 0000    D...............
1f2021c0: 5555 0000 5555 0000 5555 0000 5555 0000    UU..UU..UU..UU..
1f2021d0: 0055 0000 0000 0000 0000 0000 1f1f 0000    U...............
1f2021e0: 1f1f 0000 0000 0000 0000 0000 0200 0000    ................
1f2021f0: 8600 0000 0007 0000 c0c0 0000 c0c0 0000    ................
1f202200: 8015 0000 2008 0000 0400 0000 ffff 0000    ..... ..........
1f202210: ffff 0000 3210 0000 7654 0000 ba98 0000    .....2..Tv......
1f202220: fedc 0000 ffff 0000 0000 0000 0000 0000    ................
1f202230: 0000 0000 0000 0000 0000 0000 0040 0000    ............@...
1f202240: 8015 0000 2008 0000 0400 0000 0000 0000    ..... ..........
1f202250: ffff 0000 3210 0000 7654 0000 ba98 0000    .....2..Tv......
1f202260: fedc 0000 ffff 0000 0000 0000 0000 0000    ................
1f202270: 0000 0000 0000 0000 0000 0000 0040 0000    ............@...
1f202280: 0000 0000 0000 0000 2000 0000 0000 0000    ......... ......
1f202290: 0000 0000 0000 0000 ffff 0000 ffff 0000    ................
1f2022a0: 00ff 0000 001f 0000 0000 0000 0000 0000    ................
1f2022b0: 0000 0000 0000 0000 1000 0000 0000 0000    ................
1f2022c0: 0000 0000 0000 0000 0000 0000 0030 0000    ............0...
1f2022d0: 5000 0000 0028 0000 0000 0000 ffff 0000    .P..(...........
1f2022e0: 0000 0000 2000 0000 0242 0000 0000 0000    ..... ..B.......
1f2022f0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202300: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202310: 0000 0000 0000 0000 0000 0000 707c 0000    ............|p..
1f202320: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202330: 0000 0000 0000 0000 60ff 0000 001f 0000    .........`......
1f202340: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202350: 0000 0000 0000 0000 0b0b 0000 0b0b 0000    ................
1f202360: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202370: 0000 0000 0000 0000 0000 0000 07ff 0000    ................
1f202380: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202390: 0000 0000 0000 0000 8321 0000 0000 0000    ........!.......
1f2023a0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2023b0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2023c0: 0002 0000 001e 0000 0000 0000 0000 0000    ................
1f2023d0: 0018 0000 4008 0000 0202 0000 0808 0000    .....@..........
1f2023e0: 0008 0000 7170 0000 0000 0000 0000 0000    ....pq..........
1f2023f0: ffe1 0000 1074 0000 0000 0000 00e1 0000    ....t...........
```

```
1f202400: 800f 0000 0292 0000 0051 0000 1b50 0000    ........Q...P...
1f202410: 1e99 0000 2777 0000 95a8 0000 404c 0000    ....w'......L@..
1f202420: 0003 0000 4004 0000 8000 0000 c000 0000    .....@..........
1f202430: 0000 0000 0000 0000 0000 0000 8008 0000    ................
1f202440: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202450: 0070 0000 0000 0000 8021 0000 0000 0000    p.......!.......
1f202460: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202470: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202480: 8015 0000 2008 0000 0400 0000 0000 0000    ..... ..........
1f202490: ffff 0000 3210 0000 7654 0000 ba98 0000    .....2..Tv......
1f2024a0: fedc 0000 ffff 0000 0000 0000 0000 0000    ................
1f2024b0: 0000 0000 0000 0000 0000 0000 0040 0000    ............@...
1f2024c0: 8015 0000 2008 0000 0400 0000 0000 0000    ..... ..........
1f2024d0: ffff 0000 3210 0000 7654 0000 ba98 0000    .....2..Tv......
1f2024e0: fedc 0000 ffff 0000 0000 0000 0000 0000    ................
1f2024f0: 0000 0000 0000 0000 0000 0000 0040 0000    ............@...
1f202500: 8015 0000 2008 0000 0400 0000 0000 0000    ..... ..........
1f202510: ffff 0000 3210 0000 7654 0000 ba98 0000    .....2..Tv......
1f202520: fedc 0000 ffff 0000 0000 0000 0000 0000    ................
1f202530: 0000 0000 ffff 0000 0000 0000 0040 0000    ............@...
1f202540: 8015 0000 2008 0000 0400 0000 0000 0000    ..... ..........
1f202550: ffff 0000 3210 0000 7654 0000 ba98 0000    .....2..Tv......
1f202560: fedc 0000 0000 0000 0000 0000 0000 0000    ................
1f202570: 0000 0000 0000 0000 0000 0000 0040 0000    ............@...
1f202580: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f202590: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2025a0: 0000 0000 6000 0000 00c0 0000 0000 0000    .....`..........
1f2025b0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2025c0: 0000 0000 0000 0000 ffff 0000 003e 0000    ............>...
1f2025d0: 5aa5 0000 0000 0000 0000 0000 0000 0000    .Z..............
1f2025e0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2025f0: 0000 0000 0000 0000 951a 0000 80e1 0000    ................
```


```
miupll reg 0x0000 - 0x0000
miupll reg 0x0004 - 0x0000
miupll reg 0x0008 - 0x0000
miupll reg 0x000c - 0x0119
miupll reg 0x0010 - 0x0010
miupll reg 0x0014 - 0x0000
miupll reg 0x0018 - 0x0000
miupll reg 0x001c - 0x0000
miupll reg 0x0020 - 0x0000
miupll reg 0x0024 - 0x0000
miupll reg 0x0028 - 0x0000
miupll reg 0x002c - 0x0000
miupll reg 0x0030 - 0x0000
miupll reg 0x0034 - 0x0000
miupll reg 0x0038 - 0x0000
miupll reg 0x003c - 0x0000
miupll reg 0x0040 - 0x0000
miupll reg 0x0044 - 0x0000
miupll reg 0x0048 - 0x0000
miupll reg 0x004c - 0x0000
miupll reg 0x0050 - 0x0000
miupll reg 0x0054 - 0x0000
miupll reg 0x0058 - 0x0000
miupll reg 0x005c - 0x0000
miupll reg 0x0060 - 0x0000
miupll reg 0x0064 - 0x0000
miupll reg 0x0068 - 0x0000
miupll reg 0x006c - 0x0000
miupll reg 0x0070 - 0x0000
miupll reg 0x0074 - 0x0000
miupll reg 0x0078 - 0x0000
miupll reg 0x007c - 0x0000
miupll reg 0x0080 - 0x0000
miupll reg 0x0084 - 0x0000
miupll reg 0x0088 - 0x0000
miupll reg 0x008c - 0x0000
miupll reg 0x0090 - 0x0000
miupll reg 0x0094 - 0x0000
miupll reg 0x0098 - 0x0000
miupll reg 0x009c - 0x0000
miupll reg 0x00a0 - 0x0000
miupll reg 0x00a4 - 0x0000
miupll reg 0x00a8 - 0x0000
miupll reg 0x00ac - 0x0000
miupll reg 0x00b0 - 0x0000
miupll reg 0x00b4 - 0x0000
miupll reg 0x00b8 - 0x0000
miupll reg 0x00bc - 0x0000
miupll reg 0x00c0 - 0x0000
miupll reg 0x00c4 - 0x0000
miupll reg 0x00c8 - 0x0000
miupll reg 0x00cc - 0x0000
miupll reg 0x00d0 - 0x0000
miupll reg 0x00d4 - 0x0000
miupll reg 0x00d8 - 0x0000
miupll reg 0x00dc - 0x0000
miupll reg 0x00e0 - 0x0000
miupll reg 0x00e4 - 0x0000
miupll reg 0x00e8 - 0x0000
miupll reg 0x00ec - 0x0000
miupll reg 0x00f0 - 0x0000
miupll reg 0x00f4 - 0x0000
miupll reg 0x00f8 - 0x0000
miupll reg 0x00fc - 0x0000
```


https://www.diffchecker.com/nFuNXkf0

# JTAG

TMS - SR_IO1
TCK - SR_IO0
TDO - SR_IO2
TDI - SR_IO3

