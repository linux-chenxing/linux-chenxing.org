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

| #   | name         | #   | name         |
|-----|--------------|-----|--------------|
| 1   |              | 65  |              |
| 2   |              | 66  |              |
| 3   |              | 67  | sd dat1      |
| 4   |              | 68  | sd dat0      |
| 5   |              | 69  | sd cmd or clk|
| 6   |              | 70  | sd cmd or clk|
| 7   |              | 71  | sd dat3      |
| 8   |              | 72  | sd dat2      |
| 9   | usb          | 73  | camera mipi? |
| 10  | usb          | 74  | camera mipi? |
| 11  |              | 75  | camera mipi? |
| 12  |              | 76  | camera mipi? |
| 13  |              | 77  | camera mipi? |
| 14  |              | 78  | camera mipi? |
| 15  |              | 79  | camera mipi? |
| 16  |              | 80  | camera mipi? |
| 17  |              | 81  | camera mipi? |
| 18  |              | 82  | camera mipi? |
| 19  |              | 83  |              |
| 20  |              | 84  | i2c?         |
| 21  |              | 85  | i2c?         |
| 22  |              | 86  |              |
| 23  |              | 87  |              |
| 24  |              | 88  |              |
| 25  |              | 89  |              |
| 26  |              | 90  |              |
| 27  | pm spi cs    | 91  |              |
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
| 40  |              | 104 |              |
| 41  |              | 105 |              |
| 42  |              | 106 |              |
| 43  |              | 107 |              |
| 44  |              | 108 |              |
| 45  |              | 109 |              |
| 46  |              | 110 |              |
| 47  |              | 111 |              |
| 48  |              | 112 |              |
| 49  |              | 113 |              |
| 50  |              | 114 |              |
| 51  |              | 115 |              |
| 52  |              | 116 |              |
| 53  |              | 117 |              |
| 54  |              | 118 |              |
| 55  |              | 119 |              |
| 56  |              | 120 |              |
| 57  |              | 121 |              |
| 58  |              | 122 |              |
| 59  |              | 123 |              |
| 60  |              | 124 |              |
| 61  | i2c0         | 125 |              |
| 62  | i2c0         | 126 |              |
| 63  | 3v3          | 127 | xtal         |
| 64  |              | 128 | xtal         |

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
