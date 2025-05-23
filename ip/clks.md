# Clocks

## Clock Tree

This is a rough guess.

```
       /-------------------------------------------\
       |  |-----\        |-------\                 |
       |  |      |-------| cpupll |----------------|------------- processors 
       |  |      |   |   |-------/                 |
       |  |      |   |          |------\           |
  xtal-+--| mpll |    \---------|       |-----|------------\
       |  |      |--------------|  pll  |-----| clkgen gate |---- perpheral
       |  |      |--------------| gates |-----|------------/
       |  |      |--------------|       |
       |  |-----/     /---------|       |
       |             |          |------/
       |             |
       |  |-----\    |
       |  |      |   |
       |--| usb  |---/-------------------------------------------- usb
       |  | pll  |
       |  |      |
       |  |-----/
       |
       |
       |  |-----\
       |  |      |
       |  | miu  |------------------------------------------------ miu
       \--| pll  |
          |      |
          |-----/
```

## MPLL

Seems to mean "Main PLL". This is the main source of clocks for peripherals. Outside of the PM domain.

- note: How did I come up with this table? :/ -- based on the register descriptions for the mst786 and i2m soc.c
- note: This is entirely a guess based on needing a 864mhz pll frequency and watching what the bits do on the hardware.
        This seems to have the registers shifted to the right by 8 bits compared to the layouts of other mplls that have code in some of the sdks on github.

| name          | offset | 15           | 14 | 13                    | 12                    | 11                         | 10                         | 9                        | 8                   | 7                    | 6                    | 5                    | 4                    | 3                    | 2                    | 1                    | 0                    | notes |
|---------------|--------|--------------|----|-----------------------|-----------------------|----------------------------|----------------------------|--------------------------|---------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|-------|
| test?         | 0x0    |              |    |                       |                       |                            |                            |                          | ?                   |                      |                      |                      | ?                    |                      |                      |                      |                      |       |
| power control | 0x4    |              |    |                       | pd_digclk             | pd_mpll_clk_adc_vco_div2_3 | pd_mpll_clk_adc_vco_div2_3 | pd_mpll_clk_adc_vco_div2 | pd_mpll             | ro?                  | ro?                  | ro?                  | ro?                  | ro?                  | ro?                  | ro?                  | ro?                  |       |
| config 1      | 0x8    |              |    |                       |                       |                            |                            | mpll_loop_div_first      | mpll_loop_div_first |                      |                      | mpll_input_div_first | mpll_input_div_first |                      |                      |                      | en_mpll_rst          |       |
| config 2      | 0xc    |              |    | mpll_output_div_first | mpll_output_div_first |                            | ?                          | ?                        | ?                   | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second | mpll_loop_div_second |       |
| status        | 0x10   | en_mpll_prdt |    |                       | mpll_lock             |                            | en_mpll_xtal               |                          |                     |                      | ?                    | ?                    | ?                    | ?                    | ?                    | en_mpll_ov_sw        | en_mpll_test         |       |

Most ?'s are bits that are writable but are of unknown function.

The main frequency of the PLL is calculated like this ```((f_input / input_div_first) * (loop_div_first * loop_div_second)) / output_div_first```.
Default settings seem to be to give a 432MHz output. Power control should contain bit to power on various dividers that generate the other mpll outputs.

M5 coming out of reset has bits 11 to 8 in the power control register set high.

The IPL code writes to the upper byte of the power control register twice.
- Once before switching the uart clock from the boot clock (xtal/2 IIRC), writes all zeros
- Once before configuring the cpu pll, again writes all zeros. Making sure the out the cpu needs is on?

Post IPL the i3 registers look like this:

```
=> md.w 0x1f206000 0x10
1f206000: 0110 0000 0000 0000 0100 0000 1412 0000    ................
1f206010: 9410 0000 0000 0000 0000 0000 0000 0000    ................
```

At power up on the M5

```
mpll: 0 - 0110
mpll: 4 - 0f00
mpll: 8 - 0100
mpll: c - 1412
mpll: 10 - 8410
```

Bit 12 of 0x10 goes high some time after clearing the top bits of 0x4. Hence it's probably the pll lock bit.

0x8 - clears to 0x0, write 0xffff results in 0x0331
0xc - clears to 0x0, write 0xffff results in 0x37ff
0x10 - clears to 0x0 if not powered up, clears to 0x1000 if powered up (bit 12 is r/o), writes 0x847f

https://github.com/schreibikus/wenshuai.xi/blob/7906c437f42aabfc8ac2e103efac3e885030f0cd/Mstar_code/mboot/sboot/chip/kaiser/script_MainPll_ARMPLL_UPLL_otp.inc#L33

2 - 432

3 - 288

4 - 216

5 - 172.8

6 - 144

7 - 123.4

10 - 86.4

## UPLL

This seems to generate 320MHz and 384MHz clocks for the USB phys/controllers

| address | name | 15        | 14        | 13        | 12        | 11        | 10        | 9         | 8         | 7         | 6         | 5         | 4         | 3             | 2             | 1         | 0                | notes |
|---------|------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|---------------|---------------|-----------|------------------|-------|
| 0x0     |      |           |           |           |           |           |           |           |           | enxtal    |           | enfrun    | enddisc   |               |               | pd        |                  |       |
| 0x4     |      |           |           |           |           |           |           |           |           | en_prdt   |           |           |           |               |               |           |                  |       |
| 0x8     |      | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test | upll_test     | upll_test     | upll_test | upll_test        |       |
| 0x1c    |      |           |           |           |           |           |           |           |           |           |           |           |           | pd_clk0_audio | clk_upll_192m | en_prdt2  | clk0_upll_384_en |       |

UPLL0 at boot on p3:

```
upll dump: 0x1f284000 - 0x11b2
upll dump: 0x1f284004 - 0x1498
upll dump: 0x1f284008 - 0x0110
upll dump: 0x1f28400c - 0x0000
upll dump: 0x1f284010 - 0x23cc
upll dump: 0x1f284014 - 0x0000
upll dump: 0x1f284018 - 0xff00
upll dump: 0x1f28401c - 0x000a
upll dump: 0x1f284020 - 0x0000
upll dump: 0x1f284024 - 0x0000
upll dump: 0x1f284028 - 0x0000
upll dump: 0x1f28402c - 0x0000
upll dump: 0x1f284030 - 0x0000
upll dump: 0x1f284034 - 0x0000
upll dump: 0x1f284038 - 0x0000
upll dump: 0x1f28403c - 0x0000
upll dump: 0x1f284040 - 0x0000
upll dump: 0x1f284044 - 0x0000
upll dump: 0x1f284048 - 0x0000
upll dump: 0x1f28404c - 0x001e
upll dump: 0x1f284050 - 0x0000
upll dump: 0x1f284054 - 0x0000
upll dump: 0x1f284058 - 0x0000
upll dump: 0x1f28405c - 0x0000
upll dump: 0x1f284060 - 0x0000
upll dump: 0x1f284064 - 0x0000
upll dump: 0x1f284068 - 0x0000
upll dump: 0x1f28406c - 0x0000
upll dump: 0x1f284070 - 0x0000
upll dump: 0x1f284074 - 0x0000
upll dump: 0x1f284078 - 0x0000
upll dump: 0x1f28407c - 0x0000
upll dump: 0x1f284080 - 0x11b2
upll dump: 0x1f284084 - 0x1498
upll dump: 0x1f284088 - 0x0110
upll dump: 0x1f28408c - 0x0000
upll dump: 0x1f284090 - 0x23cc
upll dump: 0x1f284094 - 0x0000
upll dump: 0x1f284098 - 0xff00
upll dump: 0x1f28409c - 0x000a
upll dump: 0x1f2840a0 - 0x0000
upll dump: 0x1f2840a4 - 0x0000
upll dump: 0x1f2840a8 - 0x0000
upll dump: 0x1f2840ac - 0x0000
upll dump: 0x1f2840b0 - 0x0000
upll dump: 0x1f2840b4 - 0x0000
upll dump: 0x1f2840b8 - 0x0000
upll dump: 0x1f2840bc - 0x0000
upll dump: 0x1f2840c0 - 0x0000
upll dump: 0x1f2840c4 - 0x0000
upll dump: 0x1f2840c8 - 0x0000
upll dump: 0x1f2840cc - 0x001e
upll dump: 0x1f2840d0 - 0x0000
upll dump: 0x1f2840d4 - 0x0000
upll dump: 0x1f2840d8 - 0x0000
upll dump: 0x1f2840dc - 0x0000
upll dump: 0x1f2840e0 - 0x0000
upll dump: 0x1f2840e4 - 0x0000
upll dump: 0x1f2840e8 - 0x0000
upll dump: 0x1f2840ec - 0x0000
upll dump: 0x1f2840f0 - 0x0000
upll dump: 0x1f2840f4 - 0x0000
upll dump: 0x1f2840f8 - 0x0000
upll dump: 0x1f2840fc - 0x0000
upll dump: 0x1f284100 - 0x11b2
upll dump: 0x1f284104 - 0x1498
upll dump: 0x1f284108 - 0x0110
upll dump: 0x1f28410c - 0x0000
upll dump: 0x1f284110 - 0x23cc
upll dump: 0x1f284114 - 0x0000
upll dump: 0x1f284118 - 0xff00
upll dump: 0x1f28411c - 0x000a
upll dump: 0x1f284120 - 0x0000
upll dump: 0x1f284124 - 0x0000
upll dump: 0x1f284128 - 0x0000
upll dump: 0x1f28412c - 0x0000
upll dump: 0x1f284130 - 0x0000
upll dump: 0x1f284134 - 0x0000
upll dump: 0x1f284138 - 0x0000
upll dump: 0x1f28413c - 0x0000
upll dump: 0x1f284140 - 0x0000
upll dump: 0x1f284144 - 0x0000
upll dump: 0x1f284148 - 0x0000
upll dump: 0x1f28414c - 0x001e
upll dump: 0x1f284150 - 0x0000
upll dump: 0x1f284154 - 0x0000
upll dump: 0x1f284158 - 0x0000
upll dump: 0x1f28415c - 0x0000
upll dump: 0x1f284160 - 0x0000
upll dump: 0x1f284164 - 0x0000
upll dump: 0x1f284168 - 0x0000
upll dump: 0x1f28416c - 0x0000
upll dump: 0x1f284170 - 0x0000
upll dump: 0x1f284174 - 0x0000
upll dump: 0x1f284178 - 0x0000
upll dump: 0x1f28417c - 0x0000
upll dump: 0x1f284180 - 0x11b2
upll dump: 0x1f284184 - 0x1498
upll dump: 0x1f284188 - 0x0110
upll dump: 0x1f28418c - 0x0000
upll dump: 0x1f284190 - 0x23cc
upll dump: 0x1f284194 - 0x0000
upll dump: 0x1f284198 - 0xff00
upll dump: 0x1f28419c - 0x000a
upll dump: 0x1f2841a0 - 0x0000
upll dump: 0x1f2841a4 - 0x0000
upll dump: 0x1f2841a8 - 0x0000
upll dump: 0x1f2841ac - 0x0000
upll dump: 0x1f2841b0 - 0x0000
upll dump: 0x1f2841b4 - 0x0000
upll dump: 0x1f2841b8 - 0x0000
upll dump: 0x1f2841bc - 0x0000
upll dump: 0x1f2841c0 - 0x0000
upll dump: 0x1f2841c4 - 0x0000
upll dump: 0x1f2841c8 - 0x0000
upll dump: 0x1f2841cc - 0x001e
upll dump: 0x1f2841d0 - 0x0000
upll dump: 0x1f2841d4 - 0x0000
upll dump: 0x1f2841d8 - 0x0000
upll dump: 0x1f2841dc - 0x0000
upll dump: 0x1f2841e0 - 0x0000
upll dump: 0x1f2841e4 - 0x0000
upll dump: 0x1f2841e8 - 0x0000
upll dump: 0x1f2841ec - 0x0000
upll dump: 0x1f2841f0 - 0x0000
upll dump: 0x1f2841f4 - 0x0000
upll dump: 0x1f2841f8 - 0x0000
upll dump: 0x1f2841fc - 0x0000
```

## pll gates

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

## clkgen muxes

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

## cpuclk

This (probably) a PLL that is used for dynamically scaling the CPU frequency.

### Support Matrix

|           | u-boot | linux |
|-----------|--------|-------|
| infinity  |        | yes   |
| infinity3 |        | yes   |
| mercury5  |        | yes   |

## LPLL 

Line/LCD PLL? Seems to be a PLL for generating the base clock for PNL.

| address | name | 15              | 14 | 13      | 12           | 11           | 10           | 9            | 8            | 7              | 6              | 5              | 4              | 3          | 2        | 1              | 0              | description |
|---------|------|-----------------|----|---------|--------------|--------------|--------------|--------------|--------------|----------------|----------------|----------------|----------------|------------|----------|----------------|----------------|-------------|
| 0x0     |      | pd (power down) |    | en_mini | fifo_div5_en | dual_lp_en   | en_fifo      | en_scalar    | sdiv2p5_en   |                |                |                |                | sdiv3p5_en | ictrl    | ictrl          | ictrl          |             |
| 0x4     |      |                 |    |         |              | loop_div_sec | loop_div_sec | loop_div_sec | loop_div_sec |                |                | loop_div_fst   | loop_div_fst   |            |          | input_div_fst  | input_div_fst  |             |
| 0x8     |      |                 |    |         |              |              | fifo_div     | fifo_div     | fifo_div     | scalar_div_sec | scalar_div_sec | scalar_div_sec | scalar_div_sec |            |          | scalar_div_fst | scalar_div_fst |             |
| 0xc     |      |                 |    |         |              |              |              |              |              |                |                |                | skew_en_fixclk |            | skew_div | skew_div       | skew_div       |             |
| 0x10    |      |                 |    |         |              |              |              |              |              |                |                |                |                |            |          |                |                |             |
| 0x14    |      |                 |    |         |              |              |              |              |              |                |                |                |                |            |          |                |                |             |
| 0x18    |      |                 |    |         |              |              |              |              |              |                |                |                |                |            |          |                |                |             |
| 0x1c    |      |                 |    |         |              |              |              |              |              |                |                |                |                |            |          |                |                |             |
| 0x20    |      |                 |    |         |              |              |              |              |              |                |                |                |                |            |          |                |                |             |
| 0x24    |      |                 |    |         |              |              |              |              |              |                |                |                |                |            |          |                |                |             |

 i2m before bootlogo command on the sbc2d70:
 
```
1f206700: 8801 0000 0420 0000 0000 0000 0000 0000    .... ...........
1f206710: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206720: 5544 0000 0024 0000 0001 0000 0000 0000    DU..$...........
1f206730: 0000 0000 0000 0000 0020 0000 0000 0000    ........ .......
1f206740: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206750: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206760: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206770: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206780: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206790: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067a0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067b0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067c0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067d0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067e0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067f0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206800: 0204 0000 0000 0000 0080 0000 1fff 0000    ................
1f206810: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206820: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206830: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206840: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206850: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206860: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206870: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206880: 0080 0000 f0f0 0000 0000 0000 0000 0000    ................
1f206890: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068a0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068b0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068c0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068d0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068e0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068f0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
```

after

```
Wireless-tag# md.w 0x1f206700 0x100                           
1f206700: 2201 0000 0420 0000 0042 0000 0001 0000    .".. ...B.......
1f206710: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206720: c3c3 0000 0043 0000 0001 0000 0000 0000    ....C...........
1f206730: 0000 0000 0000 0000 8019 0000 00c0 0000    ................
1f206740: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206750: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206760: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206770: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206780: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206790: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067a0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067b0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067c0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067d0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067e0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2067f0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206800: 0204 0000 0000 0000 0080 0000 1fff 0000    ................
1f206810: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206820: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206830: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206840: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206850: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206860: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206870: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f206880: 0080 0000 0f0f 0000 0000 0000 0000 0000    ................
1f206890: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068a0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068b0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068c0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068d0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068e0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
1f2068f0: 0000 0000 0000 0000 0000 0000 0000 0000    ................
```

https://github.com/linux-chenxing/linux-ssc325/blob/ikayaki_dlm00v014/arch/arm/boot/dts/infinity2m-clks.dtsi

## MCM

"memory clock manager"?


## Clock register listings

- pioneer3: https://github.com/linux-chenxing/linux-ssc325/blob/ikayaki_dlm00v014/drivers/sstar/include/pioneer3/reg_clks.h
