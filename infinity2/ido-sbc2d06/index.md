# IDO-SBC2D06

![board](board_thumb.jpg)

## Hardware notes

- Second ethernet uses gpio0, gpio1, ttl16-23 (probably eth1 mode4 with ttl16 as a gpio for phy reset)
- The dip switches (J11) control whether pm uart is connected to the usb->serial or the debug header. For flashing via the debug header you need to put them to the left (close to the expansion header) and to use the serial port over usb you need to put them to the right (close to the debug connector).
