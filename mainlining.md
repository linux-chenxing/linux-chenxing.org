# Mainlining

## Git trees

[Mainline staging tree](https://github.com/fifteenhex/linux/tree/msc313_mainlining) - This tree contains cleaned up patches that have/will be trying to enter mainline. This will get rebased but only for new versions of a patch series or on top of torvalds/master.

[Linux v5.9 tree](https://github.com/fifteenhex/linux/tree/mstar_v5_9_rebase) - Linux 5.9 with a mess of patches on top. Frozen. This is for validating that rebasing, cleaning up etc for 5.10 hasn't busted anything.

[Linux v5.10 tree](https://github.com/fifteenhex/linux/tree/mstar_v5_10_rebase) - Linux 5.10 with slightly less of a mess of patches on top. Frozen. This if for validating that rebase, cleaning up etc for 5.11 hasn't busted anything

[Linux v5.11 tree](https://github.com/fifteenhex/linux/tree/mstar_v5_11_rebase) - Linux 5.11 with patch soup. Frozen.

[Linux v5.12 tree](https://github.com/fifteenhex/linux/tree/mstar_v5_12_rebase) - Linux 5.12 with patch soup. Frozen.

[Linux v5.13 tree](https://github.com/fifteenhex/linux/tree/mstar_v5_13_rebase) - This tree contains the most hardware support but is also a complete mess. Rebasing happens often here.

## Round 1: Initial support (arch definition, basic DTS, UART)

**DONE**

The current patcheset is at V4 and can be seen on [patchwork](https://patchwork.kernel.org/cover/11607257/) or [on msc313_mainlining branch on github](https://github.com/fifteenhex/linux/commits/msc313_mainlining). With those patches you can boot your [Breadbee](https://github.com/breadbee/breadbee/) or [70mai Dash Cam](boards/dashcamlite.md) boards with the serial console and initramfs. Not much more is working at this stage, though, not even a reset.

## Round 2: Push as much trivial DTS stuff as possible

**DONE**

Bunch of purely DTS stuff. Adds SRAM, PMU and reboot support so that resetting now works.

## Round 3: non-PM interrupt controller

**DONE** 5.10

## Round 4: GPIO

**DONE** 5.11

https://patchwork.kernel.org/bundle/dgp/mstar%20-%20msc313%20gpio/


## Round 5: Initial clocks, MPLL, PLL gater, clock gates

** MPLL Pushed ** 
https://patchwork.kernel.org/bundle/dgp/mstar%20-%20mpll/

** v2 pushed **
** in clk-next** Driver is in 5.12. DTS bits are missing, queued for 5.13

## Round 6: pm intc

## Round 7: pm gpio

## Round 8: DW uart quirk + wiring for mstar

## Round 9: Push i2m/SMP support?

https://patchwork.kernel.org/bundle/dgp/mstar%20-%20infinity2m%20SMP/

**DONE** 5.11

## Round 10: CPU PLL

** pushed **

## Round 11: Pinctrl?

** Cleaning up **
