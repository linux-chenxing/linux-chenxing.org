# Boot ROM

When the SoC is powered on the Boot ROM starts and tries to load the IPL from SPI NOR, SD or NAND and tries to jump into it.
The Boot ROM outputs some limited messages at 38400 baud. All of the IPLs so far use 115200 baud so this results in the Boot ROM messages showing as junk before the IPL output.

## Boot Media

There seem to be some strap pins to tell the boot rom which media to boot from. Booting from SD card, NAND and SPI NOR are apparently supported.

- Booting from SD card involves putting a file called IPL on the SD card in a FAT16 partition (partition type 0x4,0x6 or 0xe)
- Booting from SPI NOR involves putting the IPL at an address in the SPI NOR at an address that seems to be specific to the SoC

## Tags

At the end of the Boot ROM for infinity 3 forward there seems to be an ASCII tag that contains the git hash the ROM was built from.

## Messages

 - E:CD - This seems to be related to the boot ROM trying to load the IPL from SD but the card not being present. On MSC313e (infinity 3) this message is always present before booting from SPI NOR. Maybe because there aren't enough pins to have a strap for booting from SD so it always tries.
 - E:I - This seemas to mean that SD card couldn't be initialised.
 - E:F - This seems to mean that the MBR, partition with the IPL etc isn't right.
 - NF - Seems to mean the IPL file was not found in the FAT16 partition
 - F1 - Seems to mean the first IPL block couldn't be loaded
