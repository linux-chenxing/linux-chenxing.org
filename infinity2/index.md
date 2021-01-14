# infinity2

# infinity2m

## Specs

- Dual Cortex A7
- Only 64KB of internal SRAM

## MSR620 / SSR621D

### Known Devices

### TL-NVR6108C-B

[internals etc](tlnvr6108cb/)

[vendor page](https://www.tp-link.com.cn/product_1497.html#tag)

## SSD201/SSD202

Seems to be all of the base stuff the other chips have with an extra ethernet
controller, a video decoder intead of encoder etc.

- Chip id: 0xf0

### SSD201

- [Data brief](SSD201_pb_S_v01.pdf)

### SSD202

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

##### SSD201_HT_V2

[see](ssd201_ht_v2/)

##### [ido-som2d01](http://www.wireless-tag.cn/portfolio/ido-som2d01-2/)

Cheap solder down IoT module.

[online doc](http://doc.industio.com/docs/ssd20x-system/page_0)

##### GW300

GW300 is a SSD201 and the GW302 is a SSD202D

- [vendor page](http://myzr.com.cn/public/index/index/product/id/115.html)
- [tear down etc](gw300)

##### [widora](https://github.com/widora/SSD202)

Widora are apparently designing a board.

##### Pinout

See [pinouts](pinouts.md).
