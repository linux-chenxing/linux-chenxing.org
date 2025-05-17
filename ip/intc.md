# Interrupt controllers

## Details

Each interrupt controller "piece" can handle up to 64 interrupts which are either level-triggered (IRQ) or edge-triggered (FIQ).
The FIQ and IRQ pieces are then paired into a block called "host"; all of them share the same interrupt inputs but they target different places on the SoC.

The `INTR_CTRL` block in the Non-PM space has a total of 4 intc hosts, that can handle up to 64 IRQs and FIQs each.
The hosts usually target the following places in the SoC: 1st host goes to PM51, 2nd host goes to AEON (aka MCU32 or MHEG5),
and the remaining two hosts are going to the MIPS/ARM CPU(s).

The `IRQ` block in the PM space has only two pieces that handle just 16 interrupts each.

### IRQ

These are simple level-triggered interrupts that are simply passed through when the 'mask' bit is cleared on the corresponding interrupt line.

```
           _____
IRQ >>----\\    \      ____               status
          || XOR |-----\   \       ____     |
      .---//____/      | OR |-----|    \    |
      |             .--/___/      | AND |---+-->> output
   polarity         |          .--o____/
                  assert       |
                              mask
```

### FIQ

These are edge-triggered interrupts that are basically connected to an RS-latch, which sets whenever a rising edge comes on its input,
and then it stays active until the 'eoi' bit is set, which resets the latch and thus acknowledges the interrupt itself.

The mask only affects the final status of the interrupt, the latch can still be set even when the interrupt is masked on the output.

```
           _____
FIQ >>----\\    \        ____
          || XOR |------|S   |      ___               status
      .---//____/       |    |-----\   \       ____     |
      |             .---|R___|     | OR |-----|    \    |
   polarity         |           .--/___/      | AND |---+-->> output
                   eoi          |          .--o____/
                              assert       |
                                          mask
```

## Register map

In the Non-PM intc (the `INTR_CTRL`), there are 8 intc pieces that are laid out as follows:

| RIU   | CPU    | Description |
|-------|--------|-------------|
| +0x00 | +0x000 | Host 1 FIQ  |
| +0x20 | +0x040 | Host 1 IRQ  |
| +0x40 | +0x080 | Host 2 FIQ  |
| +0x60 | +0x0C0 | Host 2 IRQ  |
| +0x80 | +0x100 | Host 3 FIQ  |
| +0xA0 | +0x140 | Host 3 IRQ  |
| +0xC0 | +0x180 | Host 4 FIQ  |
| +0xE0 | +0x1C0 | Host 4 IRQ  |

Each piece has the following registers:

| RIU   | CPU   | Description                               |
|-------|-------|-------------------------------------------|
| +0x00 | +0x00 | interrupt assert (0..15)                  |
| +0x02 | +0x04 | interrupt assert (16..31)                 |
| +0x04 | +0x08 | interrupt assert (32..47)                 |
| +0x06 | +0x0c | interrupt assert (48..63)                 |
| +0x08 | +0x10 | interrupt mask, 0=allow, 1=block (0..15)  |
| +0x0a | +0x14 | interrupt mask, 0=allow, 1=block (16..31) |
| +0x0c | +0x18 | interrupt mask, 0=allow, 1=block (32..47) |
| +0x0e | +0x1c | interrupt mask, 0=allow, 1=block (48..63) |
| +0x10 | +0x20 | interrupt polarity (0..15)                |
| +0x12 | +0x24 | interrupt polarity (16..31)               |
| +0x14 | +0x28 | interrupt polarity (32..47)               |
| +0x16 | +0x2c | interrupt polarity (48..63)               |
| +0x18 | +0x30 | interrupt status, write 1 to ACK (0..15)  |
| +0x1a | +0x34 | interrupt status, write 1 to ACK (16..31) |
| +0x1c | +0x38 | interrupt status, write 1 to ACK (32..47) |
| +0x1e | +0x3c | interrupt status, write 1 to ACK (48..63) |

Note: ACKs are needed only on the FIQ interrupts (for the obvious reasons).
On IRQs they have no effect (or actually may break something, not exactly sure).

## Platform-specific info

### ARM

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

### MIPS

On MIPS platforms, one of the intc hosts is connected to the CPU's interrupt inputs this way: IRQ piece goes to the HW0 input and FIQ piece goes to the HW1 input. (these are interrupts 2 and 3 respectively.)

Usually it's the 4th host (0x1f203380-0x1f2033ff) that is used for the MIPS CPU, but sometimes the 3rd host (0x1f203300-0x1f20337f) is used instead (maybe also for the second VPE in the former case).
