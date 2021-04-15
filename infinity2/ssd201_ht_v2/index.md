# SSD201_HT_V2

This seems to be an official dev board.
It's available from taobao for ~$200.

The vendor provided a copy of the SDK but no schematics or chip documentation.

![board](board.jpg)

## Hardware

- SigmaStar SSD201 or SSD202 SoC
- IC Plus [IP101GR](https://datasheet.lcsc.com/szlcsc/IC-Plus-IP101GR_C79324.pdf) PHY for the second eithernet.
- SSW101B connected via USB for WiFi
- SGM4890 Audio Amp
- FS35ND01G SPI NAND 1Gbit
- 1838T IR receiver
- Goodix 911 touchscreen
- i2c0 mode4 on jp3
- spi0 mode5 on jp4
- 24bit 7 inch LCD panel

### lsusb

```
Bus 002 Device 006: ID 1b20:8888                                                                                                                        
Bus 001 Device 001: ID 1d6b:0002                                                                                                                                                                                                          
Bus 002 Device 001: ID 1d6b:0002
```

## Reg dumps

LPLL

```
/ # devmem 0x1f206700
0x00002201
/ # devmem 0x1f206704
0x00000420
/ # devmem 0x1f206708
0x00000042
/ # devmem 0x1f20670c
0x00000001
/ # devmem 0x1f206710
0x00000000
/ # devmem 0x1f206714
0x00000000
/ # devmem 0x1f206718
0x00000000
/ # devmem 0x1f20671c
0x00000000
/ # devmem 0x1f206720
0x0000C3C3
/ # devmem 0x1f206724
0x00000043
/ # devmem 0x1f206728
0x00000001
/ # devmem 0x1f20672c
0x00000000
```
## Vendor partition table

```
0x000000140000-0x0000001a0000 : "IPL0"
0x0000001a0000-0x000000200000 : "IPL1"
0x000000200000-0x000000260000 : "IPL_CUST0"
0x000000260000-0x0000002c0000 : "IPL_CUST1"
0x0000002c0000-0x000000380000 : "UBOOT0"
0x000000380000-0x000000440000 : "UBOOT1"
0x000000440000-0x0000004a0000 : "ENV0"
0x0000004a0000-0x0000004c0000 : "KEY_CUST"
0x0000004c0000-0x000000520000 : "LOGO"
0x000000520000-0x000000a20000 : "KERNEL"
0x000000a20000-0x000000f20000 : "RECOVERY"
0x000000f20000-0x000008000000 : "UBI"
```
