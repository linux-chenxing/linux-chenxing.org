# MPIF

MPIF (Mstar/Master Parallel InterFace?) is primarily a controller for some MStar's special parallel bus,
whose controller (which is described there) also supports the SPI protocol.

It can transfer data either through local 16-byte buffer or through DMA (up to 65536 bytes per single transfer).

Note that when DMA writes into memory, when the transfer length is not aligned to 8 byte boundary, the remaining bytes is written with 0x00. (i.e. the dma buffer length needs to be aligned) -- maybe related with the MIU dummy write thing?

The controller supports 3 wire SPI (CSxZ, CLK and bidirectional MOSI), and 4 wire SPI (CSxZ, CLK, MOSI and MISO) with full duplex support (when not in DMA mode).

The bus clock is the incoming module clock divided by 2, e.g. ~62 MHz for ~123 MHz or 13.5 MHz for 27 MHz.

## Registers

```
...

reg2A-39:
    MPIF channel 3B / SPI data buffer (16 bytes)

...

reg46: SPI (4 wire) control
    b0 = start transfer
    b1 = direction [0: receive, 1: transmit]
    b2 = enable full duplex (when direction is receive and DMA is disabled)

reg48: SPI (3 wire) control
    b0 = start transfer
    b1 = direction [0: receive, 1: transmit]

reg4A: SPI config
    b0~b1 = slave select
    b2 = clock phase (CPHA)
    b3 = clock polarity (CPOL)
    b4~b5 = leading cycle count
    b6~b7 = trailing cycle count
    b8~b10 = command data length (in bytes)
    b11 = DMA enable
    b12 = "miu path selection"
    b13 = "separate io mode"
    b14 = "not wait miu mode"

reg4C-4F:
    SPI command data (4 bytes)

reg50:
    b0~b15 = SPI transfer length (0 == 65536)

reg52-55:
    b0~b25 = SPI DMA MIU address [3..28]

reg56: busy status
    b0 = SPI (4 wire) busy
    b1 = SPI (3 wire) busy
    b2 = MPIF ch 1A busy
    b3 = MPIF ch 2A busy
    b4 = MPIF ch 2B busy
    b5 = MPIF ch 3A busy
    b6 = MPIF ch 3B busy
    b7 = MPIF ch 4A busy

reg58: interrupt enable
    << below >>

reg5A: interrupt status (write 1 to clear)
    b0 = SPI (4 wire) transfer done
    b1 = SPI (3 wire) transfer done
    b2 = MPIF ch 1A transfer done
    b3 = MPIF ch 2A transfer done
    b4 = MPIF ch 2B transfer done
    b5 = MPIF ch 3A transfer done
    b6 = MPIF ch 3B transfer done
    b7 = MPIF ch 4A transfer done
    b8 = MPIF ch 2A transfer error
    b9 = MPIF ch 2B transfer error
    b10 = MPIF ch 3A transfer error
    b11 = MPIF ch 3B transfer error
    b12 = MPIF ch 4A transfer error
    b13 = MPIF busy timeout
    b14 = "slave request"

...

reg60:
    b0 = software reset (active low)

...

reg68:
    b0~b15 = SPI tx/rx incomplete data length

reg6A:
    b0 = MIU write request mask
    b1 = Clear MIU write out of range status
    b2 = MIU dummy write enable
    b3 = MIU dummy write length (0: 2, 1: 4)
    b8 = MIU write out of range status

reg6C-6F:
    b0~b25 = MIU write address lower range [3..28]

reg70-73:
    b0~b25 = MIU write address upper range [3..28]

reg74:
    b0~b3 = data pins GPO enable
    b4~b7 = data pins GPO value
    b8~b11 = CS pins GPO enable <n/a>
    b12~b15 = CS pins GPO value <n/a>

...

reg7C-7F:
    spare regs
```

---

All regs filled to 0xffff:

```
>>> for i in range(0,0x100,2): riu.write16(0x110400+i, 0xffff)
... 
>>> riu.dump(0x110400)
110400: 7E 12 DE 00 FF FF 29 D0 DF 00 FF FF AD AC FF FF |~.....).........|
110410: FF FF 18 3C 26 23 48 98 D2 14 93 CD 62 FB 67 A1 |...<&#H.....b.g.|
110420: 95 1C FF FF FF 03 FF FF FF FF FF FF FF FF FF FF |................|
110430: FF FF FF FF FF FF FF FF FF FF FF FF FF 03 CF FF |................|
110440: FF FF FF FF FF 03 06 00 02 00 FF 7F FF FF FF FF |................|
110450: FF FF FF FF FF 03 F3 00 FF 7F 04 20 FF FF 05 03 |........... ....|
110460: FF FF 0F F7 FF FF 07 FF 00 00 0F 00 FF FF FF 03 |................|
110470: FF FF FF 03 FF 00 33 00 00 00 00 00 FF FF FF FF |......3.........|
110480: 07 00 DC 35 0E 0D AE FC 0F 00 00 00 00 00 00 00 |...5............|
110490: 00 00 00 00 00 00 01 00 01 00 07 00 00 00 00 00 |................|
1104a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
```

All regs filled to 0x0000:

```
>>> for i in range(0,0x100,2): riu.write16(0x110400+i, 0x0000)
... 
>>> riu.dump(0x110400)
110400: 00 12 00 00 00 00 29 D0 00 00 00 00 AD AC 00 00 |......).........|
110410: 00 00 18 3C 26 23 48 98 D2 14 93 CD 62 FB 67 A1 |...<&#H.....b.g.|
110420: 95 1C 00 00 00 00 00 00 00 00 FF FF FF FF FF FF |................|
110430: FF FF FF FF FF FF FF FF FF FF 00 00 00 00 00 00 |................|
110440: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
110450: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 05 03 |................|
110460: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
110470: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
110480: 00 00 DC 35 0E 0D 2E FC 0F 00 00 00 00 00 00 00 |...5............|
110490: 00 00 00 00 00 00 01 00 00 00 00 00 00 00 00 00 |................|
1104a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................|
1104f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 |................| 
```
