# IPL blobs

## First stage IPL loaded by the bootrom

This is usually copied from memory mapped SPI NOR into the internal SRAM (IMI).

- First 4 bytes are an ARM instruction to jump somewhere else in the IPL binary like a reset vector.
   This also seems to be generally used to switch from ARM to Thumb execution.
- Second 4 bytes are "IPL_"
- Third 4 bytes are the size of the IPL
- Forth 4 bytes are a checksum of the upcoming data. The checksum is just each u32 of the data added together. The boot rom        doesn't seem to actually check this and not all IPL version check it before loading the second stage IPLC.

### mercury5 notes

- This *seems* to be located at 0x1000 in SPI NOR or the file IPL on an SD card in a fat16 partition.
- The vendor IPL loads a kernel image from the file RTS on an SD card in a fat16 partition. It seems to load to 0x20008000 (in DDR) and jumps there.

### infinity3 notes

- Located at 0x4000 in SPI NOR.

#### Version capability/feature matrix

| version               | msc313 | msc313e | msc316dc | checks IPLC chksum | notes |
|-----------------------|--------|---------|----------|--------------------|-------|
| I3g0c706bbIPL_QFN64MW | y      | y       | n[0]     | n                  |       |
| I3gd156225IPL_EFUSE   | ?      | y       | y        | y                  |[1]    |

- 0 - Runs but can't init the DRAM
- 1 - Makes extensive use of magic numbers in the efuse area, this version can apparently
      detect if the included memory is DDR2 or DDR3

### infinity6 notes

- Located at 0x0 in SPI NOR.

#### Version capability/feature matrix

| version               | msc313 | msc313e | msc316dc | checks IPLC chksum | notes |
|-----------------------|--------|---------|----------|--------------------|-------|
| I6gf1d3932IPL         |        |         |          |                    |       |

## Second stage IPL loaded by the first stage IPL

The header format is the same as the first stage IPL but the second 4 bytes are "IPLC"




