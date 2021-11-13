# ISP

The chips have two i2c slaves behind the uart pins that seems to work even when the uart is on.

For example on a mercury5 device with the uart pins connected to the i2c controller of a board
running linux we can see two slaves on the bus:

```
$ i2cdetect -y 0
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- -- 49 -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- 59 -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- -- 
```

These i2c slaves are present on infinity, infinity3, infinity2m, pioneer3.. and probably everything else.

# Debug tool

![isp tool front](debugtool_front_thumb.jpg)

- FTDI FT2232D
- NXP 74HC08D (Quad 2-input AND gate)
- Atmel 93C56A (2Kb EEPROM)

# Homebrew

- Adafruit 5v trinket.
- [i2c-tiny-usb](https://github.com/harbaum/I2C-Tiny-USB/tree/master/digispark)
- [flashrom](https://github.com/flashrom/flashrom) - If you have SPI NOR flash
  - If configured correctly flashrom has a driver that can talk via i2c to the flash very slowly.
  - ```make CONFIG_MSTARDDC_SPI=yes CONFIG_ENABLE_LIBPCI_PROGRAMMERS=no```
- [SNANDer fork with mstarddc support](https://github.com/fifteenhex/SNANDer/tree/mstar) for SPI NOR or NAND.
  - Same deal as flashrom, very slow!
  - Good enough to write the required blobs and u-boot.

# ISP SPI protocol

Some details on the SPI over i2c protocol are [here](http://boeglin.org/blog/index.php?entry=Flashing-a-BenQ-Z-series-for-free%40dom%40). The same windows tool is used for all MStar chips it seems so this is probably valid across the board.

The 0x49 i2c slave is the SPI bridge to the flash.

# ISP DEBUG protocol

- Lives on the 0x59 slave
- synchronization string is "SERDB".

Reading a bank of registers looks like this:

```
Writing "SERDB"

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42
---
Setting up something? Memory dump also has this sequence

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 34
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 45
---
"SERDB" again

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42

---
Another common senquence between register dump and mem dump

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
---
Common between reg dump and memdump

i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 1E
i2c-1: Data write: CF
i2c-1: Read
---
Common

i2c-1: Address read: B3
i2c-1: Data read: 00
i2c-1: Write
---
Common
i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 1E
i2c-1: Data write: CC
i2c-1: Read
---
common
i2c-1: Address read: B3
i2c-1: Data read: F5
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 1E
i2c-1: Data write: CD
i2c-1: Read
---
common
i2c-1: Address read: B3
i2c-1: Data read: 00
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 34
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 45
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
---
*** reg dump and mem dump diverge here ***
---
"SERDB"
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42
i2c-1: Write
---
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
---

This looks like a command and then bank 0x30?

i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 30
i2c-1: Data write: 00
i2c-1: Read
---

Register values?

i2c-1: Address read: B3
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 09
i2c-1: Data read: FF
i2c-1: Data read: FF
```

### Channel select

A lot of the above seems to be the sequence to select the desired channel

- Channel select sequence:
  - https://github.com/jockyw2001/utopia/blob/53ee8cc121a030b8d368113ac3e966b4705770ef/UTPA2-700.0.x/modules/demodulator/hal/maldives/demod/halDMD_INTERN_common.c#L319

## Booting from SDRAM

https://github.com/fifteenhex/SDK_pulbic/blob/c1436fa7446457e8d6547874d27ee4e34be150cf/Mercury5/proj/sc/driver/hal/mercury/kernel/inc/kernel_chiptop.h#L1897

## ISP tool scripts

- swch - Switch channel?
  - 0 - DRAM?
  - 3 - PM registers
  - 4 - Normal registers
- wsdr - Write a file?
- wriu - Write a register
  - `-b` write a byte?
  - `-w` write a word?
- wait - Wait for N seconds?

