# QFN68 Demoboard

## Hardware specs

- SSD210 or SSC9211, seem to be pin to pin compatible.
- SPI NOR
- SPI NAND
- Leadchip LC9226 PMIC (http://www.leadchip.com.cn/productinfo/442517.html)


## Reverse engineering notes

- For the SSC9211 SD card power is connected to "GPIO 24", which is "TTL7" (I think) on the SSD210 diagram.
  gpio register that changes when u-boot toggles it is 0x2d8.
   
