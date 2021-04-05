# EMAC

The 100mbit version seems to be a Cadence emac or macb.
We can be fairly sure of this as the drivers on both the u-boot
and linux sides for the Cadence IP work already.

This is probably via similar to the AT91RM200 version of the IP
based on the comments that are in the vendor driver. Those comments
match almost exactly with some comments that were in some official
code for the AT91RM200

[AT91RM200 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-1768-32-bit-ARM920T-Embedded-Microprocessor-AT91RM9200_Datasheet.pdf)

[Recent register header](https://github.com/m-zjj/myzr-gateway-info/blob/master/kernel/drivers/sstar/emac/hal/infinity3/mhal_emac.h)

## Known differences from the AT91RM200

- Registers have the weird split and spacing because they
  are connected to the CPU via RIU. For the MSC313e and beyond the
  registers are also accessible unsplit via XIU.

- AT91RM200 datasheet says the RX descriptor counter wraps at 1024
  descriptors if there isn't a wrap marked descriptor. For some reason
  or other in u-boot at least you can' just use any old number of descriptors.
  
  For the i1/i3:
  - 8 works, 16 doesn't work, 32 works, 64 works, 96 works, 128 works
  
  For the i2m:
  - 8 works, 96 doesn't work.

The TSR register has some new bits

| name        | 15 | 14 | 13 | 12        | 11        | 10        | 9         | 8    | 7    | 6 | 5 | 4 | 3 | 2 | 1 | 0                          | notes            |
|-------------|----|----|----|-----------|-----------|-----------|-----------|------|------|---|---|---|---|---|---|----------------------------|------------------|
| TSR         |    |    |    | FIFO4IDLE | FIFO3IDLE | FIFO2IDLE | FIFO1IDLE | FBNQ | TBNQ |   |   |   |   |   |   |                            |                  |

- There are some extra registers after the documented ones that are called "JULIAN".
  These are only visable via the RIU interface. The XIU only exposes the standard registers.

| name        | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0                          | notes            |
|-------------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|----------------------------|------------------|
| julian 0100 |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                            | select mii/rmii? |
| julian 0104 |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   | software descriptor enable |                  |
| julian 0108 |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                            |                  |

- TAR/TCR seem to load the descriptor address and length into a 4 deep FIFO so that frames can be queued while transmission is on going. 
