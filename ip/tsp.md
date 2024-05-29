# TSP

Transport Stream Processor
houses an [OpenRISC](../cpu/or1k.md) CPU.

## Registers

```

*
* Access to the internal register space:
*
reg90-91: IDR_CTRL
    b0 = Start!
    b1 = Access type (0 = read / 1 = write)
    b5 = ?? MCU Wait
reg92-95: IDR_ADDR
    b0~b31 = Access address
reg96-99: IDR_WRITE
    b0~b31 = Data to write
reg9A-9D: IDR_READ
    b0~b31 = Read data

*
* Offset within MIU that's going to be visible by the internal CPU.
*
regC0-C3: CPU_BASE
    b0~b31 = CPU MIU base address [:3]

*
* QMEM (an internal SRAM) mapping to the CPU address space
*
*  The QMEM is going to be accessible from the respective bus
*  whenever this evaluates to true:  (addr & QMEM_xMASK) == QMEM_xBASE
*
* QMEM itself is 16 KiB long.
*
regC4-C7: QMEM_IBASE
    b0~b31 = QMEM base address (on instruction bus)
regC8-CB: QMEM_IMASK
    b0~b31 = QMEM address mask (on instruction bus)
regCC-CF: QMEM_DBASE
    b0~b31 = QMEM base address (on data bus)
regD0-D3: QMEM_DMASK
    b0~b31 = QMEM address mask (on data bus)

*
* Firmware download:
*
*  The firmware is downloaded into the QMEM.
*
regF0-F1: DNLD_ADDR
    b0~b15 = Firmware download MIU address [21:6]
regF2-F3: DNLD_NUM
    b0~b15 = Download size [17:2]

*
* CPU control:
*
regF4-F5: CTRL
    b0 = Enable CPU
    b1 = CPU soft reset (0 = assert)
    b2 = Download start
    b3 = Download done flag
    b4 = TSFile Enable
    b5 = MIU read priority
    b6 = MIU write priority
    b7 = MUX0 pad select
    b8 = Instruction cache enable
    b9 = MUX1 pad select
    b10 = CPU2MI read priority (MIU access by the CPU)
    b11 = CPU2MI write priority
    b12 = Instruction bus endianess (0 = Little, 1 = Big)
    b13 = Data bus endianess (0 = Little, 1 = Big)

reg10E:
    b0~b3 = MIU DMA address high [25:22]
    * used for e.g. the firmware download
```

## CPU details

The CPU describes itself in the SPR's as follows:

```
Version Register...........................: $12200003
    Revision..............: 3
    Updated version regs..? no
    Reserved..............: 0
    Configuration.........: 32
    Version...............: 18
Unit Present Register......................: $00000665
    UPR itself............? yes
    Data cache............? no
    Instruction cache.....? yes
    Data MMU..............? no
    Instruction MMU.......? no
    MAC...................? yes
    Debug unit............? yes
    Performance counters..? no
    Interrupt controller..? no
    Power management......? yes
    Tick timer............? yes
    Reserved.: 0
    CUP......: $00
CPU Configuration Register.................: $00000020
    Shadow GPRs...........: 0
    Custom GPR file.......? no
    ORBIS32...............? yes
    ORBIS64...............? no
    ORFPX32...............? no
    ORFPX64...............? no
    ORVDX64...............? no
    No delay slot.........? no
    Arch version register.? no
    EVBAR present.........? no
    Imp-spec registers....? no
    AECR/AESR present.....? no
    ORFPX64A32............? no
Data Cache Configuration Register..........: $00000000
Instruction Cache Configuration Register...: $00002648
    Cache ways............: 1
    Cache sets............: 512
    Cache block size......: 16
    Control register......? yes
    Block invalidate reg..? yes
    Block prefetch reg....? no
    Block lock register...? no
    Size..................: 8192 bytes
```
