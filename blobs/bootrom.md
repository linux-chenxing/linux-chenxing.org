# Boot ROM

When the SoC is powered on the Boot ROM starts and tries to load the [IPL](ipl.html) from somewhere and tries to jump into it.
The Boot ROM outputs some limited messages at 38400 baud. All of the IPLs so far use 115200 baud so this results in the Boot ROM messages showing as junk before the IPL output.

## Boot Media

There seem to be some strap pins to tell the boot rom which media to boot from. Booting from eMMC, SD card, NAND and SPI NOR are apparently supported.

- For mercury5 booting from SD card involves putting a file called IPL on the SD card in a FAT16 partition (partition type 0x4,0x6 or 0xe).
- Booting from SPI NOR involves putting the IPL at an address in the SPI NOR that seems to be specific to the SoC:
  * For infinity 3 the address is 0x4000
- Booting from SPI NAND seems to invole some metadata being put into the first "golden" block of the NAND so that the bootrom can reliably load the IPL from NAND. There seems to be some support for backup blocks. The metadata seems to be dependant on the type of chip being used and there is a tool to generate the right metadata from a list of chips. However, there also seem to be generic data that can be loaded that allows the boot rom to load the IPL but maybe doesn't handle bad blocks.

## Tags

At the end of the Boot ROM for infinity 3 forward there seems to be an ASCII tag that contains the git hash the ROM was built from.
BROM Tag/Signature can be viewed by using the u-boot command `md.b 0x3fe0 0x20` or `md.b 0x7fe0 0x20`.

## Messages

 - E:CD - This seems to be related to the boot ROM trying to load the IPL from SD but the card not being present. On MSC313e (infinity 3) this message is always present before booting from SPI NOR. Maybe because there aren't enough pins to have a strap for booting from SD so it always tries.
 - E:I - This seems to mean that SD card couldn't be initialised.
 - E:F - This seems to mean that the MBR, partition with the IPL etc isn't right.
 - NF - Seems to mean the IPL file was not found in the FAT16 partition
 - F1 - Seems to mean the first IPL block couldn't be loaded

## SMP

For SMP systems all cores boot the same boot ROM but all CPUs other than 0 stop in a loop that waits for an interrupt and checks if the boot address and magic number are valid. When an interrupt comes and the registers are valid the secondary CPU will jump to the address.

## Dumping
 
 Enable capture in minicom and then at the u-boot prompt enter
 
 ```
 md.b 0x0 0x8000
 ```
 Then clean up the header and footer of the capture so there are no extra lines and use [uboot-mdb-dump](https://github.com/gmbnomis/uboot-mdb-dump) to turn the dump into a binary. Make sure the binary has a tag at the end. Some ROMs are 16KB and some are 32KB so check the 32KB dump to see if it repeats and turncate it with dd if needed like so:
 
 ```
 dd if=bootrom.bin of=fixed_bootrom.bin bs=1024 count=16
 ```
