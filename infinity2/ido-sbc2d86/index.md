# IDO-SBC2D86-V1A

Thiny ssd202d based board with a 4 inch screen.

## Hardware

- SigmaStar SSD202D
- [TG040H02-CT-V 4](https://www.panelook.cn/TG040H02-CT-V1-4inch-TFT-display-720-720-IPS-LCD-450cd-m-sup2-30PINS-MIPI-Square-LCD-detail_107480.html) inch 720 x 720 LCD module.
  - FRD720X720BK 4 inch LCD
  - Goodix touchpanel controller
  - [Init code](https://github.com/wireless-tag-com/openwrt-ssd20x/blob/ad8305b3234bdb2b3207c5c8c3a07696cb3a18df/18.06/package/sigmastar/sstar-init/files/FRD720X720BK/config/LCM/FRD720x720BK_MIPI.ini)
- HYM8563 RTC
- ES7243 - "High Performance Stereo Audio ADC"
- Unisound US516P6
  - LPA4871(?) mono amp
- FS35ND02G - SPI NAND
- SSW101B - Crappy WiFi
- WT5105 - BLE (phyplus62xx series?)
- NS4150B - Audio amp
- SY7201 (DQCRA) - LED driver
- SY6280 (COCPK) - Power switch


## Pins

- GPIO4 - backlight control?
- GPIO5 - backlight control?
- GPIO47?? - vbus control for external usb
- GPIO11 - external usb power control

## Connectors

- J4 i2c is i2c0, shared with RTC.

## Notes

```
# gpioset 0 16=0
[ 1099.114719] usb 1-1: USB disconnect, device number 2
# gpioset 0 16=1
# [ 1177.169962] usb 1-1: new high-speed USB device number 3 using fotg210-hcd
[ 1177.371156] usb 1-1: Dual-Role OTG device on non-HNP port
```
