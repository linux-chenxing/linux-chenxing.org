# MCU32

The MCU32 / 32BIT_MCU (also called MHEG5 / VD_MHEG5 respectively) blocks are used to control
the underlying CPU (usually the [OpenRISC](../cpu/or1k.md) one)
and control some aspects of their integraion with the rest of the system.

The MCU32 / MHEG5 is also referred to as "[AEON](../cpu/aeon.md)".

This block allows to:
 - Control the CPU reset and enable the CPU itself.
 - Write-protect up to two areas in MIU (by a means of a mask-address comparsion)
 - Control where the QMEM (a tiny SRAM), RIU/REG32 bus and SPI flash are mapped to.
 - Control the endiannes swap for instruction and data bus bridges.
 - Force the code execution from MIU or SPI flash (forcing to access those on the instruction bus)

## Registers

This block usually can be seen at these RIU addresses:
 - 0x100300 → 32BIT_MCU / VD_MHEG5
 - 0x100F00 → MCU32 / MHEG5

```
reg80:
    b0 = "NCDRAMPOSTW" - NC write DRAM post write and merge
    b1 = "IOWINORDER" - Writes to IO/MIU are in-order
    b4 = "WRPROTEN" - Write protection region enable

reg92:
    ??

*
*  If the address masked by DRAMx_MASK matches DRAMx_BASE,
*  the write will be ignored in case WRPROTEN is set.
* - i.e.  write_enable = wr & !(WRPROTEN && ((addr & DRAMx_MASK) == DRAMx_BASE))
*
* The comparsion is done with the upper 16 bits of the address (i.e. bits 16-31)
*
regC0-C1:
    b0~b15 = DRAM1_BASE
regC2-C3:
    b0~b15 = DRAM1_MASK
regC4-C5:
    b0~b15 = DRAM2_BASE
regC6-C7:
    b0~b15 = DRAM2_MASK

*
* All relating to the mapping of the MIU into the instruction bus.
* No idea why it's all scattered around..
*
regE2-E3:
    b8~b15 = Code Memory MIU base address [27:20]
regE4-E5:
    b0~b15 = Code Memory MIU base address [19:4]
regE6-E7:
    b0 = <cleared>
    b1 = <set>
    b2 = <set>
    b8~b9 = Code Memory MIU base address [29:28]

*
* When (addr & QMEM_DMASK) == QMEM_DADDR evaluates to true,
* the QMEM is going to be accessed on the data bus.
*
* The QMEM is 4 KiB long on AEON and is 8 KiB long on VPU.
*
regE8-EB:
    b0~b31 = QMEM_DMASK
regEC-EF:
    b0~b31 = QMEM_DADDR


regF0:
    b0 = Enable the CPU
    b1 = Software reset (0 = assert)
    b2 = Instruction bus bridge endian swap
    b3 = Data bus bridge endian swap           (doesn't seem to work?)
    b4 = MIU read priority
    b5 = MIU write priority
    b6 = Force instruction access from SPI flash
    b7 = Force instruction access from MIU

regF2-F3:
    b0~b15 = DBG_SEL
    * setting b8~b15 to 0xDB enables debug, apparently.

*
* Offset within MIU to the start of the area seen by the CPU
*  in the units of the MIU words (which are usually 8 bytes long)
* Note that this is for the MIU mapping on the data bus, for the instruction
*  bus mapping refer to regE2-E7 above.
*
regF4-F7:
    b0~b31 = SDR_BASE   (MIU address [:3])

*
* Base address of the register bus, bits [31:16]
* In case of the VPU, that's some VPU specific bus, otherwise it's an ordinary RIU bus.
*
regF8-F9:
    b0~b15 = REG32_BASE

regFA-FD:
    b0~b31 = SDR_MAP

*
* Base address of the SPI flash mapping, bits [31:16]
*
*  On AEON only the top 8 bits (i.e. address bits [31:24]) are effective,
*   while VPU indeed can only access the first 64 KiB of SPI flash.
*
regFE-FF:
    b0~b15 = SPI_BASE
```
