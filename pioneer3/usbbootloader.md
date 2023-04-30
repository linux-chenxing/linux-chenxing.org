# Pioneer3 usb bootloader

https://github.com/DongshanPI/SigmaStar-USBDownloadTool


```
Bus 001 Device 100: ID 1b20:0300 MStar Semiconductor, Inc.
```

```
[15471429.057780] usb 1-2: new high-speed USB device number 100 using xhci_hcd
[15471429.207229] usb 1-2: New USB device found, idVendor=1b20, idProduct=0300, bcdDevice= 1.00
[15471429.207240] usb 1-2: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[15471429.209402] usb-storage 1-2:1.0: USB Mass Storage device detected
[15471429.209633] scsi host3: usb-storage 1-2:1.0
[15471430.239331] scsi 3:0:0:0: Direct-Access     GCREADER                       PQ: 0 ANSI: 0
[15471430.239662] sd 3:0:0:0: Attached scsi generic sg1 type 0
[15471430.241948] sd 3:0:0:0: [sdc] Media removed, stopped polling
[15471430.242567] sd 3:0:0:0: [sdc] Attached SCSI removable disk
```

## usb_updater.bin

This is an IPL that implements memory configuration and loading a u-boot legacy image via USB.

Load address for the uploaded u-boot image seems to be `23c00000`
