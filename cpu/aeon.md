# AEON

AEON (or "RISC32", "R2", "AEONR2", "BEON"?) is acutally an Little-endian version of the [OpenRISC](or1k.md) arch
that also has the fixed 32-bit instructions replaced to the variable 24/32-bit ones (as well as the instruction encoding being changed)

It is used as an main ("HouseKeeping"?) CPU in families such as **Macaw12** (TSUMV59...), **Music**, **Nasa**, etc.

Also in families such as **Titania4** it is used as a coprocessor core (where in Chakra it is in charge of playing video and decoding pictures).

This arch also has an second revision ("R2") that apparenly has an branch delay slot (an optional feature in or1k),
and seem to have some other changes related to caches, etc.

So far it seems like that this arch was developed when MStar had 8051-based SoCs, since this arch has seen only "Non-OS" firmwares,
and anyway if you want to run Linux on your SoCs,
then it makes sense to use "mainstream" arches like [MIPS](mips.md) or [ARM](arm.md), althrough they need to be licensed.
But they save you from also caring about adding support to Linux, libc, and whatever other stuff that needs to make Linux systems go. 

## Memory map

-  `0x00000000` - MIU (or also SPI flash)
-  `0x90000000` - UART
-  `0xA0000000` - RIU
-  `0xB0000000` - SRAM (4k of it?)
-  `0xC0000000` - SRAM (the Titania2 variant or the pre-Titania3 one?)

Because of the roots of this arch, the MIU and SPI flash needs to start from the same address
since the vector addresses are fixed, and is starting from the beginning of the address space.
And so, when the secondary part of sboot needs to be loaded, it is done through [BDMA](/ip/bdma.md)
because maybe it's not possible to write into the SPI flash map, where the write is directed to the MIU instead.

And the switch from SPI flash into the MIU is done by [configuring some regs](https://github.com/neuschaefer/mstar-mboot/blob/962e8b8258378dded694883a9f9acb7058d34631/sboot/src/macaw12/bootaeonsysinit.c#L155)
and then resetting the CPU so that it now boots into the MIU map instead. And so during the switch, the icache is needed because otherwise
the instructions to switch and reset will be (of course) lost.

**Wait, the reg1002B4 sets some "reset vector base", does it also affect other vectors as well and so my assumpions are wrong??
But at least, the fact about the impossibility to write MIU by CPU while being in SPI flash map might be true...**

It also seems that SRAM could be [mapped to arbitrary location?](https://github.com/neuschaefer/mstar-mboot/blob/962e8b8258378dded694883a9f9acb7058d34631/sboot/src/macaw12/reset.S#L100)

The coprocessor of course doesn't need to do all of that because how it is going to be mapped is decided by other CPU. (because it's a coprocessor!)

The RIU is mapped in same insane way as everywhere (i.e. one 32-bit word only contains 16 bits of RIU).

## Interrupt map

Since or1k has an PIC, AEON has it too.

-  IRQ#2 => Non-PM intc FIQ
-  IRQ#3 => Non-PM intc IRQ
-  IRQ#19 => UART

## UART

The AEON also has its own UART (which is 8250/16550-compatible).
It is mapped in with one byte per register (i.e. `reg-shift = <0>;`)

Don't know whether it exists in SoCs with the AEON working as HK, but the coprocessor does have it because it has to write something into UART,
and so to not put all of that into the main PIU UART, it does that into its own UART instead.

It is possible to connect the UART pads into the AEON's UART by configuring the UART mux.

## Arch details

### Instructions

Conventions:
-  The bits specified there are stored in big endian, and the first bit is the MSB
   -  i.e. `11001000101001100100011101110111` is `C8 A6 47 77`.
-  The caps letter denotes the MSB, then any following or preceding letter is bit that goes down to LSB.
-  Bit letters follow the OpenRISC specs at least where it's possible

**For details on instructions refer to the OpenRISC specs, unless otherwise specified.**

```

000000000000000000000000                l.nop
000010DddddAaaaa00000001                l.lhz                 rD, 0(rA)
000011BbbbbAaaaa00000000                l.sw                  0(rA), rB
000111DddddAaaaaKkkkkkkk                l.addi                rD, rA, K
00100000Nnnnnnnnnnnnnnnn                l.bf                  N
001101100000000000000001                l.movhi               r1, ???
010001DddddAaaaaBbbbb100                l.and                 rD, rA, rB
010100AaaaaBbbbbKkkkkkkk                l.ori                 rA, rB, K
010111AaaaaIiiii00000001                l.sfeqi               rA, I
010111AaaaaBbbbb00001101                l.sfne                rA, rB
010111BbbbbAaaaa00010111                l.sfgeu               rA, rB
100100Nnnnnnnnnnnnnnnnnn                l.j                   N

... TODO ...

110000DddddKkkkkkkkkkkkkkkkk0001        l.movhi               rD, K
110000BbbbbAaaaaKkkkkkkkkkkk1101        l.mtspr               rA, rB, K
110000DddddAaaaaKkkkkkkkkkkk1111        l.mfspr               rD, rA, K
110001DddddAaaaaKkkkkkkkkkkkkkkk        l.andi                rD, rA, K
110010DddddAaaaaKkkkkkkkkkkkkkkk        l.ori                 rD, rA, K
111010Nnnnnnnnnnnnnnnnnnnnnnnnnn        l.j                   N
111011BbbbbAaaaaIiiiiiiiiiiiiiii        l.sw                  I(rA), rB
11110100000Aaaaa00000000000J0001        l.invalidate_line     0(rA), J    ***1
111111DddddAaaaaKkkkkkkkkkkkkkkk        l.addi                rA, rB, K

... TODO ...

***1: Not in OpenRISC spec?

```
