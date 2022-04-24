# USB

 - [EHCI spec from Intel](https://www.intel.com/content/dam/www/public/us/en/documents/technical-specifications/ehci-specification-for-usb.pdf)


## USBC

| offset | name | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | notes |
|--------|------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|---|-------|
|        |      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |       |

## MStar FUSBH200 notes

- Patch series that added support to Linux (later removed..):
  - https://lore.kernel.org/all/1366969040-28892-1-git-send-email-yhchen@faraday-tech.com/

- Patch series that added support to u-boot:
  - https://www.mail-archive.com/u-boot@lists.denx.de/msg113338.html

- Needs 128 byte alignment for everything?
  - https://github.com/linux-chenxing/linux-ssc325/blob/979122be45d470e959c2245c996fa93dea10069b/drivers/sstar/usb/host/ehci-mstar.h#L220
  - https://github.com/linux-chenxing/linux-ssc325/blob/89341c7012404c72e192f198b2ea6405ec80d15d/drivers/usb/host/ehci-mem.c#L174
