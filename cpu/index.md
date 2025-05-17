# CPU cores

## 8051

The first MCU/CPU that was ever used in MStar's chips, as before that, you had to use an external MCU to control their display controller chips.

It's also used in various in-chip subsystems like [PM51](../ip/pm51.md), etc;
and in various utlility chips like touchscreen controllers, DTV demodulators...

## OpenRISC

The [OpenRISC](https://openrisc.io) architecture, or specifically, OpenRISC 1000 "or1k" core,
although this does not imply that they didn't made a compatible core themselves.

It is mostly seen used as a coprocessor in the system (the "AEON" coprocessor, and the "VPU");
it also lives in the TSP (MPEG-2 Transport Stream processor) block.

- [More info](or1k.md)

## AEON R2

AEON R2 (or simply "R2") is a custom 32-bit architecture that is heavily based off OpenRISC.

- [More info](aeon-r2.md)
- [AEON in general](aeon.md)

## MIPS

A family of MIPS CPU's were used in MStar SoCs.

- MIPS 4Kc
- MIPS 34Kc
- MIPS 34Kf
- MIPS 74Kf

- [More info](mips.md)

## ARM

Used in all SigmaStar SoCs, many MStar SoCs, and basically chips made on this arch is the main scope of this project.
