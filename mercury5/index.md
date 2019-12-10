# Mercury 5

The mercury 5 family seems to be targetted at dash recorders. So far all of the devices that have been obtained have been running something that seems to be based on eCOS and not Linux.

The mercury 5 seems to be very close to the [infinity3](/infinity3).

# Specs

- Probably a 800MHz Cortex A7
- 32KB Boot ROM
- 128KB SRAM (based on where the boot rom sets the stack pointer)
- MIPI DSI for an LCD panel
- 1 or 2 MIPI CSI for cameras
- Most if not all of the peripherals from the [infinity3](/infinity3/).

## Chips

### SSC8336

Probably the same chip as the SSC8336N but in QFP instead of QFN. Pinout seems to be identical.

- Chip id: 0xd9

#### Known Devices

##### [Super cheapie ebay mirror dash cam](https://www.ebay.com/itm/9-66-Inch-2-5D-Mirror-Dash-Cam-Backup-Camera-For-Cars-Streaming-Media-Dual-I4D7/264489118570?ssPageName=STRK%3AMEBIDX%3AIT&_trksid=p2060353.m2749.l2649)

- Probably [GT911](https://www.distec.de/fileadmin/pdf/produkte/Touchcontroller/DDGroup/GT911_Datasheet.pdf) touch screen controller.

### SSC8336N

- Chip id: 0xee

#### Pinout

128 Pin QFP/QFN

* this was sourced from a schematic and reverse engineering with a meter. Don't trust it!! *


| #   | name            | #   | name             |
|-----|-----------------|-----|------------------|
| 1   | aud_lineout_lo  | 65  | pada_ctrl        |
| 2   | aud_miccm0      | 66  | avdd_sdio_3318   |
| 3   | aud_micin0      | 67  | sd_d1            |
| 4   | aud_vrm_adc     | 68  | sd_d0            |
| 5   | aud_vag         | 69  | sd_clk           |
| 6   | avdd_aud_3v3    | 70  | sd_cmd           |
| 7   | usb_dm1         | 71  | sd_d3            |
| 8   | usb_dp1         | 72  | sd_d2            |
| 9   | usb_dm          | 73  | camera mipi?     |
| 10  | usb_dp          | 74  | camera mipi?     |
| 11  | avdd_usb_3v3    | 75  | camera mipi?     |
| 12  | usb_cid         | 76  | camera mipi?     |
| 13  | vdd_1v0 - core  | 77  | camera mipi?     |
| 14  | poc_pwr_en      | 78  | camera mipi?     |
| 15  | reset           | 79  | camera mipi?     |
| 16  | vbus_5v         | 80  | camera mipi?     |
| 17  | pwr_key_det     | 81  | camera mipi?     |
| 18  | avdd_poc        | 82  | camera mipi?     |
| 19  | xtal_in_32k     | 83  | vdd_1v0          |
| 20  | avss_xtal_pos   | 84  | psda/sr0_gpio1   |
| 21  | xtal_out_32k    | 85  | psck/sr0_gpio0   |
| 22  | dvdd_nodie      | 86  |                  |
| 23  | avdd_nodie_3v3  | 87  |                  |
| 24  | sar_gpio0       | 88  |                  |
| 25  | sar_gpio1       | 89  |                  |
| 26  | sar_gpio3       | 90  |                  |
| 27  | pm_spi_cz       | 91  | vddp_2_1v8/3v3   |
| 28  | pm_spi_mosi     | 92  |                  |
| 29  | pm_spi_wpz      | 93  |                  |
| 30  | pm_spi_miso     | 94  |                  |
| 31  | pm_spi_ck       | 95  |                  |
| 32  | pm_spi_hold     | 96  |                  | 
| 33  | gnd_efuse       | 97  | ccir1_y2/sr1_d0p |
| 34  | pm_gpio8/dvfs1  | 98  | ccir1_y3/sr1_d0n |
| 35  | pm_gpio6        | 99  | ccir1_y4/sr1_ckp |
| 36  | pm_gpio5        | 100 | ccir1_y5/sr1_ckn |
| 37  | pm_gpio4/sleep  | 101 | ccir1_y6/sr1_d1p |
| 38  | pm_gpio2        | 102 | ccir1_y7/sr1_d1n |
| 39  | pm_gpio0        | 103 | avdd1p2_mipi     |
| 40  | pm_uart_tx      | 104 | lcd_hsync        | 
| 41  | pm_uart_rx      | 105 | lcd_vsync        |
| 42  | pm_irin         | 106 | lcd_pclk         |
| 43  | pm_sd_cdz       | 107 | lcd_de           |
| 44  | avddio_dram_1v8 | 108 | mipi dsi d0p     |
| 45  | vdd_1v0         | 109 | mipi dsi d0n     |
| 46  | avddio_dram_1v8 | 110 | mipi dsi d1p     |
| 47  | vddio_data_1v8  | 111 | mipi dsi d1n     |
| 48  | vddio_data_1v8  | 112 | mipi dsi clkp    |
| 49  | avdd_pll_3v3    | 113 | mipi dsi clkn    |
| 50  | dvdd_ddr_rx     | 114 | mipi dsi d2p     |
| 51  | dvdd_ddr_1v0    | 115 | mipi dsi d2n     |
| 52  | fuart_rx        | 116 | mipi dsi d3p     |
| 53  | fuart_tx        | 117 | mipi dsi d3n     |
| 54  | fuart_cts       | 118 | lcd_d10          |
| 55  | fuart_rts       | 119 | lcd_d11          |
| 56  | spi0_miso       | 120 | lcd_d12          |
| 57  | spi0_mosi       | 121 | lcd_d13          |
| 58  | spi0_ck         | 122 | lcd_d14          |
| 59  | spi0_cz         | 123 | lcd_d15          |
| 60  | spi0_cz1        | 124 | vddp_3_3v3       |
| 61  | i2c0_scl        | 125 | avdd_mipi_3v3    |
| 62  | i2c0_sda        | 126 | avdd_xtal        |
| 63  | vdd_1v0         | 127 | xtal_in          |
| 64  | vddp_1_3v3      | 128 | xtal_out         |

#### Boot ROM Tag

This is slighly interesting. Presumably I3 is infinity3 so maybe this chip's ROM is a hacked up. 

```
MVX1##I3gb83f2cbCMN_ROM######XVM
```

#### Known Devices 

##### 70mai Smart dash cam 

- [vendor page](https://www.70mai.com/en/70mai-dash-cam-lite/?gclid=EAIaIQobChMIzsLkl6y_5QIVEz5gCh1UOg9eEAAYASAAEgLvffD_BwE) 
- [fcc.io internal photos](https://fccid.io/2AOK9-MIDRIVED08/Internal-Photos/internal-photos-4351132)
- injoinc ip6303 pmic on i2c0@0x30 (custom i2c address and default voltages)
- SC7A30E accelerometer on i2c0@0x1d
- [ST7701S](http://www.startek-lcd.com/res/starteklcd/pdres/201705/20170512144242904.pdf) based 480x640 LCD
- Realtek 8188FTV usb wifi, probably RL-UM12BS-8188FTV-V3.0


### SSC8339D
