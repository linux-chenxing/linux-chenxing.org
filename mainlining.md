# Mainlining

## Git trees

[Mainline staging tree](https://github.com/fifteenhex/linux/tree/msc313_mainlining) - This tree contains cleaned up patches that have/will be trying to enter mainline.

[Dirty work tree](https://github.com/fifteenhex/linux/tree/mstar_dev_v5_8_rebase_cleanup) - This tree contains the most hardware support but is also a complete mess. Rebasing happens often here.

## Round 1: Initial support (arch definition, basic DTS, UART)

**DONE**

The current patcheset is at V4 and can be seen on [patchwork](https://patchwork.kernel.org/cover/11607257/) or [on msc313_mainlining branch on github](https://github.com/fifteenhex/linux/commits/msc313_mainlining). With those patches you can boot your [Breadbee](https://github.com/breadbee/breadbee/) or [70mai Dash Cam](boards/dashcamlite.md) boards with the serial console and initramfs. Not much more is working at this stage, though, not even a reset.

## Round 2: Push as much trivial DTS stuff as possibleg

**DONE**

Bunch of purely DTS stuff. Adds SRAM, PMU and reboot support so that resetting now works.

## Round 3: Interrupt controllers?

**WAITING**

- MediaTek are pushing a driver for the same intc. Waiting for that to merge before pushing the DTS parts we need.

## Round 4: Initial clocks, MPLL, PLL gater, clock gates

## Round 5: DW uart quirk + wiring for mstar

## Round 6: Push i2m/SMP support?
