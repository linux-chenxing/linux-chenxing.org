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

# ISP protocol

Some details on the SPI over i2c protocol are [here](http://boeglin.org/blog/index.php?entry=Flashing-a-BenQ-Z-series-for-free%40dom%40). The same windows tool is used for all MStar chips it seems so this is probably valid across the board.
