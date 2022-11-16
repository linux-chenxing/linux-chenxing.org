# CPU cores

## 8051

The first MCU/CPU that was ever used in MStar's chips,
as before that, you had to use an external MCU to control their display controller chips.

It's also used in various chip subsystems (like [PM51](../ip/pm51.md));
and in various utlility chips like touchscreens, demodulators...

## OpenRISC

The [OpenRISC](https://openrisc.io) architecture, or specifically, OpenRISC 1000 "or1k" core,
althrough this does not imply that they didn't made a compatible core themselves.

It lives in some IP blocks (like TSP, MVD and HVD), rather than being a housekeeping core (i.e. the main core).

## AEON

AEON, "BEON", "R2", "RISC32", whatever it could be called, is a custom 32-bit architecture that is heavily based off OpenRISC,
where the changes basically were done in the instruction encoding scheme, as well as any other change that might follow because of that.

[More info](aeon.md)

## MIPS

The MIPS architectures...

- MIPS 4Kc
- MIPS 34Kc
- MIPS 34Kf

[More info](mips.md)

## ARM

The ARM architectures...

A higher performance, feature, and etc architecture.

Used in all SigmaStar SoCs, many MStar SoCs, and basically chips made on this arch is the main scope of this project.
