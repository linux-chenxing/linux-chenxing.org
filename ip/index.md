# IP blocks

## Interrupt controllers

## Clock

## Bus Glue

- MIU - memory interface unit
- RIU - register interface unit
- IMI - "internal memory interface"? interface for embedded SRAM

## Timers

## RTC

## DMA

### BDMA

BDMA or "Byte DMA" is a simple A -> B DMA engine. It's mainly used to
move data from the memory mapped SPI NOR into main memory so the CPU
doesn't have to do it.

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |

### CMDQ

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | wip   |
| infinity3 |        | wip   |

## Crypto

- AESDMA

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | wip   |
| infinity3 |        | wip   |


## Ethernet

- Cadence EMAC

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | yes    | yes   |
| infinity3 | yes    | yes   |

## USB

## ADC

### SAR

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |

## Serial

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | yes    | yes   |
| infinity3 | yes    | yes   |

## i2c

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |

## spi

## pwm

## spi-nor

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  | yes    | yes   |
| infinity3 | yes    | yes   |
| mercury5  | yes    |       |

## SD/SDIO

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
