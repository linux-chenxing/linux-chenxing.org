# linux-chenxing

[Github project](https://github.com/linux-chenxing)

## Intro

This is intended to be a repository for info on the MStar/[SigmaStar](http://www.sigmastarsemi.com) SoCs
and the associated mainling effort.

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

## FAQ

- Q: Why linux-chenxing?
- A: The name is a parody of linux-sunxi for Allwinner SoCs. MStar in Chinese is
     chenxing and the newer SigmaStar name is xingchen.

- Q: Is this the official support site for MStar/SigmaStar?
- A: No. There is no relationship between this site and the vendor. This is a
     "community" (community meaning one fat guy with a multimeter right now) research
     effort.
     
- Q: Have you reached out to the vendor to get more information?
- A: Yes, they said without an NDA and project in place they cannot help.
     Signing an NDA would be a bad idea for code that is going mainline.

- Q: If I pay you money will you support me using the official SDKs?
- A: No.

- Q: Is there an IRC channel, discord or something for discussion?
- A: Please use github's [discussion feature](https://github.com/linux-chenxing/linux-chenxing.org/discussions) for now.

- Q: Should I upload SDKs and post links here?
- A: Please don't. Extract the parts that are licensed in a friendly way
    (i.e. GPLv2 or BSD) and push them onto github or somewhere and link that instead.
    
    The exception to this rule is where the SDK has already been leaked to github.
    For example there are some copies of the SDKs that seem to have been uploaded by
    manufacturers that are actually trying to comply with the licenses covering the kernel, u-boot etc
    and uploaded the entire SDK.

    Basically, if someone else leaks their copy of an SDK that's their problem.

- Q: Should I upload datasheets or other references here?
- A: Maybe. If they are already easy to download then putting them here for non-profit educational/research
     purposes should be ok. IANAL but as far as I can tell github is in the US and
     [fair use](https://www.copyright.gov/title17/92chap1.html#107) applies.

     Materials that are behind an NDA wall like those in the SDKs might be interesting but
     most of the information they contain can be worked out from the kernel sources or about
     stuff contained the proprietary modules we don't really care about anyways.

- Q: Why is Tux orange and why does he have a stalk and leaf sticking out of his head?
- A: The SigmaStar logo is an orange isn't it? Looks like one to me.

# Porting Progress Matrix

## u-boot

For most chips u-boot is loaded by loading the SPL as IPL-CUST from the IPL so that blob is needed.
The mercury5 however can boot with the u-boot SPL as the IPL so no blobs are required.
Getting the other chips to boot without the vendor IPL is mostly a case of doing the DDR setup in the SPL.

|                           | load u-boot SPL from boot ROM | load u-boot SPL from vendor IPL | load u-boot from SPI NOR | load u-boot from SPI NAND | load u-boot from SD |
|---------------------------|-------------------------------|---------------------------------|--------------------------|---------------------------|---------------------|
| [infinity1](#infinity1)   |                               | yes                             | yes                      |                           |                     |
| [infinity2m](#infinity2m) |                               | yes                             | wip                      | yes                       |                     |
| [infinity3](#infinity3)   |                               | yes                             | yes                      |                           |                     |
| [infinity5](#infinity5)   |                               | wip                             | wip                      |                           |                     |
| [infinity6](#infinity6)   |                               | wip                             | wip                      |                           |                     |
| [infinity6b0](#infinity6) |                               | wip                             | wip                      |                           |                     |
| [infinity6e](#infinity6)  |                               |                                 |                          |                           |                     |
| [mercury5](#mercury5)     | yes, SD                       | yes                             | yes                      |                           | yes                 |
| [pioneer3](#pioneer3)     |                               |                                 |                          |                           |                     |

## linux

|                          | boots to shell from initramfs | boots to shell from local storage | full system from local storage with network etc | boots without blobs (no vendor IPL) | smp |
|--------------------------|-------------------------------|-----------------------------------|-------------------------------------------------|-------------------------------------|-----|
| [infinity1](#infinity1)  | yes                           | yes                               | yes                                             |                                     |     |
| [infinity2m](#infinity2) | yes                           |                                   | yes                                             |                                     | yes |
| [infinity3](#infinity3)  | yes                           | yes                               | yes                                             |                                     |     |
| [infinity5](#infinity5)  |                               |                                   |                                                 |                                     |     |
| [infinity6](#infinity6)  | wip                           | wip                               | wip                                             |                                     |     |
| [infinity6b0](#infinity6)| yes                           | wip                               | wip                                             |                                     |     |
| [infinity6e](#infinity6) |                               |                                   |                                                 |                                     |     |
| [mercury5](#mercury5)    | yes                           | yes                               | yes                                             | yes                                 |     |
| [mercury6](#mercury6)    |                               |                                   |                                                 |                                     |     |
| [pioneer3](#pioneer3)    |                               |                                   |                                                 |                                     |     |

# Data Mining Progress

This table is an attempt to collect all of the different part numbers for
the different families and the resources that have been found to reverse engineer each of them.

If possible the data codes will have the earliest and latest known date codes so that we can tell roughly
when each type of chip was produced.

| family                    | part     | date codes | process size | sample device acquired | boot rom dumped | firmware dumped | SDK acquired | product brief acquired                | datasheet acquired                       |
|---------------------------|----------|------------|--------------|------------------------|-----------------|-----------------|--------------|---------------------------------------|------------------------------------------|
| [cedric](#cedric)         |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | mst786   |            |              |                        |                 |                 |              |                                       | [yes](cedric/mst786_ds_v01maite_new.pdf) |
| [infinity1](#infinity1)   |          |            |              |                        |                 |                 | yes[0]       |                                       |                                          |
|                           | msc313   | 1647B      |              | yes                    | yes             |                 |              |                                       |                                          |
|                           | msc313d  | 1638B      |              |                        |                 |                 |              |                                       |                                          |
| [infinity2m](#infinity2m) |          |            |              |                        |                 |                 | yes          |                                       |                                          |
|                           | msr620   |            |              |                        |                 |                 |              |                                       |                                          |
|                           | msr620q  | 1717S      |              |                        |                 |                 |              |                                       |                                          |
|                           | ssr621d  | 1945S      |              | yes                    | yes             | yes             |              |                                       |                                          |
|                           | ssd201   |            |              |                        |                 |                 |              | [yes](infinity2/SSD201_pb_S_v01.pdf)  |                                          |
|                           | ssd202d  |            |              |                        |                 |                 |              | [yes](infinity2/SSD202D_pb_S_v01.pdf) |                                          |
| [infinity3](#infinity3)   |          |            |              |                        |                 |                 | yes[0]       |                                       |                                          |
|                           | msc313e  | 1744B      |              | yes                    | yes             | yes             |              | [yes](infinity3/msc313e_pb_v03.pdf)   |                                          |
|                           |          | 1916S      |              |                        |                 |                 |              |                                       |                                          |
|                           | msc316dc | 1929S      |              | yes                    | same as msc313e | yes             |              | [yes](infinity3/msc316dc_pb_v03.pdf)  |                                          |
|                           | msc316q  |            |              |                        |                 |                 |              | [yes](infinity3/msc316q_pb_v01.pdf)   |                                          |
|                           | msc318   |            |              |                        |                 |                 |              | [yes](infinity3/msc318_pb_v03.pdf)    |                                          |
| [infinity5](#infinity5)   |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssa520d  |            |              |                        |                 |                 |              |                                       |                                          |
| [infinity6](#infinity6)   |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssc323   | 1928S      |              |                        |                 |                 |              |                                       |                                          |
|                           |          | 1936J      |              |                        |                 |                 |              |                                       |                                          |
|                           | ssc325   | 1937S      |              | yes                    | yes             | yes             |              |                                       |                                          |
|                           | ssc333   |            | 28nm         |                        |                 |                 |              |                                       |                                          |
|                           | ssc333de |            | 28nm         |                        |                 |                 |              |                                       |                                          |
| [infinity6b0](#infinity6) |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssc335   |            | 28nm         |                        |                 |                 |              |                                       |                                          |
|                           | ssc336d  |            | 22nm         |                        |                 |                 |              |                                       |                                          |
|                           | ssc336q  |            | 22nm         |                        |                 |                 |              |                                       |                                          |
|                           | ssc337de |            | 28nm         | yes                    |                 |                 |              |                                       |                                          |
|                           | ssc338q  |            | 22nm         |                        |                 |                 |              |                                       |                                          |
|                           | ssc338g  |            | 22nm         |                        |                 |                 |              |                                       |                                          |
| [infinity6e](#infinity6e) |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssc339g  |            | 22nm         |                        |                 |                 |              |                                       |                                          |
| [mercury2](#mercury2)     |          |            |              | yes                    |                 |                 |              |                                       |                                          |
|                           | msc8328  | 1744       |              |                        |                 | yes             |              |                                       |                                          |
| [mercury5](#mercury5)     |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssc8336  | 1915S      |              | yes                    |                 | yes             |              |                                       |                                          |
|                           | ssc8336n | 1918S      |              | yes                    | yes             | yes             |              |                                       |                                          |
|                           |          | 1936S      |              |                        |                 |                 |              |                                       |                                          |
|                           | ssc8339d | 1838A      |              |                        |                 |                 |              | yes                                   |                                          |
| [mercury6](#mercury6)     |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssd268g  |            |              |                        |                 |                 |              |                                       |                                          |
| [pioneer3](#pioneer3)     |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssd210   |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssd212   |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssc9211  | 2118S      |              |                        | yes             | yes             |              |                                       |                                          |
| misc                      |          |            |              |                        |                 |                 |              |                                       |                                          |
|                           | ssa330d  |            |              |                        |                 |                 |              | [yes](/misc/SSA330D.pdf)              |                                          |
|                           | ssa530g  |            |              |                        |                 |                 |              | [yes](/misc/SSA530G.pdf)              |                                          |
|                           | ssd222   |            |              |                        |                 |                 |              | [yes](/misc/SSD222.pdf)               |                                          |

- [0] SDK seems to actually be for the infinity1 but the infinity3 is very similar
- [List up of some newer chips with process size info](http://bbs.16rd.com/thread-568161-1-1.html)

# Mainlining progress

See [mainlining](mainlining.md)

# SoCs

Spotted a chip that isn't here? Please see [adding new chips](addingnewchips.md).

## MIPS based

MStar used to make a lot of MIPS based SoCs for STBs. These aren't that
interesting in themselves but the IP blocks used in the MIPS SoCs were
carried forward to the later ARM chips so any datasheets that can be found
for the MIPS SoCs might help with reverse engineering the current ARM based
ones.

### STB

- MSD7818
- MSD7828

## 32bit ARM based

### Napoli?

- [MSO9810]() - Quad Core ARM Cortex-A9

### Cedric Family

- [MST786](cedric#mst786) - Dual core Cortex A9 automotive (head unit) SoC

### Infinity IP camera family

#### [Infinity1](infinity1)

- IP camera chips with video encoder and camera interface

- [MSC313](infinity1#msc313) - Cortex A7 + 64MB DDR2 in a QFN80
- [MSC313D](infinity1#msc313d) - Probably a Cortex A7 + 128MB DDR3 in a BGA

#### [Infinity2](infinity2)

- part numbers not known. there are some references in the SDKs etc to infinity2 and it seems
  to be dual Cortex A9
- Probably for the recording side i.e. has a video decoder and no camera interface.

#### [Infinity2m](infinity2)

- Closer to the [infinity6](#infinity6) chips than the infinity2.
- Probably a replacement for the recording side, has video decoder, framebuffer etc.

- [SSR621D](infinity2#ssr621d) - Dual Cortex A7 128MB DDR3(TBC) in QFN128 with HDMI, VGA, SATA
- [SSD201](infinity2#ssd201) - Dual Cortex A7 with 64MB of DDR2 in QFN128
- [SSD202D](infinity2#ssd202d) - Dual Cortex A7 with 128MB of DDR3 in a QFN128

- [MSR620?](http://www.sigmastarsemi.com/en/products/info.aspx?itemid=390&lcid=53&pid=) Maybe "k6lite" family
- [MSR630?](http://www.sigmastarsemi.com/en/products/info.aspx?itemid=391&lcid=53&pid=) Maybe "k6" family
  - [TL-NVR6104C-4PX](https://www.tp-link.com.cn/product_1388.html#tag) (based on MSR630 being in the source paths in the kernel binary)

#### [Infinity3](infinity3)

- Updated version of the infinity1

- [MSC313E](infinity3#msc313e) - Cortex A7 + 64MB DDR2 in a QFN80
- [MSC316DC](infinity3#msc316dc) - Cortex A7 + 128MB DDR3 in a QFN88
- [MSC316Q](infinity3) - Cortex A7 + 128MB DDR3 in a 256 ball BGA
- [MSC318](infinity3) - Cortex A7 + 128MB DDR3 in a 324 ball BGA 

#### Infinity 4

Doesn't seem to exist.

#### [Infinity5](infinity5)

- Seems to be a version of the infinity3 that can handle higher resoltion sensors.

- [SSC328Q](infinity5#ssc328q) - Cortex A7 + 256MB DDR3 (this might be i6)
- [SSC329Q](infinity5#ssc329q) - Cortex A7 + 256MB DDR3 + NPU (this might be i6)
- [SSA520D](infinity5#ssa520d) - 64MB DDR2? BGA

#### [Infinity6](infinity6)

- Updated version of the infinity3.

- [SSC323](infinity6#ssc323) - probably Cortex A7 + 64MB DDR2 in a QFN88
- [SSC325](infinity6#ssc325) - Cortex A7 + 64MB DDR2 in a QFN88
- [SSC325DE](infinity6#ssc325de) - Cortex A7 + 128MB DDR3 in a QFN88
- [SSC326D](infinity6#ssc326d) - Cortex A7 + 128MB DDR3 + NPU
- [SSC327DE](infinity6#ssc327de) - Cortex A7 + 128MB DDR3

#### [Infinity6b0](infinity6)

- [SSC335DE](infinity6#ssc335) - probably Cortex A7 +  ?? + in a QFN88
- [SSC337DE](infinity6#ssc337) - probably Cortex A7 +  128MB DDR3 + in a QFN128
-- MC-F50: https://item.taobao.com/item.htm?id=619778901522&spm=1101.1101.N.N.e3dd64c

#### [Infinity 6e](infinity6)

- Infinity 6e seems to be a dual core variation in this family

- [SSC339G](infinity6#ssc339) - Dual Cortex A7

These seem to be i6e based on the build tag found in a kernel image for the SSC8629

- SSC8629D - AI enabled
- SSC8629G
  - 70mai A800S https://fccid.io/2AOK9-A800S/Internal-Photos/Internal-Photos-5061810
  - VIA M360-M800 https://fccid.io/NCI-M360-M800/
- SSC8629Q

### [Pioneer3](pioneer3)

This seems to be an evolution of the infinity2m chips.

- [SSD210](pioneer3#ssd210) - Dual Cortex A7 QFN68
- [SSD212](pioneer3#ssd212) - Dual Cortex A7 QFN128
- [SSC9212](pioneer3#ssc9212) - Dual Cortex A7? QFN68

### Mercury family

#### [Mercury2](mercury2)

- Dash camera SoC.

- [AIT8328/MSC8328](mercury2#msc8328) - Probably ARM9
- [AIT8428](mercury2#ait8428) - Probably ARM9

#### [Mercury5](mercury5)

- Dash camera SoC based on the infinity3.

- [SSC8336](mercury5#ssc8336) - Probably Cortex A7 + 64MB DDR2 in a QFP128
- [SSC8336N](mercury5#ssc8336n) - Cortex A7 + 64MB DDR2 in a 128 pin QFN
- [SSC8339D](mercury5#ssc8339d) - Probably in this family, Cortex A7 + 128MB(?) DDR3(?) in a 268 ball BGA

#### [Mercury6](mercury6)

- SSD268G - 2 * Cortex A53

### Misc

- [MSB2521](misc/msb2521.md) - ARM9 based SatNav on a chip
- MSB2531 - Cortex A7 SatNav on a chip
- [MSW8535N](misc/MSW8535N_Datasheet.pdf) - ARM9 based feature phone chip?
- SSC8668G
- SSC8539
- SSA520
- SSD203D - probably same die as the ssd201/ssd202d but with HDMI. Seems it was used in some TV dongles.
- SSD221 SSD9221 
  - https://web.archive.org/web/20210715144141/https://item.taobao.com/item.htm?spm=a230r.1.14.87.42b915f765wP7M&id=650844830905&ns=1&abbucket=18

# 64bit ARM based

According to the code that is in the wild and SigmaStars page there are some Cortex-A53 based chips.

- SSC8826D - 2 * Cortex A53, QFN
- SSC8826Q - 2 * Cortex A53, QFN
- SSC8836Q - Cortex A53, LQFP
- SSC8838G - Cortex A53, BGA
- SSC8526 - 2 * Cortex A53, BGA
- SSD261Q - 2 * Cortex A53
- SSR910Q - 2 * Cortex A53, LQFP
- SSR920G - 2 * Cortex A53, BGA

https://wemp.app/posts/1d5e4d06-dab5-408d-8349-7721957ca66e

# MediaTek chips that contain/have some MStar heritage

- MT53xx
- MSD6886

# Non-SoC chips

- SSW101B - Seems to be a wifi chip, maybe based on the same core as the XR819.
  - See [xradio](https://github.com/fifteenhex/xradio).
  - [Driver code](https://github.com/fifteenhex/sigmastar-ssw101b-driver)
  - [Maybe the same as this](https://www.altobeam.com/en/contents/72/6.html)
  - [Driver that looks really similar...](https://github.com/BPI-SINOVOIP/BPI-S905X3-Android9/tree/master/hardware/wifi/atbm/atbm602x)
  - Maybe the same chip as ATBM6032

# Injoinic PMICs

Injoinic seem to be the recommended PMIC vendor for these chips. Maybe like the Allwinner/Xpowers relationship?
- [Injoinic PMICs](injoinicpmics/index.md)

# Silan chips

Silan MEMs accelerometers seem to be used for a lot of the dash cam devices.

- [Silan chips](silan/)

# IP blocks

See [IP](ip).

# ISP/Debug Tool

See [ISP](isp).

# Blobs, headers, layouts

- [BootROM](blobs/bootrom.md) - Baked in BootROM
- [IPL](blobs/ipl.md) - First/Second stage bootloaders
- [MXPT](blobs/mxpt.md) - Partition table used for SPI NOR
- [CIS](blobs/cis.md) - "Chip information structure"? first block for SPI NAND.

# Vendor uboot, kernels..

- [Old 2015.01 based uboot from Taobao sourced SDK](https://github.com/fifteenhex/uboot_msc313e)
- [Old 3.18.30 based kernel from Taobao sourced SDK](https://github.com/fifteenhex/linux_msc313e)
- [Recent 4.9.84 based kernel](https://github.com/fifteenhex/linux-ssc325)

# Vendor SDKs

- [Mercury5](https://github.com/longyanjun2020/SDK_pulbic)
- [Probably Infinity2 NVR](https://github.com/ZYCX8888/Democode-TAKOYAKI-BETA001-0312)

## Sources of firmwares for reverse engineering

- [Anjvision firmwares](http://www.anjvision.com:8021/firmware/)

To get the device tree out of the kernel you can use binwalk + [extract-dtb](https://github.com/PabloCastellano/extract-dtb.git) and dtc.

```
binwalk -e <firmware.bin>
extract-dtb.py <extracted firmware dir><uncompressed kernel blob>
dtc -I dtb -O dts -o out.dts <extracted dtb that looks right>
```

# Dumping out registers from running vendor kernels

This works for dumping out a bank under wireless tag's openwrt:

```
BASE=0x1f206800; for X in `seq 0 127`; do A=$(($BASE + (4 * $X))); V=`devmem $A`; printf "0x%X - %s\n" $A $V; done
```


# Development boards

- [Breadbee](https://github.com/breadbee/breadbee/) (Infinity3 - msc313e)
- [70mai Midrive D08 a.k.a Dash Cam Lite](boards/dashcamlite.md) (Mercury5)

# Links

- [aiwinn](http://www.aiwinn.com/) - seems to supply a bunch of AI enabled things based on SigmaStar SoCs
- [comake.online](http://comake.online/) - Sigmastar's new open forum.
- [WhyCan SSD20X section](https://whycan.com/f_52.html)

## Buying chips

See [wheretobuy](wheretobuy.md)

