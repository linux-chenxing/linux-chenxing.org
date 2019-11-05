# IPL blobs

## First stage IPL loaded by the bootrom

This is usually copied from memory mapped SPI NOR into the internal SRAM (IMI).

- First 4 bytes are an ARM instruction to jump somewhere else in the IPL binary like a reset vector.
   This also seems to be generally used to switch from ARM to Thumb execution.
- Second 4 bytes are "IPL_"
- Third 4 bytes are the size of the IPL

### mercury5 notes

- This *seems* to be located at 0x1000 in SPI NOR or the file IPL on an SD card in a fat16 partition.
- The vendor IPL loads a kernel image from the file RTS on an SD card in a fat16 partition.

### infinity3 notes

- Located at 0x4000 in SPI NOR.

### infinity6 notes

- Located at 0x0 in SPI NOR.

## Second stage IPL loaded by the first stage IPL

The header format is the same as the first stage IPL but the second 4 bytes are "IPLC"
