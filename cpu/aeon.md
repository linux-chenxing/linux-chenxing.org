# AEON

**Notice:** For the description of the AEON R2 architecture, that this page previously was all about,
refer to the corresponding page: [AEON R2](aeon-r2.md).

This page describes the common stuff implemented with both the [OpenRISC](or1k.md) proper and the AEON R2 itself.

## Memory map

The usual memory mapping is as follows:

| Address    | Usage                                                |
|------------|------------------------------------------------------|
| 0x00000000 | MIU (or also SPI flash)                              |
| 0x90000000 | Local UART                                           |
| 0xA0000000 | RIU                                                  |
| 0xB0000000 | SRAM (4k?)                                           |
| 0xC0000000 | SRAM (the Titania2 variant or the pre-Titania3 one?) |

However, the SRAM and RIU portions can be remapped to almost any arbitrary address, if needed.
For example, in coprocessors the [MCU32](../ip/mcu32.md) block has registers that control exactly that.

The MIU map, however, is fixed to zero (since the exception vectors start at 0x100 and there is no EVBAR implemented),
thus it's important to have it fixed to the beginning of the memory space.

Same almost applies to the SPI flash map, with the exception of that the SPI mapping on the data bus usually can be changed too.

### Local UART

There is an "tigthly coupled" 8250 UART that is mapped with one byte per register (i.e. `reg-shift = <0>'`).

## Interrupt map

The interrupt controller used is the native Programmable Interrupt Controller (PIC).

| Line | Usage                         |
|------|-------------------------------|
| 2    | Second Non-PM intc's FIQ part |
| 3    | Second Non-PM intc's IRQ part |
| 19   | Local UART                    |
