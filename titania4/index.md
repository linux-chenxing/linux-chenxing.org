# Titania4

## Specs

- MIPS 34Kc (PRId = 0x00019555)
  - Only one VPE
  - 8 KiB I/D caches
  - Clock speed: 312 MHz
- 2x External 16-bit DDR2 up to 64 MiB (128 MiB total)

[Pinouts](pinouts.md) | [RIU map](riu-map.md) | [Interrupt map](int-map.md)

## MSD309PX

- Chip ID: 0x18 / 0x00 0x00 0x03
- 536-ball BGA package (20x20 mm); [Pinout (or ball map, if you will)](pinouts.md#msd309px)
- overclocks to 480/504 MHz when heat up --more testing needed

### Boards

- [L0M05(00)](l0m05-00/index.md)
