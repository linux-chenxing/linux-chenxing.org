# AEON

AEON (or "RISC32", "R2", "AEONR2", "BEON"?) is a 32-bit CPU architecture that is in fact, a Little-endian version of [OpenRISC](or1k.md)
with different instruction coding (fixed 32-bit ones in or1k vs variable 24/32-bit ones),
as well with any archetictural changes caused by that, and some custom instructions for caches, etc.

It could be seen as the housekeeping (i.e. main) CPU in families such as **Macaw12**, **Music**, **Nasa**, etc.

Also in some families it acts as an coprocessor in the MHEG5/VD_MHEG5 blocks,
and it seems to be used as an additional DSP in the audio subsystem (seems to be called "R2" there).

There is an second revison (apparently called "R2"/"AEONR2"), that **lacks** the branch delay slots
(as in the assembly sources the branches are guarded with #ifdefs that changes the instruction order
from branch->something to something->branch, implying that the delay slots were removed).

This arch was most likely developed to replace the 8-bit [8051](8051.md) MCU, to a more featured 32-bit CPU,
thus making possible to run directly from DRAM, instead of fetching the code from the SPI flash (this only happens at bootup),
have direct access to DRAM, thus also having a lot more of code/data space, etc.
while 8051-based ones were limited to 256 bytes IDATA and 1k XDATA SRAMs, 64k banked code space and 
4k/64k windowed accesses to the DRAM through XDMIU.

## Memory map

- `0x00000000` - MIU (or also SPI flash)
- `0x90000000` - Local UART
- `0xA0000000` - RIU
- `0xB0000000` - SRAM (4k of it?)
- `0xC0000000` - SRAM (the Titania2 variant or the pre-Titania3 one?)

### MIU/SPI flash

Same as in OpenRISC, the exception vectors are fixed at memory address 0x00000000.

#### Housekeeping deal

For a housekeeper it is important because you are the only one who runs now (a scenario when the PM51 runs **earlier** is not counted),
and so the SPI flash is mapped in by default.

And since the MIU and SPI flash mappings should start at the same address (to have the reset vector point to a valid startup code, and to be able to handle exceptions&interrupts in a app),
to copy data from the SPI flash the [BDMA](/ip/bdma.md) should be used as the MIU is totally inaccessible when the SPI flash is mapped there.

The switch from SPI flash into the MIU is done by [configuring some regs](https://github.com/neuschaefer/mstar-mboot/blob/962e8b8258378dded694883a9f9acb7058d34631/sboot/src/macaw12/bootaeonsysinit.c#L155)
and then resetting the CPU so that it now boots into the MIU map instead. And so during the switch, the icache is needed because otherwise
the instructions to switch and reset will be (of course) lost.

**Wait, the reg1002B4 sets some "reset vector base", does it also affect other vectors as well and so my assumpions are wrong??
But at least, the fact about the impossibility to write MIU by CPU while being in SPI flash map might be true...**

#### Coprocessor deal

The coprocessors of course does not need to care about that because the code is already loaded by something else in right places.

### Local UART

There is an "tigthly coupled" 8250 UART that is mapped with one byte per register (i.e. `reg-shift = <0>'`).

Basically this might be a convention from the 8051 MCU as it is not only the CPU itself,
but also the additional peripherals it has (e.g. Timers, GPIO, UART, etc.)

Nevertheless, this is convenient for the coprocessors as in this case to output something into UART you can use
local UART interface rather than using the "generic"/"shared" UARTs in the RIU.

### RIU

There is nothing special for it compared to other SoCs (MIPS/ARM ones, of course),
it's the same insanity where the 16-bit RIU word is mapped in a 32-bit word.

### SRAM

It seems that SRAM could be [mapped to arbitrary location?](https://github.com/neuschaefer/mstar-mboot/blob/962e8b8258378dded694883a9f9acb7058d34631/sboot/src/macaw12/reset.S#L100)

## Interrupt map

The local interrupt controller is of course, the OpenRISC one (guess why).

- 2 => Non-PM intc FIQ (Host 2)
- 3 => Non-PM intc IRQ (Host 2)
- 19 => Local UART

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
