# linux-chenxing

## Intro

This is intended to be a repository for info on the MStar/[SigmaStar](http://www.sigmastarsemi.com) SoCs.
The name is a parody of linux-sunxi for Allwinner SoCs. MStar in Chinese is
chenxing and the newer SigmaStar name is xingchen.

This will probably never get as big as linux-sunxi so github pages should be
more than enough.

Before MStar was bought out by MediaTek the company offered a wide range
of SoCs focused at STB and camera applications. Since the company was
bought by MediaTek the camera SoC part of the company has been spun out
into the fully owned subsidiary called Sigmastar. The camera SoCs that are 
now marketed by Sigmastar will be the main focus here.

It's worth noting that the MStar/Sigmastar camera SoCs seem to be derived
from the SoCs made by Alpha Imaging Technology which was merged into MStar
at some point.

# Porting Progress Matrix

## u-boot

|           | load u-boot SPL from vendor IPL | load u-boot from SPI NOR |
|-----------|---------------------------------|--------------------------|
| infinity  | yes                             | yes                      |
| infinity3 | yes                             | yes                      |
| infinity6 | wip                             | wip                      |
| mercury5  | yes                             | yes                      |

## linux

|           | boots to shell from initramfs | boots to shell from local storage | full system from local storage with network etc |
|-----------|-------------------------------|-----------------------------------|-------------------------------------------------|
| infinity  | yes                           | yes                               | yes                                             |
| infinity3 | yes                           | yes                               | yes                                             |
| infinity6 | wip                           | wip                               | wip                                             |
| mercury5  | yes                           | wip                               | wip                                             |

# Reverse Engineering Progress

|           | sample device acquired | boot rom dumped | firmware dumped | SDK acquired | databrief acquired | datasheet acquired |
|-----------|------------------------|-----------------|-----------------|--------------|--------------------|--------------------|
| infinity1 | yes                    | yes             | yes             | yes[0]       |                    |                    |
| infinity3 | yes                    | yes             | yes             | yes[0]       | yes                |                    |
| infinity6 | yes                    |                 | yes             |              |                    |                    |
| mercury5  | yes                    | yes             | yes             |              |                    |                    |

- [0] SDK seems to actually be for the infinity1 but the infinity3 is very similar

# SoCs

## MIPS based

MStar used to make a lot of MIPS based SoCs for STBs. These aren't that
interesting in themselves but the IP blocks used in the MIPS SoCs were
carried forward to the later ARM chips so any datasheets that can be found
for the MIPS SoCs might help with reverse engineering the current ARM based
ones.

### STB

- MSD7818
- MSD7828

## ARM based

### Cedric Family

- [MST786](cedric#mst786) - Dual core Cortex A9 automotive (head unit) SoC

### Infinity IP camera family

#### [Infinity 1](infinity1)
- [MSC313](infinity1#msc313) - Cortex A7 + 64MB DDR2 in a QFN80

#### [Infinity 3](infinity3)
- [MSC313E](infinity3#msc313e) - Cortex A7 + 64MB DDR2 in a QFN80
- [MSC316DC](infinity3#msc316dc) - Cortex A7 + 128MB DDR3 in a QFN88

#### [Infinity 5](infinity5)
- [SSC328Q](infinity5#ssc328q) - Cortex A7 + 256MB DDR3 (this might be i6)
- [SSC329Q](infinity5#ssc329q) - Cortex A7 + 256MB DDR3 + NPU (this might be i6)

#### [Infinity 6](infinity6)
- [SSC325](infinity6#ssc325) - Cortex A7 + 64MB DDR2 in a QFN88
- [SSC325DE](infinity6#ssc325de) - Cortex A7 + 128MB DDR3 in a QFN88
- [SSC326D](infinity6#ssc326d) - Cortex A7 + 128MB DDR3 + NPU
- [SSC327DE](infinity6#ssc327de) - Cortex A7 + 128MB DDR3

### Mercury family

#### [Mercury 2](mercury2)

- [AIT8328/MSC8328](mercury2#msc8328) - Probably ARM9
- [AIT8428](mercury2#ait8428) - Probably ARM9

#### [Mercury 5](mercury5)

- [SSC8336N](mercury5#ssc8336n) - Cortex A7 + 64MB DDR2
- [SSC8339D](mercury5#ssc8339d) - Probably in this family, probably Cortex A7

### Misc

- [MSB2521](misc/msb2521.md) - ARM9 based SatNav on a chip
- MSB2531 - Cortex A7 SatNav on a chip

# IP blocks

See [IP](ip).

# ISP/Debug Tool

See [ISP](isp).

# Blobs, headers, layouts

- [BootROM](blobs/bootrom.md) - Baked in BootROM
- [IPL](blobs/ipl.md) - First/Second stage bootloaders
- [MXPT](blobs/mxpt.md) - Partition table used for SPI NOR

## Sources of firmwares for reverse engineering

- [Anjvision firmwares](http://www.anjvision.com:8021/firmware/)

To get the device tree out of the kernel you can use binwalk + [extract-dtb](https://github.com/PabloCastellano/extract-dtb.git) and dtc.

```
binwalk -e <firmware.bin>
extract-dtb.py <extracted firmware dir><uncompressed kernel blob>
dtc -I dtb -O dts -o out.dts <extracted dtb that looks right>
```
