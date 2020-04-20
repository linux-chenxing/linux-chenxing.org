# IP blocks

## Interrupt controllers

### IRQ intc

64 interrupts forwarded to the GIC

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### FIQ intc

32 interrupts forwarded to the GIC as FIQs

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### sleep intc

32 interrupts forwarded to the IRQ intc via a single interrupt

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

## Pinmux

### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | wip   |

## Clock

### pll gates

### clkgen muxes

These are 16 bit registers that contain clock muxes for one or more peripherals usually grouped, i.e. uart0 and uart1.

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### cpuclk

This (probably) a PLL that is used for dynamically scaling the CPU frequency.

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### LPLL 

Line/LCD PLL? Seems to be a PLL for generating the base clock for PNL.

## Bus Glue

### L3 Bridge/AXI interface

There is some fabric between the CPU, other bus masters and the memory.
Some magic bits in here are used to flush pending cpu writes to memory
so other bus masters can see them.

[Rough register descriptions](https://github.com/fifteenhex/SDK_pulbic/blob/master/Mercury5/proj/sc/driver/hal/mercury/kernel/inc/kernel_axi.h)

### MIU

MIU or "memory interface unit" is a multiport DDR controller that is wired to the CPU(s)
and DMA capable perpherials like USB, Ethernet and so on.

### RIU

RIU of "register interface unit" is a brige between the CPU and perpherial registers.
It's fairly straight forward for the most part with one annoying quirk; 32 bit registers
are split into two 16 bit locations that are spaced 4 bytes apart. This means that
any existing drivers that expect 32 bit registers aligned to 4 bytes needs to have a quirk
added to read the two 16 bit parts and stitch them back together.

### IMI

IMI or "internal memory interface"? interface for embedded SRAM. It seems to have multiple
ports so the CPU and some perpherials are able to access the SRAM but not a lot is known about
that yet.

## Timers

## RTC

### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

## DMA

### BDMA

BDMA or "Byte DMA" is a simple A -> B DMA engine. It's mainly used to
move data from the memory mapped SPI NOR into main memory so the CPU
doesn't have to do it. It also apparently supports doing CRC calculations.

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### CMDQ

CMDQ or "command queue" is a descriptor list based DMA engine that seems
to be intended to be used to tie the parts of the camera pipeline together
so that the CPU doesn't need to be involved.

Note: This seems to live in the "RIU" register address space and maybe can't see
the system memory.

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | wip   |
| infinity3 |        | wip   |

## Crypto

### AESDMA

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | wip   |
| infinity3 |        | wip   |


## Ethernet

### Cadence EMAC

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | yes    | yes   |
| infinity3 | yes    | yes   |

### GMAC

- infinity2m has something called a GMAC. Might be a Cadence GEM.

## USB

### UTMI

This is the USB PHY. It's probably a Faraday design to go with the Faraday EHCI host but this isn't confirmed.
This also supplies the clocks for the UHC and OTG so it's not safe to access them before enabling the clocks here first.

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### BC

This seems to be a way of presenting the right resistor values on the data lines to trigger chargers into supplying more current.

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        |       |
| infinity3 |        |       |
| mercury5  |        |       |

### USBC

This seems to be essentially a mux that sits between the UTMI and the UHC and OTG blocks so that UTMI can be connected to the right block for the current role the port is in.

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### UHC

This is a usb host controller that seems to be based on a Faraday design. It's a broken-EHCI controller.

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### OTG

This seems to be an musb USB device controller.

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | wip   |
| infinity3 |        | wip   |
| mercury5  |        | wip   |

## ADC

### SAR

This seems to be a fairly standard ADC. Channel 7 is an on-die [temp sensor](https://github.com/fifteenhex/linux-ssc325/blob/89341c7012404c72e192f198b2ea6405ec80d15d/drivers/sstar/cpufreq/infinity3-cpufreq.c#L222).

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

## Serial

Serial seems to be a standard Designware UART with one of the registers in a different location.

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | yes    | yes   |
| infinity3 | yes    | yes   |
| mercury5  | yes    | yes   |

## i2c

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

[Rough register descriptions](https://github.com/fifteenhex/linux_mstar_3.18/blob/e424e92e5442490e2f19b6d18464be3730e0678c/drivers/mstar/i2c/infinity/mhal_iic_reg.h#L208)

## spi

## pwm

## spi-nor

spi-nor functionality is made of 3 different IP blocks; ISP, FSP and QSP.
These are all basically slightly different SPI masters.

- ISP is the simplest and seems to be for doing basic SPI transactions
- FSP allows for parts of an SPI transaction come from registers, like the opcode and address, while
  other parts are read direcly from memory. This seems to be for doing fast zero copy writes.
- QSP seems to implement the memory mapped interface that allows the CPU and BDMA to read from flash
  as if it was memory.

### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | yes    | yes   |
| infinity3 | yes    | yes   |
| mercury5  | yes    | yes   |

## SD/SDIO

There seem to be many versions or revions of the SD/SDIO block. Some versions seem to also support memory stick etc.

### *v5* as seen in i3 and m5

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

## Display pipeline

This display pipeline(s) are made up of a bunch of different blocks that can be changed/mixed together and then thrown out of an output. The vendor code for this area is a complete mess so it's going to be very hard to work out how to use any of it.

For a mipi display on the m5 the pipeline seems to look like this:

```
 -----      ----------      ------
| PNL | -> | MIPI DSI | -> | DPHY |
 -----      ----------      ------
```


### MIPI DSI

Seems to be the same as the [mediatek one](https://github.com/torvalds/linux/blob/master/drivers/gpu/drm/mediatek/mtk_dsi.c) based on [this header](https://github.com/fifteenhex/linux_mstar_3.18/blob/another_codedrop/drivers/mstar/driver/hal/infinity2/mipi_dsi/inc/reg_mipi_dsi.h).

### GOP

"Graphics Output Path". This is a simple framebuffer that uses a chunk of system memory.

### PNL

PaNeL? Seems to be incharge of driving LCDs either via a parallel interface or MIPI.

## Camera

The pipeline for the m5 seems to look like this:

```
          
 -------         -----      ------
|  VIF  | <-X-- | CSI | <- | DPHY |
 -------    |    -----      ------
            |    -------
             \- | BT656 |
                 -------
```

There seems to be 3 "vif" blocks. Then two csi blocks and two dphys. The sr0 dphy seems to only support two lanes. The sr1 dphy supports 4.

### VIF

vif, video interface?, seems to also be called "sensor" seems to be the sink for the video after it's come from mipi or somewhere else.

[Rough register descriptions](https://github.com/fifteenhex/SDK_pulbic/blob/master/Mercury5/proj/sc/driver/hal/mercury/isp/inc/mercury5_reg_vif.h)

### ISP

This is the main camera sensor interface block. It can either take input from a parallel sensor or from the CSI and in turn a MIPI CSI sensor.

### CSI

This is a frontend for the ISP that allows it to interface with a MIPI CSI sensor.

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | n/a    | wip   |
| infinity3 | n/a    | wip   |
| mercury5  | n/a    | wip   |

## Video Encoder/Decoder

### MFE

"Multi-Format Encoder".

- Infinity1 is apparently "mfe5"
- Infinity3 is apparently "mfe6"
 
[Rough register descriptions](https://github.com/fifteenhex/SDK_pulbic/blob/master/Mercury5/proj/sc/driver/hal/mercury/mfe/inc/hal_mfe_reg.h)
 
### VFE 

- Infinity1 is apparently "h2v1"
- Infinity3 is apparently "h2v3"

### JPE

Hardware JPEG encoder

[Rough register descriptions](https://github.com/fifteenhex/SDK_pulbic/blob/master/Mercury5/proj/sc/driver/hal/mercury/jpe/pub/hal_jpe_reg.h)

## Audio

### BACH

BACH is a fairly generic DMA engine with a DAC attached audio block.

[Reverse engineering](bach.md)

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | n/a    | wip   |
| infinity3 | n/a    | wip   |
| mercury5  | n/a    | wip   |

## Misc

### Mailbox

### AI/NN

Some chips seem to contain a [CEVA XM6](https://www.ceva-dsp.com/product/ceva-xm6/).
