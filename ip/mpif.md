# MPIF

MPIF (Mstar/Master Parallel InterFace?) is primarily a controller for some MStar's special parallel bus,
whose controller (which is described there) also supports the SPI protocol.

It can transfer data either through local 16-byte buffer or through DMA (up to 65535 bytes per single transfer).

SPI transfers can be prefixed with a "command" bytes (up to 4 bytes), and the transfer itself is half duplex.
And there seem to be no way to hold CS low on the end of the transaction!

Also note that when DMA writes into memory, when the transfer length is not aligned to 8 byte boundary,
the remaining bytes is written with 0x00. (i.e. the dma buffer length needs to be aligned).

The bus clock is the incoming module clock divided by 2, e.g. ~62 MHz for ~123 MHz or 13.5 MHz for 27 MHz.

## Registers

```
reg00: MPIF channel 1A control
    b0 = start transfer
    b1 = access type [0: read, 1: write]
    b2~b3 = slave select
    b4~b6 = index
    b8~b15 = data

reg02: MPIF channel 2A control
    b0 = start transfer
    b1 = access type [0: read, 1: write]
    b2~b3 = slave select
    b4 = checksum enable
    b6~b7 = read/write attempt count

reg04:
    b0~b15 = MPIF channel 2A access address

reg06:
    b0~b15 = MPIF channel 2A data

reg08: MPIF channel 2B control
    b0 = start transfer
    b1 = access type [0: read, 1: write]
    b2~b3 = slave select
    b4 = checksum enable
    b6~b7 = read/write attempt count

reg0A:
    b0~b15 = MPIF channel 2B access address

reg0C:
    b0~b15 = MPIF channel 2B data

reg0E: MPIF channel 3A control
    b0 = start transfer
    b1 = access type [0: read, 1: write]
    b2~b3 = slave select
    b4 = checksum enable
    b5 = 
    b6~b7 = 
    b8 = DMA enable
    b10 = 
    b11 = 
    b12~b15 = 

reg10:
    b0~b15 = MPIF channel 3A transfer length (in 16 byte units)

reg12:
reg14:
reg16:
reg18:
reg1A:
reg1C:
reg1E:
reg20:
    MPIF channel 2A/2B/3A data buffer (16 bytes)

reg22:
    b0~b23 = MPIF channel 3A DMA MIU address [3..26]

reg26:
    b0 = start transfer
    b1 = access type [0: read, 1: write]
    b2~b3 = slave select
    b4 = checksum enable
    b5 = 
    b6~b7 = 
    b8 = DMA enable
    b10 = 
    b11 = 
    b12~b15 = 

reg28:
    b0~b15 = MPIF channel 3B transfer length (in 16 byte units)

reg2A:
reg2C:
reg2E:
reg30:
reg32:
reg34:
reg36:
reg38:
    MPIF channel 3B / SPI data buffer (16 bytes)
reg3A:
    b0~b23 = MPIF channel 3B DMA MIU address [3..26]

reg3E: MPIF channel 4A control
    b0 = start transfer
    b1 = access type [0: read, 1: write]
    b2~b3 = slave select
    b6~b7 = 
    b8 = 
    b9 = 
    b10~b11 = 
    b12~b15 = 

reg40:
    b0~b15 = MPIF channel 4A transfer length

reg42:
    b0~b23 = MPIF channel 4A DMA MIU address [3..26]

reg46: SPI control
    b0 = start transfer
    b1 = direction [0: receive, 1: send]

reg4A: SPI config
    b0~b1 = slave select
    b2 = clock phase (CPHA)
    b3 = clock polarity (CPOL)
    b4~b5 = leading cycle count
    b6~b7 = trailing cycle count
    b8~b10 = command data length (in bytes?)
    b11 = DMA enable
    b12 = DMA MIU select?

reg4C:
reg4E:
    SPI command data (4 bytes)

reg50:
    b0~b15 = SPI transfer length

reg52:
    b0~b25 = SPI DMA MIU address [3..28]

reg56: busy status
    b0 = SPI busy
    b2 = MPIF channel 1A busy
    b3 = MPIF channel 2A busy
    b4 = MPIF channel 2B busy
    b5 = MPIF channel 3A busy
    b6 = MPIF channel 3B busy
    b7 = MPIF channel 4A busy

reg58: interrupt mask?
    ...

reg5A: interrupt status
    b0 = SPI transfer done
    b2 = MPIF channel 1A transfer done
    b3 = MPIF channel 2A transfer done
    b4 = MPIF channel 2B transfer done
    b5 = MPIF channel 3A transfer done
    b6 = MPIF channel 3B transfer done
    b7 = MPIF channel 4A transfer done
    b8 = MPIF channel 2A transfer error
    b9 = MPIF channel 2B transfer error
    b10 = MPIF channel 3A transfer error
    b11 = MPIF channel 3B transfer error
    b12 = MPIF channel 4A transfer error
    b13 = Error

reg60:
    b0 = soft reset (clear then set)
    b2~b3 = MPIF channel 1A/2A/2B turnaround cycle count [0..1]
    b4~b5 = MPIF ACK/NAK wait cycle count
    b6~b7 = MPIF slave 0 data width:
    b8~b9 = MPIF slave 1 data width:
    b10~b11 = MPIF slave 2 data width:
    b12~b13 = MPIF slave 3 data width:
    b14~b15 = MPIF command data width:
      0 => 1 bit
      1 => 2 bits
      2 => 4 bits
      3 => 8 bits

reg62:
    b0~b2 = MPIF channel 3A/3B/4A turnaround cycle count
    b3 = MPIF channel 1A/2A/2B turnaround cycle count [2]

reg6A:
    b2~b3 = ?? set to 3
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
