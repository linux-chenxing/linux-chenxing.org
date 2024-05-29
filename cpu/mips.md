# MIPS

## Memory map

### Old MIPS

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

MIPS cores have a local interrupt controller that handles 8 interrupts in total,
out of which the first two interrupts are the software-generated interrupts,
and the fifth hardware interrupt input (the 7th interrupt) is wired to the
MIPS' internal timer.

The [Non-PM intc](../ip/intc.md) host used for the MIPS CPU is usually the 4th one, but sometimes
the 3rd one is used instead. I believe the 3rd host is also used for the 2nd VPE
but I haven't yet verified that.

| Input   | Usage                    |
|---------|--------------------------|
| 0 (SW0) | Software interrupt       |
| 1 (SW1) | Software interrupt       |
| 2 (HW0) | Non-PM intc IRQ          |
| 3 (HW1) | Non-PM intc FIQ          |
| 4 (HW2) |                          |
| 5 (HW3) |                          |
| 6 (HW4) |                          |
| 7 (HW5) | MIPS timer               |
