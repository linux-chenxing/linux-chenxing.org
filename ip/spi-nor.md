# SPI Memory controllers

All known chips contain a set of SPI controllers that are responsible for
driving an SPI NOR or NAND chip connected to the PM SPI pin.

There seems to be one controller called "ISP", another called "FSP" and
finally "QSPI".

There seems to be three ways to *read* flash content:

- By manually sending commands via the ISP like a standard SPI controller.
- By accessing 0x14000000. This triggers a read and the data is visable to the CPU. This seems to be called "XIU" read.
  Which block actually implements this isn't known yet.
- By programming the BDMA controller to do a read from flash directly into system memory.
  Which block actually implements this isn't known yet.
  
There seems to be two ways to *write* flash content:

- By manually sending commands via the ISP like a standard SPI controller.
- By creating command streams that can DMA data from system memory with the FSP.

To make things really fun all of these blocks seem to have their own clock setup:

- ISP - Clock is divided from the CPU source 432MHz clock, doesn't seem to care about the mux at 0x1f2070c8
- FSP - 
- QSPI -

Messing with the clkgen mux at 0x1f2070c8 can break the CPU interface at 0x14000000. BDMA seems to work just fine.

Maybe the hardware looks something like this?

```
 ------
| ISP  |-\
 ------   |   ---------------      -------------------
| FSP  | ----| ?? bus arb ?? | -- | SPI NOR/NAND chip |
 ------   |   ---------------      -------------------
| QSPI |-/
 ------
```



```

 *
 * ISP registers
 *
 * 0x00 - password
 * 0x04 - cmd
 * 0x10 - wdata - data to be written
 * 0x14 - rdata - data to be read
 * 0x18 - clkdiv?
 * 0x20 - ceclr - chip select control
 * 0x30 - rdreq - read trigger
 * 0x54 - rd_datardy - read data poll
 * 0x58 - wr_datardy - write data poll
 * 0x7e - reset
 *   2
 * ~rst
 * 0xa8 - trigger mode
 *
 * 0xfc - rst
 *
 *    2     |
 *   rst    |
 * 0 - rst  |
 * 1 - nrst |
 *
 * FSP
 *
 * The idea of the FSP seems to be to allow fast page writes.
 * You load a page of data into it's buffer, setup some bytes
 * that go before and after it for the flash protocol and then
 * fire the whole lot off.
 *
 * 0x0
 *  .
 *  . Seems to be a 256 byte buffer that is writable by
 *  . the bdma controller
 *  .
 * 0xFF
 *
 * 0x1b0 - ctrl
 *
 * |  3   |    2   |   1  |  0
 * | chk? | int en | ~rst | en
 *
 * 0x1b4 - trigger
 *    0
 * trigger
 *
 * 0x1b8 - status
 *   0
 * done
 *
 * QSPI register
 *
 * 0x01c - pm code: spi_arb_ctrl[1:0]
 * 0x020 - pm code: non_pm_ack_timeout_len[15:0]
 *
 * 0x028 - burst write control
 * 0x1 enable burst
 * 0x2 disable burst
 *
 * 0x150 - wrap val
 *
 * 0x1c0 - ckg spi
 *
 * 0x1c4 - chip select timing
 *
 * 0x1c8 - Read mode
 *
 *        3 - 0
 * val | mode   | spi command
 * 0x0 |        | 0x03
 * 0x1 | fast   | 0x0b
 * 0x2 | 1_1_2  | 0x3b
 * 0x3 | 1_2_2  | 0xbb
 * 0xa | 1_1_4  | 0x6b
 * 0xb | 1_4_4  | 0xeb
 * 0xc |        | 0x0b
 * 0xd | 4eb?   | ?
 *
 * 0x1e8 - chip select
 *
 * 0x1f4 - function select
 *    13   |    12    |    11    |
 * wrap_en | dummy_en | addr2_en |
 */
 ```
