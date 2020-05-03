# MIU

## Analog

| offset | name | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|--------|------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|---|
|        |      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |

## Digital

| offset | name    | 15        | 14                  | 13                 | 12                    | 11   | 10   | 9   | 8                    | 7        | 6       | 5                     | 4           | 3            | 2         | 1          | 0                       |
|--------|---------|-----------|---------------------|--------------------|-----------------------|------|------|-----|----------------------|----------|---------|-----------------------|-------------|--------------|-----------|------------|-------------------------|
| 0x0    | config0 | init done | single command done | enter self refresh | enter deep power down | rasz | casz | wez | issue single command |          |         | turn off auto refresh | turn on odt | dram reset   | enable cs | enable cke | auto initial dram cycle |
| 0x4    | config1 | cko en    | address en          | dq enable          | cke enable            |      |      |     |                      | columns  | columns | banks                 | banks       | bus width    | bus width | dram type  | dram type               |
|        |         |           |                     |                    |                       |      |      |     |                      | 0x0 - 8  |         | 0x0 - 2               |             | 0x0 - 16 bit |           | 0x0 - SDR  |                         |
|        |         |           |                     |                    |                       |      |      |     |                      | 0x1 - 9  |         | 0x1 - 4               |             | 0x1 - 32 bit |           | 0x1 - DDR  |                         |
|        |         |           |                     |                    |                       |      |      |     |                      | 0x2 - 10 |         | 0x2 - 8               |             | 0x2 - 64bit  |           | 0x2 - DDR2 |                         |
|        |         |           |                     |                    |                       |      |      |     |                      |          |         |                       |             |              |           | 0x3 - DDR3 |                         |

## IPL DDR2 init cycle

- clear config0
- delay
- set dram cs and reset in config0
- delay
- enable cke in config0
- delay
- turn on odt and trigger initial cycle in config0
- big delay

```
/*
 * MSC313 MIU (memory interface unit?) - multiport ddr controller
 *
 * The product brief for the msc313e that is available
 * doesn't detail any of the registers for this but it
 * seems to match the MIU in another MStar chip called
 * the MSB2521 that does have a leaked datasheet available.
 * That said I can't be 100% sure that all the bits in the
 * registers match what is actually in the msc313 so I'll
 * document anything that matches and not just paste the
 * whole lot here. TL;DR; there be gaps.
 *
 * 0x1f202000?
 * In the MSB2521 datasheet this is called MIU_ATOP, miu analog?
 *
 * 0x004 -
 *    15 - 8    |    7 - 0
 * dqs waveform | clock waveform
 * 0xaa - x8?   | 0xaa - x8?
 * 0xcc - x4?   | 0xcc - x4?
 *
 * 0x1f202400
 * In the MSB2521 datasheet this is called MIU_DIG, miu digital?
 *
 * 0x008 - config2
 * |   4 - 0
 * | rd timing
 * | 0xD
 *
 * 0x00c - config3
 *
 * 0x010 - config4
 *
 *    15   |    14    | 13 - 8 |    7 - 4  |   3 - 0
 * trp[4]  |  trcd[4] |  trs   |  trp[3:0] | trcd[3:0]
 *    0    |     0    |  0x1e  |  0x9      | 0x9
 *
 * 0x014 - config5
 * 13 - 8 | 7 - 4 | 3 - 0
 *   trc  | trtp  | trrd
 *
 * 0x018 - config6
 * 15 - 12 | 11 - 8 | 7 - 4 | 3 - 0
 *  trtw   |  twtr  |  twr  |  twl
 *
 * 0x01c - config7
 *
 *    15  | 14   | 12 | 11 - 8 | 7 - 0
 * twr[4] | tccd |  txp   | trfc
 *
 * The vendor suspend code writes 0xFFFF to all of these
 * but the first where it writes 0xFFFE instead
 * Presumably this is to stop requests happening while it
 * is putting the memory into low power mode.
 *
 * 0x08c - group 0 request mask
 * 0x0cc - group 1 request mask
 * 0x10c - group 2 request mask
 * 0x14c - group 3 request mask
 *
 * 0x180 - protection 0 start
 * 0x184 - protection 0 end
 * 0x188 - protection 1 start
 * 0x18c - protection 1 end
 * 0x190 - protection 2 start
 * 0x194 - protection 2 end
 * 0x198 - protection 3 start
 * 0x19c - protection 3 end
 * 0x1a0 - protection msb 0 - 3
 * 0x1a4 - protection en / ddr size
 * top bits ddr size?
 * bottom bits protect 0 - 3 en
 * 0x1b4 - protection fault address low
 * 0x1b8 - protection fault address high
 * 0x1bc - protection fault status
 * 14 - 8    | 7 - 5  | 4         | 1        | 0
 * client id | hit no | hit flag? | int mask | clr
 *
 * 0x1f202200
 * This isn't in the MSB2521 datasheet but it looks like a bunch
 * more group registers.
 *
 * The vendor pm code writes 0xFFFF these before messing with
 * the DDR right after the 4 group registers above. Hence my guess
 * is that these are a bunch of strapped on groups.
 *
 * 0x00c - group 4 request mask?
 * 0x04c - group 5 request mask?
 */
 ```
