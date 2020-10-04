# EMAC

The 100mbit version seems to be a Cadence emac or macb.
We can be fairly sure of this as the drivers on both the u-boot
and linux sides for the Cadence IP work already.

This is probably via similar to the AT91RM200 version of the IP
based on the comments that are in the vendor driver. Those comments
match almost exactly with some comments that were in some official
code for the AT91RM200

[AT91RM200 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-1768-32-bit-ARM920T-Embedded-Microprocessor-AT91RM9200_Datasheet.pdf)

## Known differences from the AT91RM200

- Registers have the weird split and spacing because they
  are connected to the CPU via RIU. For the MSC313e and beyond the
  registers are also accessible unsplit via XIU.

- AT91RM200 datasheet says the RX descriptor counter wraps at 1024
  descriptors if there isn't a wrap marked descriptor. In this version
  of the IP the counter wraps at the 8th descriptor.
