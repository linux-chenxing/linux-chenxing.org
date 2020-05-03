# Pinctrl

[m5](https://github.com/longyanjun2020/SDK_pulbic/blob/47d85255220f39de1b13e5f2a68b24e49e179f07/Mercury5/proj/sc/driver/hal/mercury/kernel/inc/kernel_chiptop.h)

| offset | name           | 15                    | 14    | 13            | 12      | 11            | 10    | 9             | 8           | 7               | 6     | 5               | 4       | 3              | 2       | 1               | 0       |
|--------|----------------|-----------------------|-------|---------------|---------|---------------|-------|---------------|-------------|-----------------|-------|-----------------|---------|----------------|---------|-----------------|---------|
| 0x0c   | uarts          |                       |       |               |         |               |       | UART1         | UART1       |                 |       | UART0           | UART0   |                |         | FUART           | FUART   |
|        |                |                       |       |               |         |               |       | 0x0           |             |                 |       | 0x0             |         |                |         | 0x0 - disabled? |         |
|        |                |                       |       |               |         |               |       | 0x1           |             |                 |       | 0x1             |         |                |         | 0x1 - fuart     |         |
|        |                |                       |       |               |         |               |       | 0x2 - FUART   |             |                 |       | 0x2 - FUART     |         |                |         | 0x2             |         |
|        |                |                       |       |               |         |               |       | 0x3           |             |                 |       | 0x3             |         |                |         | 0x3             |         |
| 0x18   | sr             |                       |       |               |         |               |       |               |             |                 |       | SR I2C?         | SR I2C? |                | SR      | SR              | SR      |
| 0x1c   | pwm            | PWM7                  | PWM7  | PWM6          | PWM6    | PWM5          | PWM5  | PWM4          | PWM4        | PWM3            | PWM3  | PWM2            | PWM2    | PWM1           | PWM1    | PWM0            | PWM0    |
|        |                | 0x0                   |       | 0x0           |         | 0x0           |       | 0x0           |             | 0x0             |       | 0x0             |         | 0x0            |         | 0x0             |         |
|        |                | 0x1                   |       | 0x1           |         | 0x1           |       | 0x1           |             | 0x1             |       | 0x1             |         | 0x1            |         | 0x1             |         |
|        |                | 0x2 - spi0_do         |       | 0x2 - spi0_di |         | 0x2 - spi0_ck |       | 0x2 - spi0_cz |             | 0x2 - fuart_rts |       | 0x2 - fuart_cts |         | 0x2            |         | 0x2             |         |
|        |                | 0x03                  |       | 0x3           |         | 0x3           |       | 0x3           |             | 0x3             |       | 0x3             |         | 0x3 - fuart_tx |         | 0x3 -fuart_rx   |         |
| 0x20   | sd/sdio/nand   |                       |       |               |         |               |       |               | SDIO        |                 |       |                 |         |                |         |                 |         |
|        |                |                       |       |               |         |               |       |               | 0x0         |                 |       |                 |         |                |         |                 |         |
|        |                |                       |       |               |         |               |       |               | 0x1 - sdio  |                 |       |                 |         |                |         |                 |         |
| 0x24   | i2c            |                       |       |               |         |               |       |               |             |                 |       | I2C1            | I2C1    |                |         | IC20            | IC20    |
|        |                |                       |       |               |         |               |       |               |             |                 |       | 0x0             |         |                |         | 0x0             |         |
|        |                |                       |       |               |         |               |       |               |             |                 |       | 0x1 - i2c1      |         |                |         | 0x1 - i2c0      |         |
| 0x30   | spi            |                       |       |               |         |               |       |               |             |                 |       | SPI1            | SPI1    |                |         | SPI0            | SPI0    |
|        |                |                       |       |               |         |               |       |               |             |                 |       |                 |         |                |         | 0x0             |         |
|        |                |                       |       |               |         |               |       |               |             |                 |       |                 |         |                |         | 0x1             |         |
|        |                |                       |       |               |         |               |       |               |             |                 |       |                 |         |                |         | 0x2             |         |
|        |                |                       |       |               |         |               |       |               |             |                 |       |                 |         |                |         | 0x3 - fuart     |         |
| 0xcc   | FUART conf     |                       |       | pull up       | pull up |               |       | pull enable   | pull enable |                 |       | ie?             | ie?     |                |         | drive           | drive   |
| 0xd4   | drive strength |                       |       |               |         |               |       | UART1         | UART1       |                 |       | UART0           | UART0   |                |         |                 | PWM0    |
| 0x140  |                | set all pins as input |       |               |         |               |       |               |             |                 |       |                 |         |                |         |                 |         |
| 0x14c  | uart sel       | UART1                 | UART1 | UART1         | UART1   | UART0         | UART0 | UART0         | UART0       | FUART           | FUART | FUART           | FUART   | PM_UART        | PM_UART | PM_UART         | PM_UART |

```
 * These might be internal dram pins
 * 0xe0 - ipl sets to 0xffff
 * 0xe4 - ipl sets to 0x3
 * 0xe8 - ipl sets to 0xffff
 * 0xec - ipl sets to 0x3
 * 0xf0 - ipl sets to 0
 * 0xf4 - ipl sets to 0
 ```
 Wrong ... seems resetting the sensor pads.


```
/*
 * There seems to be one main pinmux block in the chip at 0x1f203C00.
 * It looks like it controls the pins on a group basis and not by
 * selecting a function per pin.
 *
 * A pin becomes GPIO if all of the different functions that can be applied to the
 * pin are disabled.
 *
 * 0x24 - I2C
 * For mercury5 the i2c1 setting here doesn't seem to actually
 * do anything
 *
 * 0x3c - JTAG, ETHERNET (TTL, CCIR)
 * 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 |        2        | 1 0
 * ?  | 0 | ? | 0 | ? | 0 | ? | 0 |    ETHERNET     | JTAG
 *                                  0x0 - disabled? | 0x0 - disabled ?
 *                                                  | 0x1 - fuart
 *                                                  | 0x2 - spi0
 *                                                  | 0x3 - ??
 *
 * - Toggling bits doesn't stop ethernet working :/
 *
 * 0x48 TEST_IN, TEST_OUT
 *
 * 0xC0 - nand drive
 * 0xC4 - nand pull up
 *
 * 0xC8 - SD/SDIO pull up/down, drive strength? rst : 0x0, can write 0x1f3f
 *         12 - 8       |           5 - 0
 *        pull en?      |          drv: 0?
 *  d3, d2, d1, d0, cmd | clk, d3, d2, d1, d0, cmd
 *

 *
 * Mercury 5 notes:
 *
 * Offsets from dashcam app
 *
 *
 * 0x3c - I2S/DMIC/TTL/CCIR
 * 0x4c - EMMC
 * 0x50 - SPI2/SD30/RGB_8B/RGB_24B/
 *
 * 0x54 - Sensor config
 *
 * setting to 0x4000 makes another i2c device visible on mirrorcam
 *
 *     15 - 13    |      12        |     11 - 10       |     9 - 8     |     6 - 4      |     2 - 0
 *  sr1 mipi mode | sr1 bt656 mode | sr0 parallel mode | sr0 mipi mode | sr0 bt656 mode | sr0 bt601 mode
 *                |                |                   |               |                |
 *
 * 0x58 - TX_MIPI
 *    1 - 0
 * tx mipi mode
 *
 * reset - 0x900
 *
 * 11 - 10 | 9 - 8 |  1 - 0
 *  i2c3   | i2c2  | tx mipi
 *
 * 0x5c - I2C1_DUAL
 *
 * default 0x42
 * can write 0xf7
 *
 * | 2 - 1
 * | i2c1 mode?
 *
 */
 ```
 
