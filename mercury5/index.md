# Mercury 5

The mercury 5 family seems to be targetted at dash recorders. So far all of the devices that have been obtained have been running something that seems to be based on eCOS and not Linux.

The mercury 5 seems to be very close to the [infinity3](/infinity3).

# Specs

- Probably a 800MHz Cortex A7
- 32KB Boot ROM
- 128KB SRAM (based on where the boot rom sets the stack pointer)
- MIPI DSI for an LCD panel
- 1 or 2 MIPI CSI for cameras
- Most if not all of the peripherals from the [infinity3](/infinity3/).

## Chips

### SSC8336

Probably the same chip as the SSC8336N but in QFP instead of QFN. Pinout seems to be identical.


#### Known Devices

- [Super cheapie ebay mirror dash cam](https://www.ebay.com/itm/9-66-Inch-2-5D-Mirror-Dash-Cam-Backup-Camera-For-Cars-Streaming-Media-Dual-I4D7/264489118570?ssPageName=STRK%3AMEBIDX%3AIT&_trksid=p2060353.m2749.l2649)

### SSC8336N

#### Pinout

128 Pin QFP/QFN

| #   | name         | #   | name         |
|-----|--------------|-----|--------------|
| 1   |              | 65  |              |
| 2   |              | 66  |              |
| 3   |              | 67  | sd dat1      |
| 4   |              | 68  | sd dat0      |
| 5   |              | 69  | sd cmd or clk|
| 6   |              | 70  | sd cmd or clk|
| 7   | usb          | 71  | sd dat3      |
| 8   | usb          | 72  | sd dat2      |
| 9   | usb          | 73  | camera mipi? |
| 10  | usb          | 74  | camera mipi? |
| 11  |              | 75  | camera mipi? |
| 12  |              | 76  | camera mipi? |
| 13  | vcore?       | 77  | camera mipi? |
| 14  |              | 78  | camera mipi? |
| 15  |              | 79  | camera mipi? |
| 16  |              | 80  | camera mipi? |
| 17  |              | 81  | camera mipi? |
| 18  |              | 82  | camera mipi? |
| 19  |              | 83  |              |
| 20  |              | 84  | i2c?         |
| 21  | 32khz xtal?  | 85  | i2c?         |
| 22  |              | 86  |              |
| 23  | 32khz xtal?  | 87  |              |
| 24  |              | 88  |              |
| 25  |              | 89  |              |
| 26  |              | 90  |              |
| 27  | pm spi cs    | 91  |?power supply?|
| 28  | pm spi di    | 92  |              |
| 29  | pm spi wp    | 93  |              |
| 30  | pm spi do    | 94  |              |
| 31  | pm spi clk   | 95  |              |
| 32  | pm spi hold  | 96  |              |
| 33  |              | 97  |              |
| 34  |              | 98  |              |
| 35  |              | 99  |              |
| 36  |              | 100 |              |
| 37  |              | 101 |              |
| 38  |              | 102 |              |
| 39  |              | 103 |              |
| 40  | pm uart tx   | 104 |              |
| 41  | pm uart rx   | 105 |              |
| 42  |              | 106 |              |
| 43  |              | 107 |              |
| 44  | vddr?        | 108 | mipi dsi d0p |
| 45  |              | 109 | mipi dsi d0n |
| 46  | vddr?        | 110 | mipi dsi d1p |
| 47  | vddr?        | 111 | mipi dsi d1n |
| 48  | vddr?        | 112 | mipi dsi clkp|
| 49  |              | 113 | mipi dsi clkn|
| 50  |              | 114 | mipi dsi d2p |
| 51  |              | 115 | mipi dsi d2n |
| 52  |              | 116 | mipi dsi d3p |
| 53  |              | 117 | mipi dsi d3n |
| 54  |              | 118 |              |
| 55  |              | 119 |              |
| 56  |              | 120 |              |
| 57  |              | 121 |              |
| 58  |              | 122 |              |
| 59  |              | 123 |              |
| 60  |              | 124 |              |
| 61  | i2c0         | 125 |              |
| 62  | i2c0         | 126 |              |
| 63  |              | 127 | xtal         |
| 64  | 3v3          | 128 | xtal         |

#### Boot ROM Tag

This is slighly interesting. Presumably I3 is infinity3 so maybe this chip's ROM is a hacked up. 

```
MVX1##I3gb83f2cbCMN_ROM######XVM
```

#### Known Devices 

##### 70mai Smart dash cam 

- [vendor page](https://www.70mai.com/en/70mai-dash-cam-lite/?gclid=EAIaIQobChMIzsLkl6y_5QIVEz5gCh1UOg9eEAAYASAAEgLvffD_BwE) 
- [fcc.io internal photos](https://fccid.io/2AOK9-MIDRIVED08/Internal-Photos/internal-photos-4351132)
- injoinc ip6303 pmic on i2c0@0x30 (custom i2c address and default voltages)
- SC7A30E accelerometer on i2c0@0x1d
- [ST7701S](http://www.startek-lcd.com/res/starteklcd/pdres/201705/20170512144242904.pdf) based 480x640 LCD
- Realtek 8188FTV usb wifi, probably RL-UM12BS-8188FTV-V3.0


### SSC8339D
