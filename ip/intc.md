# non-pm interrupt controllers

According to a developer at MediaTek this is the same IP as is in some MediaTek chips.
See this [thread](https://lore.kernel.org/linux-arm-kernel/654a81dcefb3024d762ff338d4bd7f14@kernel.org/T/#m9afc5a57195be881661dcf6ea77a1e299f36d9f6).

```
/* The MSC313 contains two interrupt controllers that are almost identical.
 * The first one handles "FIQ" interrupts and the second handles "IRQ"
 * interrupts. The only differences are the first one only has bits for 32
 * interrupts and needs irqs to be cleared.
 *
 * It's also worth noting that the GIC needs to be configured to disable
 * bypassing the GIC when delivering interrupts from the FIQ controller.
 * Currently this is being done by u-boot.
 *
 * 0x1f201310
 * GIC 96 - 127 - hardware fiq interrupts that go through the intc before the gic
 * mask bits
 * 0x0 0  - 15
 * 0x4 16 - 31
 *
 * polarity
 * 0x10 0 - 15
 * 0x14 16 - 31
 *
 * clear bits
 * 0x20
 * 0x24
 *
 * 0x1f201350
 * GIC 32 - 95 - hardware irq interrupts that go through the intc before the gic
 * mask bits
 * 0x0 - 0 - 15
 * 0x4 - 16 - 31
 * 0x8 - 31 - 47
 * 0xc - 48 - 63
 *
 * polarity
 * 0x10 - 0 - 15
 * 0x14 - 16 - 31
 * 0x18 - 31 - 47
 * 0x1c - 48 - 63
 *
 * raw interrupt status bits -- where did this come from?
 * 0x20
 * 0x24
 * 0x28
 * 0x2c
 */
```
