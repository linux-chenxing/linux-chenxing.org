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
| 9   | usb          |
| 10  | usb          |
| 27  | pm spi cs    |
| 28  | pm spi di    |
| 29  | pm spi wp    |
| 30  | pm spi do    |
| 31  | pm spi clk   |
| 32  | pm spi hold  |
| 61  | i2c0         |
| 62  | i2c0         |
| 63  | 3v3          |
| 67  | sd dat1      |
| 68  | sd dat0      |
| 69  |              |
| 70  |              |
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
