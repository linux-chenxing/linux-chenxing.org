# linux-chenxing

## Intro

This is intended to be a repository for info on the MStar/SigmaStar SoCs.
The name is a parody of linux-sunxi for Allwinner SoCs. MStar in Chinese is
chenxing and the newer SigmaStar name is xingchen.

This will probably never get as big as linux-sunxi so github pages should be
more than enough.

Before MStar was bought out by MediaTek the company offered a wide range
of SoCs focused at STB and camera applications. Since the company was
bought by MediaTek the camera SoC part of the company has been spun out
into the fully owned subsidiary called Sigmastar. The camera SoCs that are 
now marketed by Sigmastar will be the main focus here.

# SoCs

## MIPS based

MStar used to make a lot of MIPS based SoCs for STBs. These aren't that
interesting in themselves but the IP blocks used in the MIPS SoCs were
carried forward to the later ARM chips so any datasheets that can be found
for the MIPS SoCs might help with reverse engineering the current ARM based
ones.

## ARM based

### Cedric Family

- MST786 - Dual core Cortex A9 tablet SoC

### Infinity IP camera family

#### Infinity 1
- MSC313 - Cortex A7 + 64MB DDR2 in a QFN80

#### [Infinity 3](infinity3)
- [MSC313E](infinity3#msc313e) - Cortex A7 + 64MB DDR2 in a QFN80
- [MSC316DC](infinity3#msc316dc) - Cortex A7 + 128MB DDR3 in a QFN88

#### [Infinity 6](infinity6)
- [SSC326D](infinity6#ssc326d) - Cortex A7 + 128MB DDR3
- [SSC328Q](infinity6#ssc328q) - Cortex A7 + 256MB DDR3

### Misc

- [MSB2521](misc/msb2521.md) - ARM9 based SatNav on a chip
- MSB2531 - Cortex A7 SatNav on a chip

# IP blocks

See [IP](ip).
