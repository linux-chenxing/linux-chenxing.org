# BDMA

BDMA is a generic DMA that transfers from one memory location to another.
It can also calculate CRC32 with configurable polynomial and shift register initial state.

## Registers

```
reg00: control
    b0 = start
    b4 = stop

reg02: status
    b0 = queued
    b1 = busy
    b2 = int
    b3 = done
    b4 = res0
    b14 = ?

reg04: source control
    b0~b3 = src:
      0=MIU
      1=IMI?
      4=Fill?
      5=QSPI (higher width is faster)
    b4~b6 = src width:
      0=1 byte
      1=2 bytes
      2=4 bytes
      3=8 bytes
      4=16 bytes?

reg05: dest control
    b0~b3 = dest:
      0=MIU (width should be at least 8 bytes)
      3=CRC (width should be 1 byte)
      B=FSP?
    b4~b6 = dest width:
      0=1 byte
      1=2 bytes
      2=4 bytes
      3=8 bytes
      4=16 bytes?

reg06: misc ctrl
    b0 = direction (0:addr increment, 1:addr decrement) -- affects both source and dest
    b1 = int enable
    b4~b11 = ?

reg08: source address
    b0~b31 = src addr

reg0C: dest address
    b0~b31 = dst addr

reg10: transfer length
    b0~b31 = length

reg14: crc polynomial
    b0~b31 = crc polynom

reg18: crc shift register
    b0~b31 = crc shift reg

```

----
```
/*
 * MStar BDMA controller - B seems to be for byte
 *
 * This is a simple dma controller for transferring blocks from
 * a to b. The only special thing about it seems to be that it
 * can also do CRC32 calculations.
 *
 *
 * 0x0 - ctrl
 * vendor sdk says "set source and destination path" for this
 *
 * 9       | 8        | 7 - 5 | 4    | 3 - 1 | 0
 * dst_tlb | src_tlb? |       | stop |       | trigger
 *
 * writing 0xffff results in 0x310
 *
 * writing 0x11 allows writing 0 to clear trigger
 *
 * 0x4 - status
 * 14 | 7 | 6 | 5 | 4            |  3   |  2  |  1   |   0    |
 *  ? | ? | ? |   | result0(err) | done | int | busy | queued |
 *
 * 2 - 4 -- seem to status flags
 * 0 - 1 -- seem to busy indicators
 *
 * 0x8  - src, dst, width
 *      14 - 12   |   11 - 8  |     6 - 4      | 3 - 0
 *    dst width   |    dst    |   src width    |  src
 *
 * src/dst ids for infinity3
 *
 *      | src                 | dst         |
 * 0x0  | MIU - 16 bytes wide | same as src |
 * 0x1  | IMI?                |             |
 * 0x4  | Fill? - 4           |             |
 * 0x5  | QSPI - 8 bytes wide |             |
 * 0xB  |                     | FSP?        |
 *
 * width
 * 0x0 - 1 byte
 * 0x1 - 2 bytes
 * 0x2 - 4 bytes
 * 0x3 - 8 bytes
 * 0x4 - 16 bytes
 *
 * 0xc - misc
 * 16 - 5 |    1    | 0
 *        | int_en  | direction
 *    ?   |         | 0 - increment address
 *        |         | 1 - decrement address
 *
 * 4 - 7  - probably configuration for the CRC32 mode
 * 8 - 11 - might be dmywrcnt
 *
 * 0x10 - start address low
 * 0x14 - start address high
 * 0x18 - end address low
 * 0x1c - end address high
 * 0x20 - size low
 * 0x24 - size high
 *
 * -- spotted in another mstar bdma driver, might not exist but are writable--
 * 0x28 - cmd
 * 0x2c - " "
 * 0x30 - " "
 * 0x34 - " "
 *
 * -- writable
 *
 * 0x38
 * 0x3c
 */
 ```
