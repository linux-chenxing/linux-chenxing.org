# PM Regmap

The following is probably only for infinity/mercury5. The headers for different chips look very similar so there is probably a lot in common but it's hard to say.

## PM sleep registers - 0x1f001c00

This block contains a ton of random bits that control how the "PM" domain that stays powered up even when the chip is sleeping.

| offset | name             | 15         | 14 | 13 | 12           | 11                 | 10 | 9 | 8 | 7 | 6 | 5           | 4                 | 3               | 2                 | 1                 | 0 | default | Notes                                                             |
|--------|------------------|------------|----|----|--------------|--------------------|----|---|---|---|---|-------------|-------------------|-----------------|-------------------|-------------------|---|---------|-------------------------------------------------------------------|
| 0x10   | int status[0]    |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         |                                                                   |
| 0x20   | wkint mask[1]    |            |    |    |              |                    |    |   |   |   |   |             | wkint rtc mask    |                 | wkint wol mask    | wkint sar mask    |   |         | bottom 8 bits are "wake up int controller"                        |
| 0x24   | wkint intpol     | power down |    |    | hk uart sel? | disable pm_uart rx |    |   |   |   |   |             | wkint rtc pol     |                 | wkint wol pol     | wkint sar pol     |   |         | bottom 8 bits are "wake up int controller"                        |
| 0x38   | wkint intstatus  |            |    |    |              |                    |    |   |   |   |   |             | wkint rtc status? |                 | wkint rtc status? | wkint rtc status? |   |         | bottom 8 bits are "wake up int controller"                        |
| 0x48   | pm_lock          |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         | write 0xbabe to unlock pm_gpio4                                   |
| 0x70   |                  |            |    |    |              |                    |    |   |   |   |   |             | ir in is gpio     | isoen2gpio4?    | link wkint2gpio4? |                   |   |         |                                                                   |
| 0x7c   |                  |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         | chip_config in sdram boot script                                  |
| 0x80   | mcu, spi clkgen  |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         |                                                                   |
| 0xa0   | pin muxing?      |            |    |    |              |                    |    |   |   |   |   | pm_led mode | pm_led mode       |                 |                   |                   |   |         | values from ssd20x padmux table                                   |
| 0xa4   | resets           |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         |                                                                   |
| 0xb8   |                  |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         | write 0x79 to trigger a reset                                     |
| 0xbc   |                  |            |    |    |              |                    |    |   |   |   |   |             |                   | temp sensor en? |                   |                   |   |         |                                                                   |
| 0xc0   |                  |            |    |    |              |                    |    |   |   |   |   |             | ipl sets          |                 |                   | x                 | x | 0x003   |                                                                   |
| 0xcc   |                  |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         | power down code writes 0x9fe8 here                                |
| 0xc8   |                  |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         | power down code writes 0x9fe8 here                                |
| 0xdc   |                  |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         | some pm code writes 0xa5 here                                     |
| 0xec   | resume address l |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         |                                                                   |
| 0xf0   | resume address h |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   |         |                                                                   |
| 0xf4   |                  |            |    |    |              |                    |    |   |   |   |   |             |                   |                 |                   |                   |   | 0x003f  | ipl sets to zero sdram script says "turn on xtal outputs to plls" |

0 - This is the status of interrupts from the pm gpio block. The pmsleep->arm interrupt is OR'd with this.
1 - wkint is another interrupt controller that seems to output a single wakeup interrupt and is OR'd with the pmsleep->arm interrupt

0xa4, i3 and i2m can write 0xff80

-- [0x196 - PNL ip version for i2m?](https://github.com/linux-chenxing/uboot_msc313e/blob/8fcf8839f002607b789e04f6f51621a85c1826f1/drivers/mstar/panel/hal/infinity2m/src/hal_pnl.c#L739) 

### Resets experiments

Should be unlock die domain reset and fire, cause everything to lock up and power consumption to drop from 115ma to 15ma.

```
=> mw.w 0x1f001cb4 b8d4
=> mw.w 0x1f001ca4 0x0800
```

- Not setting the password stops anything happening so the password is right.
- The reset fire bit needs to be cleared and set again after setting the password. Firing and then setting the password does nothing.
- Setting the bits in the top of the reset register doesn't stop the reset from happening.

ARM cpu reset

```
=> mw.w 0x1f001cb0 0xb8d3
=> mw.w 0x1f001ca4 0x400
```

- Not setting the password stop anything happening so the password is right.
- Setting the top bits in the reset register causes everything to lock up. Reset held low? Power consumption only drops to 110ma from 115ma

8051 reset

```
mw.w 0x1f001ca4 0x1000
```

-- Consumption jumps from ~115ma to ~120ma

```
-- => md.w 0x1f0021f8 0x4
1f0021f8: 3fac 0000 ff00 0000                        .?......
```

This value starts changing. This apparently the 8051 program counter.


```
mw.w 0x1f001ca4 0x0000
```

-- Consumption returns to ~115ma

```
mw.w 0x1f001cac 0x829f
```

-- Does nothing apparently. Reset bit above doesn't care.

## mystery block - 0x1f007800?

The vendor pm suspend code does something here but the bootrom and ipl don't touch it.

| offset | name | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | Notes                                          |
|--------|------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|---|------------------------------------------------|
| 0x40   |      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | 0x0010 when booted, can write 0x00F9           |
| 0x44   |      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | 0x0001 when booted, can write 0xFFFF           |
| 0x48   |      |    |    |    |    |    |    |   |   |   | x | x |   |   |   |   |   | 0x0000 when booted, writing locks up processor |


### DRAM boot script findings

- 0x1cf8 - 0xff -- comment says "skip password"
- 0x1ca6 - 0x40??
