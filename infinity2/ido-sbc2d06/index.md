# IDO-SBC2D06

![board](board_thumb.jpg)

## Specs

## Hardware notes

- Second ethernet uses gpio0, gpio1, ttl16-23 (probably eth1 mode4 with ttl16 as a gpio for phy reset)
- The dip switches (J11) control whether pm uart is connected to the usb->serial or the debug header. For flashing via the debug header you need to put them to the left (close to the expansion header) and to use the serial port over usb you need to put them to the right (close to the debug connector).

## Pinouts

| #  | name           | #  | name   |
|----|----------------|----|--------|
| 1  | sys_3v3        | 2  | vcc_5v |
| 3  | gpio3/i2c1_sda | 4  | vcc_5v |
| 5  | gpio2/i2c1_scl | 6  | gnd    |
| 7  |                | 8  |        |
| 9  |                | 10 |        |
| 11 |                | 12 |        |
| 13 |                | 14 |        |
| 15 |                | 16 |        |
| 17 |                | 18 |        |
| 19 |                | 20 |        |
| 21 |                | 22 |        |
| 23 |                | 24 |        |
| 25 |                | 26 |        |
| 27 |                | 28 |        |
| 29 |                | 30 |        |
| 31 |                | 32 |        |
| 33 |                | 34 |        |
| 35 |                | 36 |        |
| 37 |                | 38 |        |
| 39 |                | 40 |        |

## Misc

- [schematic](ido-sbc2d06-v1b-20210311(1).pdf)
