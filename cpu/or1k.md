# OpenRISC

The OpenRISC 1000 (or1k) architecture is used inside MStar SoCs mostly as miscellaneous co-processors like AEON (MHEG5/MCU32) and VPU (VD_MHEG5/32BIT_MCU),
as well as part of the TSP (Transport Stream Processor) block.

For the coprocessor control block, see the description for [MCU32](../ip/mcu32.md), for the usage within TSP, see [TSP](../ip/tsp.md).

As a housekeeping CPU the [AEON R2](aeon-r2.md) architecture, which is heavily based off OpenRISC, is used instead.

The implementation used in MStar SoCs is a bit different from the usual implementations, one of the differences being that unlike proper OpenRISC,
which is big-endian, MStar SoCs implement it with little-endian byte ordering instead, which complicates usage of the existing toolchains.

## Implementation details

Here is a comparsion chart between the or1k instances in the SoC:

| Criteria             | AEON     | VPU      | TSP      |
|----------------------|----------|----------|----------|
| Operating frequency  | 172 MHz? | 160 MHz? | 144 MHz? |
| QMEM size            | 4 KiB    | 8 KiB    | 16 KiB   |
| SPI flash map size   | 16 MiB   | 64 KiB   | n/a      |
| MIU access           | yes      | yes      | yes      |
| RIU access           | yes      | no       | no       |
| Instruction cache    | 8 KiB    | 8 KiB    | 8 KiB    |
| Data cache           | 4 KiB    | 4 KiB    | n/a      |
| MMU                  | no       | no       | no       |
| Interrupts           | yes      | yes      | no       |
| Tightly-coupled UART | yes      | yes      | yes      |

### SPR contents

- Implementations for AEON/VPU ([MCU32](../ip/mcu32.md)) report the following:

```
Version Register...........................: $12200003
    Revision..............: 3
    Updated version regs..? no
    Reserved..............: 0
    Configuration.........: 32
    Version...............: 18
Unit Present Register......................: $00000767
    UPR itself............? yes
    Data cache............? yes
    Instruction cache.....? yes
    Data MMU..............? no
    Instruction MMU.......? no
    MAC...................? yes
    Debug unit............? yes
    Performance counters..? no
    Interrupt controller..? yes
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
Data Cache Configuration Register..........: $00002640
    Cache ways............: 1
    Cache sets............: 256
    Cache block size......: 16
    Cache write stategy...: write-back
    Control register......? yes
    Block invalidate reg..? yes
    Block prefetch reg....? no
    Block lock register...? no
    Block flush register..? yes
    Block write-back reg..? no
    Size..................: 4096 bytes
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

- Implementation in the [TSP](../ip/tsp.md) reports the following:

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

## Tightly-coupled UART

Seems like every or1k instance in the SoC comes with a tightly-coupled 8250/16550-compatible UART
mapped in the address range 0x90000000-0x9000FFFF, wrapping each 0x20 bytes.

The TSP appears to have the register order swapped within a single word (i.e. instead of "0 1 2 3 4 5 6 7" it's "3 2 1 0 7 6 5 4")

These UARTs can be wired out of the SoC by setting appropriate UART mux registers in the CHIPTOP.<sup>[where?]</sup>
