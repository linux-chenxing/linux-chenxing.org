# MIPS

## Memory map

### Old MIPS

Probably present in all MIPS 4Kc-based SoCs. Or whatever, but feels like that's an early design.

| Address                 | Usage                               |
|-------------------------|-------------------------------------|
| 0x00000000 - 0x0FFFFFFF | MIU0                                |
| 0x14000000 - 0x14FFFFFF | SPI flash mapping (might be)        |
| 0x1F800000 - 0x1F807FFF | RIU                                 |
| 0x1FC00000 - 0x1FFFFFFF | SPI flash mapping (on reset vector) |

### New MIPS (without OTP)

| Address                 | Length  | Usage                               |
|-------------------------|---------|-------------------------------------|
| 0x00000000 - 0x0FFFFFFF | 256 MiB | MIU0                                |
| 0x14000000 - 0x1BFFFFFF | 128 MiB | SPI flash (QSPI)                    |
| 0x1F000000 - 0x1F3FFFFF | 4 MiB   | RIU                                 |
| 0x1FC00000 - 0x1FFFFFFF | 4 MiB   | SPI flash (on reset vector)         |
| 0x40000000 - 0x4FFFFFFF | 256 MiB | MIU1                                |

### New MIPS (with OTP)

| Address                 | Length  | Usage                               |
|-------------------------|---------|-------------------------------------|
| 0x00000000 - 0x0FFFFFFF | 256 MiB | MIU0                                |
| 0x10000000 - 0x13FFFFFF | 4 MiB   | OTP                                 |
| 0x14000000 - 0x1BFFFFFF | 128 MiB | SPI flash (QSPI)                    |
| 0x1F000000 - 0x1F3FFFFF | 4 MiB   | RIU                                 |
| 0x1FC00000 - 0x1FFFFFFF | 4 MiB   | OTP (on reset vector)               |
| 0x40000000 - 0x4FFFFFFF | 256 MiB | MIU1 (likely)                       |

## Interrupt map

MIPS cores have a local interrupt controller which handles 8 interrupts,
where the first two are software interrupts, and the last one is connected to the MIPS' internal timer.

The Non-PM intc in question is either the third or the fourth one.
Usually it's the latter but sometimes the third one seems to be wired up instead.

Sometimes the fourth one is used for VPE0, while the third one is used for VPE1. (presumeably)

| Line | Usage                    |
|------|--------------------------|
| 0    | Software interrupt       |
| 1    | Software interrupt       |
| 2    | Non-PM intc IRQ          |
| 3    | Non-PM intc FIQ          |
| 4    |                          |
| 5    |                          |
| 6    |                          |
| 7    | MIPS timer               |
