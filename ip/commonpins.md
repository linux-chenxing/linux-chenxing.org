# Common pins

## PM_RESET

This is the global reset.
This is active *high*. The reference circuit for this shows a 10uF capacitor and 10K resistor
connected in series with PM_RESET connected at their connecting point.
The capacitor is tied to 3.3v and the resistor to ground. So the capacitor should start
charged at 3.3v and get discharged via the resistor.

## PM_UART_TX
## PM_UART_RX

This is the default UART that is used by the internal boot rom, u-boot and the kernel.
The weird thing about these pins is that there is actually a i2c slave device connected to them too!
The i2c device allows SPI NOR or SPI NAND to be updated. See the [isp page](/isp/) for more details.

These pins can also be mux'd between uart0 and "hk uart" which should be the uart for the 8051
micro controller.

## PM_LED0
## PM_LED1

These are generally used for the ethernet indicator LEDs.

## PWM0
## PWM1
## PWM3
## PWM4
## PWM5
## PWM6
## PWM7

PWM pins.

## UART1_RX

## UART1_TX

## SPI0_CZ
## SPI0_CK
## SPI0_DI
## SPI0_DO
