# Mercury 5

The mercury 5 family seems to be targetted at dash recorders. So far all of the devices that have been obtained have been running something that seems to be based on uC/OSII and not Linux.

The mercury 5 seems to be very close to the [infinity3](/infinity3).

# Specs

- Probably a 800MHz Cortex A7 (Main ID register is 0x410fc075, confirms cortex A7)
- 32KB Boot ROM
- 128KB SRAM (based on where the boot rom sets the stack pointer)

## Chips

### SSC8336N

#### Pinout

128 Pin QFN

| #   | name         |
|-----|--------------|
| 1   |              |
| 2   |              |
| 3   |              |
| 4   |              |
| 5   |              |
| 6   |              |
| 7   |              |
| 8   |              |
| 9   | usb          |
| 10  | usb          |
| 11  |              |
| 12  |              |
| 13  |              |
| 14  |              |
| 15  |              |
| 16  |              |
| 17  |              |
| 18  |              |
| 19  |              |
| 20  |              |
| 21  |              |
| 22  |              |
| 23  |              |
| 24  |              |
| 25  |              |
| 26  |              |
| 27  | pm spi cs    |
| 28  | pm spi di    |
| 29  | pm spi wp    |
| 30  | pm spi do    |
| 31  | pm spi clk   |
| 32  | pm spi hold  |
| 33  |              |
| 34  |              |
| 35  |              |
| 36  |              |
| 38  |              |
| 39  |              |
| 40  |              |
| 41  |              |
| 42  |              |
| 43  |              |
| 44  |              |
| 45  |              |
| 46  |              |
| 47  |              |
| 48  |              |
| 49  |              |
| 50  |              |
| 51  |              |
| 52  |              |
| 53  |              |
| 54  |              |
| 55  |              |
| 56  |              |
| 57  |              |
| 58  |              |
| 59  |              |
| 60  |              |
| 61  | i2c0         |
| 62  | i2c0         |
| 63  | 3v3          |
| 67  | sd dat1      |
| 68  | sd dat0      |
| 69  | sd cmd or clk|
| 70  | sd cmd or clk|
| 71  | sd dat3      |
| 72  | sd dat2      |
| 73  | camera mipi? |
| 74  | camera mipi? |
| 75  | camera mipi? |
| 76  | camera mipi? |
| 77  | camera mipi? |
| 78  | camera mipi? |
| 79  | camera mipi? |
| 80  | camera mipi? |
| 81  | camera mipi? |
| 82  | camera mipi? |
| 83  |              |
| 84  | i2c?         |
| 85  | i2c?         |
| 86  |              |
| 87  |              |
| 88  |              |
| 89  |              |
| 90  |              |
| 91  |              |
| 92  |              |
| 93  |              |
| 94  |              |
| 95  |              |
| 96  |              |
| 97  |              |
| 98  |              |
| 99  |              |
| 100 |              |
| 101 |              |
| 102 |              |
| 103 |              |
| 104 |              |
| 105 |              |
| 106 |              |
| 107 |              |
| 108 |              |
| 109 |              |
| 110 |              |
| 111 |              |
| 112 |              |
| 113 |              |
| 114 |              |
| 115 |              |
| 116 |              |
| 117 |              |
| 118 |              |
| 119 |              |
| 120 |              |
| 121 |              |
| 122 |              |
| 123 |              |
| 124 |              |
| 125 |              |
| 126 |              |
| 127 | xtal         |
| 128 | xtal         |


#### Boot ROM Tag

This is slighly interesting. Presumably I3 is infinity3 so maybe this chip's ROM is a hacked up. 

```
MVX1##I3gb83f2cbCMN_ROM######XVM
```

#### Known Devices 

##### 70mai Smart dash cam 

- [vendor page](https://www.70mai.com/en/70mai-dash-cam-lite/?gclid=EAIaIQobChMIzsLkl6y_5QIVEz5gCh1UOg9eEAAYASAAEgLvffD_BwE) 
- [fcc.io internal photos](https://fccid.io/2AOK9-MIDRIVED08/Internal-Photos/internal-photos-4351132)
- injoinc ip6303 pmic on i2c0@0x30
- mma7660(?) accelerometer on i2c0@0x1d


### SSC8339D
