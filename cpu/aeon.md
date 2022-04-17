# AEON

AEON (or "RISC32", "R2", "AEONR2", "BEON"?) is acutally an Little-endian version of the [OpenRISC](cpu/or1k.md) arch
that also has the fixed 32-bit instructions replaced to the variable 16/24-bit ones.
(as well as any possible archeticurical change that was made because of this new instruction format)

It is used as an main ("HouseKeeping"?) CPU in families such as **Macaw12** (TSUMV59...), **Music**, **Nasa**, etc.

Also in families such as **Titania4** it is used as a coprocessor core (where in Chakra it is in charge of playing video and decoding pictures).

This arch also has an second revision ("R2") that apparenly has an branch delay slot (an optional feature in or1k),
and seem to have some other changes related to caches, etc.

However it is unknown whether it has the MMU implemented.
Maybe it's not because the only thing this arch officialy has is firmwares without any kind of OS ("Non-OS" in mstar vocab),
and it might be becuase MStar intended to use the [MIPS](cpu/mips.md)/[ARM](cpu/arm.md) cores
for possible running of some OSes like Linux or an RTOS like eCos/etc.

Do you know the effort that needs to be put to port Linux to it?
You need to have gcc, libc, and all other stuff so that it does make more sense to use already supported arches instead.
Also the average clock speed of 216 MHz might tell something...

**Maybe actually AEON did came in after 8051 SoCs instead, and then MIPS came in
when they did want to run more complex stuff e.g. Linux on their SoCs?
And the switch 8051->AEON was made because the Digital TV came in, and so
managing all of that under full featured 32-bit arch was more pleasant?**

## Memory map

-  `0x00000000` - MIU (or also SPI flash)
-  `0x90000000` - UART
-  `0xA0000000` - RIU
-  `0xB0000000` - SRAM (4k of it?)
-  `0xC0000000` - SRAM (the Titania2 variant or the pre-Titania3 one?)

Because of the roots of this arch, the MIU and SPI flash needs to start from the same address
since the vector addresses are fixed, and is starting from the beginning of the address space.
And so, when the secondary part of sboot needs to be loaded, it is done through [BDMA](ip/bdma.md)
because maybe it's not possible to write into the SPI flash map, where the write is directed to the MIU instead.

And the switch from SPI flash into the MIU is done by [configuring some regs](https://github.com/neuschaefer/mstar-mboot/blob/962e8b8258378dded694883a9f9acb7058d34631/sboot/src/macaw12/bootaeonsysinit.c#L155)
and then resetting the CPU so that it now boots into the MIU map instead. And so during the switch, the icache is needed because otherwise
the instructions to switch and reset will be (of course) lost.

**Wait, the reg1002B4 sets some "reset vector base", does it also affect other vectors as well and so my assumpions are wrong??
But at least, the fact about the impossibility to write MIU by CPU while being in SPI flash map might be true...**

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

====== TODO ======
