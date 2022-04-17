# USB

## MStar FUSBH200 notes

- Patch series that added support to u-boot:
  - https://www.mail-archive.com/u-boot@lists.denx.de/msg113338.html

- Needs 128 byte alignment for everything?
  - https://github.com/linux-chenxing/linux-ssc325/blob/979122be45d470e959c2245c996fa93dea10069b/drivers/sstar/usb/host/ehci-mstar.h#L220
  - https://github.com/linux-chenxing/linux-ssc325/blob/89341c7012404c72e192f198b2ea6405ec80d15d/drivers/usb/host/ehci-mem.c#L174
