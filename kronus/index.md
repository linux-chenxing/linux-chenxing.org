# Kronus

## Specs

-  MIPS 34Kc with (broken?) FPU, 2 VPEs and 16 KiB I/D caches
-  32 KiB of some OTP ROM (which contains jump to 0x94000000 (SPI flash map in kseg0), some mips code and some hashes)

[Pinouts](pinouts.md) | [RIU map](riu-map.md) | [Interrupt map](int-map.md)

## MSD7816

-  Chip ID: 0x2f | 0x00 0x00 0x06
-  [Pinout](pinouts.md#msd7816)
-  CPU clock speed: 552 MHz

### Boards

-  [KLF7816_T2_02](klf7816_t2_02)
