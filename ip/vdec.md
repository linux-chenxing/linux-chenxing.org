# VDEC

```
/ # lsmod 
ssw101b_wifi_usb 636083 0 - Live 0xbfc81000 (O)
fbdev 28812 1 - Live 0xbfc74000 (PO)
mi_panel 21946 0 - Live 0xbfc6a000 (O)
mi_venc 136738 0 - Live 0xbfc3e000 (PO)
mi_disp 93828 0 - Live 0xbfc20000 (PO)
mi_ipu 18078 0 - Live 0xbfc16000 (O)
mi_ai 196616 0 - Live 0xbfbde000 (PO)
mi_vdec 1245049 0 - Live 0xbfaa5000 (PO)
mi_divp 41827 1 mi_vdec, Live 0xbfa95000 (PO)
mi_gfx 14540 1 mi_disp, Live 0xbfa8d000 (PO)
mi_ao 73331 0 - Live 0xbfa75000 (PO)
mi_sys 838869 10 fbdev,mi_panel,mi_venc,mi_disp,mi_ipu,mi_ai,mi_vdec,mi_divp,mi_gfx,mi_ao, Live 0xbf996000 (PO)
mi_common 5003 15 fbdev,mi_panel,mi_venc,mi_disp,mi_ipu,mi_ai,mi_vdec,mi_divp,mi_gfx,mi_ao,mi_sys, Live 0xbf991000 (PO)
mhal 456760 10 fbdev,mi_panel,mi_venc,mi_disp,mi_ai,mi_vdec,mi_divp,mi_gfx,mi_ao,mi_sys, Live 0xbf8fc000 (PO)
mdrv_crypto 21058 0 - Live 0xbf8f1000
usb_storage 35243 0 - Live 0xbf8e4000
ehci_hcd 32980 0 - Live 0xbf8d7000
ntfs 71321 0 - Live 0xbf8bf000
vfat 6480 0 - Live 0xbf8ba000
msdos 5294 0 - Live 0xbf8b5000
fat 39114 2 vfat,msdos, Live 0xbf8a6000
nfsv2 10548 0 - Live 0xbf89f000
nfs 92631 1 nfsv2, Live 0xbf87d000
lockd 35766 2 nfsv2,nfs, Live 0xbf86e000
sunrpc 146463 3 nfsv2,nfs,lockd, Live 0xbf83c000
grace 2219 1 lockd, Live 0xbf838000
nls_utf8 1380 0 - Live 0xbf834000
cifs 163903 0 - Live 0xbf800000
/ # Sending discover...
No lease, forking to background
/ # cat /proc/interrupts 
           CPU0       CPU1       
 20:       3690       3898     GIC-0  27 Level     arch_timer
 27:         20          0  MS_MAIN_INTC  57 Level     mi_GE_ISR
 30:        689          0  MS_MAIN_INTC  66 Level     ms_serial
 35:          0          0  MS_MAIN_INTC  58 Level     eth0
 37:          0          0  MS_MAIN_INTC  84 Level     eth1
 39:       3066          0  MS_MAIN_INTC  87 Level     ehci_hcd:usb2
 40:          0          0  MS_MAIN_INTC  65 Level     ehci_hcd:usb1
 43:          0          0  MS_MAIN_INTC  51 Level     ms_sdmmc_mie
 44:          0          0  MS_MAIN_INTC 119 Edge      ms_sdmmc_cdz
 47:          0          0  MS_MAIN_INTC  73 Level     BdmaIsr
 48:          0          0  MS_MAIN_INTC  93 Level     BdmaIsr
 49:          0          0  MS_MAIN_INTC  94 Level     BdmaIsr
 50:          0          0  MS_MAIN_INTC  92 Level     HalMoveDma_ISR
 55:          0          0  MS_MAIN_INTC  81 Level     MIU_Protect
 57:       2162          0  MS_MAIN_INTC  52 Level     mi_disp_isr, fbdev_dispVsync
 58:       6383          0  MS_MAIN_INTC  82 Level     mdisp_interisr
 60:          4          0  MS_GPI_INTC  58 Edge      gt911
IPI0:          0          1  CPU wakeup interrupts
IPI1:          0          0  Timer broadcast interrupts
IPI2:        989       4091  Rescheduling interrupts
IPI3:          2         13  Function call interrupts
IPI4:          0          0  CPU stop interrupts
IPI5:         42        358  IRQ work interrupts
IPI6:          0          0  completion interrupts
Err:          0
/ # random: crng init done
```
