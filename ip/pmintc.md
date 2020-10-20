```
/*
 * pm "sleep" intc
 * This is another interrupt controller that seems to be in the always on
 * power domain and is probably there to deal with interrupts that wake
 * the chip up.
 *
 * The sleep intc is connected to the GIC via the normal irq intc by a single
 * interrupt so here we handle that interrupt with a chained handler and
 * from the status register work out which interrupts to fire in the domain.
 *
 * Note: Only the first two interrupts that come through this controller are
 * controlled (mask, unmask, eoi etc) here. Everything else is passed through and
 * actually controlled by the sleep gpio controller.
 */
 ```
