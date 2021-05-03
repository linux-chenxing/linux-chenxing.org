# ido-som2d01

## Specs

- SSD201 or SSD202D
- 128MB SPI NAND
- Sigmastar Wifi

## Quick start

### Wiring

The minimum you need to wire up to get something going is:
- SYS_3V3 (1) - Connect to a 3.3v supply
- GND1 (2) - Connect to ground
- PM_UART_RX (25) - Connect TX on your usb->serial adapter
- PM_UART_TX (26) - Connect RX on your usb->serial adapter

### Flashing

See [ISP](/isp)

- You need to write the "GCIS" to 0x0
- You need to write the IPL to 0x140000
- You need to write the u-boot SPL to 0x200000

## Datasheets etc

These are available from the vendors site, mirrored here so they don't disappear.

- [Datasheet (Chinese)](IDO-SOM2D01-Datasheet-CN.pdf)
- [Datasheet (English)](IDO-SOM2D01-Datasheet_EN.pdf)
- [Hardware design guide (Chinese)](IDO-SOM2D01硬件设计手册.pdf)

## Misc

### lsusb output

```
# lsusb 
Bus 002 Device 002: ID 1b20:8888
Bus 001 Device 001: ID 1d6b:0002
Bus 002 Device 001: ID 1d6b:0002
# 
```
