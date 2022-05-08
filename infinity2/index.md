# infinity2

# infinity2m

## Specs

- Dual Cortex A7
- Only 64KB of internal SRAM
- 16KB boot ROM
- Boot from SPI NOR or SPI NAND

## MSR620 / SSR621D

### Known Devices

### TL-NVR6108C-B

[internals etc](tlnvr6108cb/)

[vendor page](https://www.tp-link.com.cn/product_1497.html#tag)

## SSD201/SSD202D/SSD203D/SSR621D/SSR621Q

Seems to be all of the base stuff the other chips have with an extra ethernet
controller, a video decoder intead of encoder etc.

- Chip id: 0xf0

### SSD201

IPL output:

```
IPL g5da0ceb
D-1d
HW Reset
miupll_166MHz
miu_bw_set
utmi_1_init done
utmi_2_init done
utmi_3_init done
usbpll init done......
cpupll init done
SPI 54M
clk_init done 
P1 USB_rterm trim=0x0001
P1 USB_HS_TX_CURRENT trim=0x0002
P2 USB_rterm trim=0x0001
P2 USB_HS_TX_CURRENT trim=0x0001
P3 USB_rterm trim=0x0001
P3 USB_HS_TX_CURRENT trim=0x0001
PM_vol_bgap trim=0x0002
GCR_SAR_DATA trim=0x0190
ETH 10T output swing trim=0x0010
ETH 100T output swing trim=0x0010
ETH RX input impedance trim=0x0000
ETH TX output impedance trim=0x0000
MIPI_HS_RTERM trim=0x0001
MIPI_LP_RTERM trim=0x0000
64MB
BIST0_0001-OK
Enable MMU and CACHE
Load IPL_CUST from SPINAND
unable to find IDX for part type:0001
[I]m7
Checksum OK
```

- [Data brief](SSD201_pb_S_v01.pdf)

### SSD202D

- [Data brief](SSD202D_pb_S_v01.pdf)

IPL output:

```
IPL g5da0ceb
D-1e
HW Reset
miupll_233MHz
MIU0 zq=0x003c
miu_bw_set
utmi_1_init done
utmi_2_init done
utmi_3_init done
usbpll init done......
cpupll init done
SPI 54M
clk_init done 
P1 USB_rterm trim=0x0000
P1 USB_HS_TX_CURRENT trim=0x0001
P2 USB_rterm trim=0x0000
P2 USB_HS_TX_CURRENT trim=0x0001
P3 USB_rterm trim=0x0000
P3 USB_HS_TX_CURRENT trim=0x0001
PM_vol_bgap trim=0x0002
GCR_SAR_DATA trim=0x0190
ETH 10T output swing trim=0x0000
ETH 100T output swing trim=0x0000
ETH RX input impedance trim=0x0000
ETH TX output impedance trim=0x0001
MIPI_HS_RTERM trim=0x0001
MIPI_LP_RTERM trim=0x0000
128MB
BIST0_0001-OK
Enable MMU and CACHE
Load IPL_CUST from SPINAND
unable to find IDX for part type:0001
[I]m7
Checksum OK
```

#### Known Devices

##### DongShanPi One

[see](dongshanpione/)

##### SSD201_HT_V2

[see](ssd201_ht_v2/)

##### [ido-som2d01](http://www.wireless-tag.cn/portfolio/ido-som2d01-2/)

Cheap solder down IoT module.

- [online doc from the vendor](http://doc.industio.com/docs/ssd20x-system/page_0)
- [local info](ido-som2d01/)

##### IDO-SBC2D06

- [local info](ido-sbc2d06/)

- [Raspberry Pi style board](https://item.taobao.com/item.htm?spm=a1z10.5-c.w4002-22922295238.13.376753d5S4NXzN&id=642882871788)

##### IDO-SBC2D70

- [local info](ido-sbc2d70/)

##### IDO-SBC2D86

- [local info](ido-sbc2d86/)

##### MYZR-SSD20X-CB096

- [vendor page](http://www.myzr.com.cn/public/index/index/product/id/141.html)

##### GW300

GW300 is a SSD201 and the GW302 is a SSD202D. MYZR-SSD20X-CB096 module.

- [vendor page](http://www.myzr.com.cn/public/index/index/product/id/115.html)
- [tear down etc](gw300)
- [module](http://www.myzr.com.cn/public/indexen/index/product/id/141.html)

##### [widora](https://github.com/widora/SSD202)

Widora are apparently designing a board.

##### m5stack

[unitv2](unitv2)
 - CoreChips SR9900A http://www.corechip-sz.com/enproductsview.asp?id=25

##### Yet another SSD202D 7inch display

https://item.taobao.com/item.htm?spm=a230r.1.14.125.35d915f7J4vCkg&id=643200464062&ns=1&abbucket=5#detail

##### Yet another SSD201/SSD202D solder down module

https://www.geniatech.com/product/som20x/

##### Miyoo Mini

- [local info](miyoomini/)

##### N1Pro

- [local info](n1pro/)

##### Pinout

See [pinouts](pinouts.md).
