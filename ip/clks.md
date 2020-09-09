## Clock

### Clock Tree

```
       
         |-----\        |-------\
         |      |-------| cpupll |------------------------------ processors 
         |      |   |   |-------/
         |      |   |          |------\
  xtal---| mpll |    \---------|       |-----|------------\
       | |      |--------------|  pll  |-----| clkgen gate |---- perpheral
       | |      |--------------| gates |-----|------------/
       | |      |--------------|       |
       | |-----/           ----|       |
       |                  /    |------/
       |                  |
       | |-----\          |
       | |      |         |
       \-| usb  |--------/
         | pll  |
         |      |
         |-----/


```

### MPLL

Seems to mean "Main PLL". This is the main source of clocks for peripherals. Outside of the PM domain.

| offset        | 15 | 14 | 13                    | 12                    | 11 | 10 | 9                   | 8                   | 7                    | 6                    | 5                    | 4                    | 3                    | 2                    | 1                    | 0                    | notes |
|---------------|----|----|-----------------------|-----------------------|----|----|---------------------|---------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|-------|
| test?         |    |    |                       |                       |    |    |                     |                     |                      |                      |                      |                      |                      |                      |                      |                      |       |
| power control |    |    |                       |                       |    |    |                     |                     |                      |                      |                      |                      |                      |                      |                      | mpll_pd              |       |
| config 1      |    |    |                       |                       |    |    | mpll_loop_div_first | mpll_loop_div_first |                      |                      | mpll_input_div_first | mpll_input_div_first |                      |                      |                      |                      |       |
| config 2      |    |    | mpll_output_div_first | mpll_output_div_first |    |    |                     |                     | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second |       |
| status        |    |    |                       | mpll_lock             |    |    |                     |                     |                      |                      |                      |                      |                      |                      |                      |                      |       |

### UPLL

This seems to generate 320MHz and 384MHz clocks for the USB phys/controllers

### pll gates

This is a pretty weird thing;
- The force on bits start on as 0xffff
- The force off bits start as 0x0.
- A gate apparently stays on if it is forced on or something is using it and it's not forced off
- A gate with get turned off if it is force off or nothing is using it and it's not forced on
- the "en rd bits" update when a consumer of a clock is turned on.

```
/*
 * - 0x1c0(0x70) - pll gater lock
 *     1     |     0
 *  off lock | on lock
 *
 *  once a bit is set here it cannot be unset.
 *
 * - 0x1c4(0x71) - pll force on bits
 * - 0x1c8(0x72) - pll force off bits
 * - 0x1cc(0x73) - pll en rd bits
 *      15   |       14  |     13   |     12   |     11   |     10   |     9    |     8
 *  pll rv1  |  mpll 86  | mpll 124 | mpll 123 | mpll 144 | mpll 172 | mpll 216 | mpll 288
 *      7    |     6     |     5    |     4    |     3    |     2    |     1    |     0
 *  mpll 345 | mpll 432  | utmi 480 | utmi 240 | utmi 192 | utmi 160 | upll 320 | upll 384
*/
```

### clkgen muxes

[listing of the muxes](https://github.com/fifteenhex/SDK_pulbic/blob/master/Mercury5/proj/sc/driver/hal/mercury/kernel/inc/kernel_clkgen.h)

These are 16 bit registers that contain clock muxes for one or more peripherals usually grouped, i.e. uart0 and uart1.

The muxes generally seemed to configured as diagramed below. There is one mux that takes inputs that are from the non-pm domain and then another mux that uses either the selected clock or a clock that is in the always on domain. The vendor code calls this "deglitching".

```
          pll select  deglitch
             | |          |
             | |          |
            -----\        |
            |     \       |
pll input - |      \     ---\
pll input - |       |---|    \
pll input - |      /    |     \
            |     /     |      |---- output
            -----/      |     /
xtal -------------------|    /
                         ---/
                          |
                          |
                          |
                        enable
```


#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### cpuclk

This (probably) a PLL that is used for dynamically scaling the CPU frequency.

#### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

### LPLL 

Line/LCD PLL? Seems to be a PLL for generating the base clock for PNL.

#### MCM

"memory clock manager"?
