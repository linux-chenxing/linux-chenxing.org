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

```
/ # cat /proc/interrupts 
           CPU0       CPU1       
 20:      13025      12653     GIC-0  27 Level     arch_timer
 26:        544          0  MS_MAIN_INTC  53 Level     mi_vdec_isr
 27:         53          0  MS_MAIN_INTC  57 Level     mi_GE_ISR
 30:       1189          0  MS_MAIN_INTC  66 Level     ms_serial
 35:          0          0  MS_MAIN_INTC  58 Level     eth0
 37:          0          0  MS_MAIN_INTC  84 Level     eth1
 39:       4119          0  MS_MAIN_INTC  87 Level     ehci_hcd:usb2
 40:          0          0  MS_MAIN_INTC  65 Level     ehci_hcd:usb1
 42:        344          0  MS_MAIN_INTC  74 Level     aio_dma1
 43:          0          0  MS_MAIN_INTC  51 Level     ms_sdmmc_mie
 44:          0          0  MS_MAIN_INTC 119 Edge      ms_sdmmc_cdz
 47:          0          0  MS_MAIN_INTC  73 Level     BdmaIsr
 48:          0          0  MS_MAIN_INTC  93 Level     BdmaIsr
 49:          0          0  MS_MAIN_INTC  94 Level     BdmaIsr
 50:          0          0  MS_MAIN_INTC  92 Level     HalMoveDma_ISR
 55:          0          0  MS_MAIN_INTC  81 Level     MIU_Protect
 57:       7838          0  MS_MAIN_INTC  52 Level     mi_disp_isr, fbdev_dispVsync
 58:      23410          0  MS_MAIN_INTC  82 Level     mdisp_interisr
 60:         10          0  MS_GPI_INTC  58 Edge      gt911
IPI0:          0          1  CPU wakeup interrupts
IPI1:          0          0  Timer broadcast interrupts
IPI2:       3533      11549  Rescheduling interrupts
IPI3:          2         13  Function call interrupts
IPI4:          0          0  CPU stop interrupts
IPI5:        286       1060  IRQ work interrupts
IPI6:          0          0  completion interrupts
Err:          0
```

```
/ # dmesg 
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 30
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 31
[emac_phy_connect][3179] connected mac emac0 to PHY at mdio-bus@emac0:00 [uid=11112222, driver=SStar 10/100 Ethernet Phy]
MSYS: DMEM request: [emac1_buff]:0x00060812
cma: cma_alloc(cma c047cef0, count 97, align 4)
cma: cma_alloc(): returned c417ca00
MSYS: DMEM request: [emac1_buff]:0x00060812 success, CPU phy:@0x24250000, virt:@0xC4250000
libphy: mdio: probed
mdio_bus mdio-bus@emac1: /soc/emac1/mdio-bus@emac1/ethernet-phy@1 has invalid PHY address
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 0
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 1
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 2
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 3
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 4
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 5
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 6
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 7
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 8
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 9
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 10
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 11
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 12
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 13
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 14
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 15
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 16
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 17
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 18
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 19
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 20
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 21
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 22
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 23
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 24
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 25
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 26
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 27
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 28
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 29
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 30
mdio_bus mdio-bus@emac1: scan phy ethernet-phy at address 31
[emac_phy_connect][3179] connected mac emac1 to PHY at mdio-bus@emac1:00 [uid=00000000, driver=Generic PHY]
[ms_cpufreq_init] Current clk=1005326304
mstar_spinand_probe: mstar_spinand enableClock
MSYS: DMEM request: [BDMA]:0x00000840
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c8c0
MSYS: DMEM request: [BDMA]:0x00000840 success, CPU phy:@0x24246000, virt:@0xC4246000
MDrv_SPINAND_Init: Detected ID: MID =cd, DID =ea
_dumpNandInformation:warning, Bytes / Page :  2048
_dumpNandInformation:warning, Pages / Block:  64
_dumpNandInformation:warning, Sector/ Page :  512
_dumpNandInformation:warning, Spare / Page :  64
_dumpNandInformation:warning, Current config r:4 w:4 drv:1
mstar_spinand_probe: Magic memcmp pass
mstar_spinand_probe: Get partition (Block 0 : page 1)
mstar_spinand_probe: CIS contains part info
mstar_spinand_probe: Before nand_scan()...
12 cmdlinepart partitions found on MTD device nand0
mstar_spinand_probe: Mtd parts parse
Creating 12 MTD partitions on "nand0":
0x000000140000-0x0000001a0000 : "IPL0"
0x0000001a0000-0x000000200000 : "IPL1"
0x000000200000-0x000000260000 : "IPL_CUST0"
0x000000260000-0x0000002c0000 : "IPL_CUST1"
0x0000002c0000-0x000000380000 : "UBOOT0"
0x000000380000-0x000000440000 : "UBOOT1"
0x000000440000-0x0000004a0000 : "ENV0"
0x0000004a0000-0x0000004c0000 : "KEY_CUST"
0x0000004c0000-0x000000520000 : "LOGO"
0x000000520000-0x000000a20000 : "KERNEL"
0x000000a20000-0x000000f20000 : "RECOVERY"
0x000000f20000-0x000008000000 : "UBI"
NET: Registered protocol family 17
ThumbEE CPU extension supported.
Registering SWP/SWPB emulation handler
ubi0: attaching mtd11
ubi0: scanning is finished
ubi0: attached mtd11 (name "UBI", size 112 MiB)
ubi0: PEB size: 131072 bytes (128 KiB), LEB size: 126976 bytes
ubi0: min./max. I/O unit sizes: 2048/2048, sub-page size 2048
ubi0: VID header offset: 2048 (aligned 2048), data offset: 4096
ubi0: good PEBs: 892, bad PEBs: 11, corrupted PEBs: 0
ubi0: user volume: 4, internal volumes: 1, max. volumes count: 128
ubi0: max/mean erase counter: 34/9, WL threshold: 4096, image sequence number: 0
ubi0: available PEBs: 2, total reserved PEBs: 890, PEBs reserved for bad PEB handling: 9
ubi0: background thread "ubi_bgt0d" started, PID 637
hctosys: unable to open rtc device (rtc0)
OF: fdt:not creating '/sys/firmware/fdt': CRC check failed
UBIFS (ubi0:0): UBIFS: mounted UBI device 0, volume 0, name "rootfs", R/O mode
UBIFS (ubi0:0): LEB size: 126976 bytes (124 KiB), min./max. I/O unit sizes: 2048 bytes/2048 bytes
UBIFS (ubi0:0): FS size: 9269248 bytes (8 MiB, 73 LEBs), journal size 1650688 bytes (1 MiB, 13 LEBs)
UBIFS (ubi0:0): reserved for root: 0 bytes (0 KiB)
UBIFS (ubi0:0): media format: w4/r0 (latest is w4/r0), UUID 24C8444B-5830-493E-A1EB-4C81FBFF0F24, small LPT model
VFS: Mounted root (ubifs filesystem) readonly on device 0:13.
devtmpfs: mounted
This architecture does not have kernel memory protection.
UBIFS (ubi0:1): background thread "ubifs_bgt0_1" started, PID 658
UBIFS (ubi0:1): recovery needed
UBIFS (ubi0:1): recovery completed
UBIFS (ubi0:1): UBIFS: mounted UBI device 0, volume 1, name "miservice"
UBIFS (ubi0:1): LEB size: 126976 bytes (124 KiB), min./max. I/O unit sizes: 2048 bytes/2048 bytes
UBIFS (ubi0:1): FS size: 9269248 bytes (8 MiB, 73 LEBs), journal size 1650688 bytes (1 MiB, 13 LEBs)
UBIFS (ubi0:1): reserved for root: 0 bytes (0 KiB)
UBIFS (ubi0:1): media format: w4/r0 (latest is w4/r0), UUID DF855D67-FE10-48FD-84FA-8EDC80F07EEE, small LPT model
UBIFS (ubi0:2): background thread "ubifs_bgt0_2" started, PID 661
UBIFS (ubi0:2): recovery needed
UBIFS (ubi0:2): recovery completed
UBIFS (ubi0:2): UBIFS: mounted UBI device 0, volume 2, name "customer"
UBIFS (ubi0:2): LEB size: 126976 bytes (124 KiB), min./max. I/O unit sizes: 2048 bytes/2048 bytes
UBIFS (ubi0:2): FS size: 80629760 bytes (76 MiB, 635 LEBs), journal size 9023488 bytes (8 MiB, 72 LEBs)
UBIFS (ubi0:2): reserved for root: 0 bytes (0 KiB)
UBIFS (ubi0:2): media format: w4/r0 (latest is w4/r0), UUID 0A27D925-C95F-4A15-B0AE-918A15225BF1, small LPT model
UBIFS (ubi0:3): background thread "ubifs_bgt0_3" started, PID 664
UBIFS (ubi0:3): recovery needed
UBIFS (ubi0:3): recovery completed
UBIFS (ubi0:3): UBIFS: mounted UBI device 0, volume 3, name "appconfigs"
UBIFS (ubi0:3): LEB size: 126976 bytes (124 KiB), min./max. I/O unit sizes: 2048 bytes/2048 bytes
UBIFS (ubi0:3): FS size: 4063232 bytes (3 MiB, 32 LEBs), journal size 1142785 bytes (1 MiB, 8 LEBs)
UBIFS (ubi0:3): reserved for root: 0 bytes (0 KiB)
UBIFS (ubi0:3): media format: w4/r0 (latest is w4/r0), UUID 312E1BDB-1EBB-47C0-A091-9519BF86C5BA, small LPT model
RPC: Registered named UNIX socket transport module.
RPC: Registered udp transport module.
RPC: Registered tcp transport module.
RPC: Registered tcp NFSv4.1 backchannel transport module.
ntfs: driver 2.1.32 [Flags: R/O MODULE].
ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
Mstar_ehc_init version:20180309
Sstar-ehci-2 H.W init
Titania3_series_start_ehc start
[USB] config miu select [70] [e8] [ef] [ef]
[USB] enable miu lower bound address subtraction
[USB] init squelch level 0x2
[USB] no platform_data, device tree coming
[USB][EHC] dma coherent_mask 0xffffffffffffffff mask 0xffffffffffffffff
BC disable 
[USB] soc:Sstar-ehci-2 irq --> 40
Sstar-ehci-2 soc:Sstar-ehci-2: EHCI Host Controller
Sstar-ehci-2 soc:Sstar-ehci-2: new USB bus registered, assigned bus number 1
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c8e0
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c900
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c920
Sstar-ehci-2 soc:Sstar-ehci-2: irq 40, io mem 0xfd285000
usb usb1: New USB device found, idVendor=1d6b, idProduct=0002
usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
usb usb1: Product: EHCI Host Controller
usb usb1: Manufacturer: Linux 4.9.84 ehci_hcd
usb usb1: SerialNumber: mstar
hub 1-0:1.0: USB hub found
hub 1-0:1.0: 1 port detected
Sstar-ehci-1 H.W init
Titania3_series_start_ehc start
[USB] config miu select [70] [e8] [ef] [ef]
[USB] enable miu lower bound address subtraction
[USB] init squelch level 0x2
[USB] no platform_data, device tree coming
[USB][EHC] dma coherent_mask 0xffffffffffffffff mask 0xffffffffffffffff
BC disable 
[USB] soc:Sstar-ehci-1 irq --> 39
Sstar-ehci-1 soc:Sstar-ehci-1: EHCI Host Controller
Sstar-ehci-1 soc:Sstar-ehci-1: new USB bus registered, assigned bus number 2
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c940
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c960
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c980
Sstar-ehci-1 soc:Sstar-ehci-1: irq 39, io mem 0xfd284800
usb usb2: New USB device found, idVendor=1d6b, idProduct=0002
usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1
usb usb2: Product: EHCI Host Controller
usb usb2: Manufacturer: Linux 4.9.84 ehci_hcd
usb usb2: SerialNumber: mstar
hub 2-0:1.0: USB hub found
hub 2-0:1.0: 1 port detected
usbcore: registered new interface driver usb-storage
MSYS: DMEM request: [AESDMA_ENG]:0x00001000
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c9a0
MSYS: DMEM request: [AESDMA_ENG]:0x00001000 success, CPU phy:@0x2424D000, virt:@0xC424D000
MSYS: DMEM request: [AESDMA_ENG1]:0x00001000
cma: cma_alloc(cma c047cef0, count 1, align 0)
cma: cma_alloc(): returned c417c9c0
MSYS: DMEM request: [AESDMA_ENG1]:0x00001000 success, CPU phy:@0x2424E000, virt:@0xC424E000
mhal: loading out-of-tree module taints kernel.
mhal: module license 'PROPRIETARY' taints kernel.
Disabling lock debugging due to kernel taint
mhal driver init
jpe driver probed
DivpProcInit 514
==20180309==> hub_port_init 1 #0
Plug in USB Port1
module [sys] init
MI_SYSCFG_SetupMmapLoader default_config_path:/config/config_tool, argv1:/config/load_mmap,argv2:/config/mmap.ini
Function = init_glob_miu_kranges, Line = 603, Insert KProtect for LX @ MIU: 0
Function = init_glob_miu_kranges, Line = 612, [INIT] for LX0 kprotect: from 0x20000000 to 0x27F00000, using block 0
config...... strPath:/config/config_tool, argv0:/config/load_config
function:parese_Cmdline,pCmd_Section:0x7f00000
m
m
a
_
h
e
a
p
_
n
a
m
e
0
    miu=0,sz=3800000  reserved_start=24400000
r_front->miuBlockIndex:0,r_front->start_cpu_bus_pa:0x20000000,r_front->start_cpu_bus_pa+r_front->length:0x24400000
r_back->miuBlockIndex:1,r_back->start_cpu_bus_pa:0x27c00000,r_back->start_cpu_bus_pa+r_back->length:0x27f00000
mi_sys_mma_allocator_create success, heap_base_addr=24400000 length=3800000 
Kernel CONFIG_HZ = 100
Sigmastar Module version: project_commit.7a28b51 sdk_commit.666f5ba build_time.20200513154737
module [ao] init
module [gfx] init
GE_EnableDynaClkGate
 MI_Moduledev_RegisterDev  
module [divp] init
usb 2-1: new high-speed USB device number 2 using Sstar-ehci-1
module [vdec] init
module [ai] init
drv_ccif_cpu_init :c8580000
 
request_irq failed
module [disp] init
module [venc] init May 13 2020 15:48:06
module [panel] init
[FB_DEVICE]
FB_HWLAYER_ID=1
FB_HWWIN_ID=0
FB_HWLAYER_DST=3
FB_HWWIN_FORMAT=5
FB_HWLAYER_OUTPUTCOLOR=1
FB_WIDTH=800
FB_HEIGHT=480
FB_TIMMING_WIDTH=1920
FB_TIMMING_HEIGHT=1080
FB_MMAP_NAME=E_MMAP_ID_FB
FB_BUFFER_LEN=4096

Mstar frame buffer device,numFbHwlayer:1


fb0 parse_hwLayerInfo can not find mmap E_MMAP_ID_FB, alloc fb buffer from mma = 4194304


fb0 parse_hwLayerInfo buffercount=2,sstar_fb_var_infos[seq].yres_virtual=960

[GOP]HalGopUpdateGwinParam 719: GOP_id=011 not support
[GOP]HalGopSetArgb1555Alpha 1207: GOPId=0x11 not support
[GOP]HalGopSetArgb1555Alpha 1207: GOPId=0x11 not support

MI_Moduledev_RegisterDev Enter


gGfxDevHdl = c856f000.


fb0: Mstar frame buffer device

[ss_gpi_intc_domain_alloc] hw:57 -> v:61
client [795] connected, module:sys
client [795] connected, module:disp
[MI_SYSCFG_GetPanelInfo 49] eTiming = 4, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 2, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 8, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 9, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 10, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 6, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 7, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 11, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 13, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 12, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 14, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 5, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 3, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 38, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 50, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 40, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 43, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 41, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 44, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 42, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 46, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 50, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 45, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 50, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 22, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 23, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 30, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 32, hdmiTx = 1  Not Fund!!!
client [795] connected, module:panel
[MI_PANEL_IMPL_Init][504]success
[MI_PANEL_IMPL_GPIO_Init][1166]bl:65535 rst:65535 scl:9 sdo:11 cs:8 en:65535
random: fast init done

sstar_fb_open fb:0 info->fix.smem_start = 0x4421000,user=1


screen_base:c9680000

Freeing fb memory: 3072K

sstar_FB_SetBlending 415 u8GOP=1,u8win=0 aType=1 u8constAlpha=255


sstar_fb_release fb:0 user=1,par->ref_count=1


sstar_fb_open fb:0 info->fix.smem_start = 0x4421000,user=1


screen_base:c9b00000


sstar_FB_SetBlending 415 u8GOP=1,u8win=0 aType=1 u8constAlpha=255


sstar_fb_release fb:0 user=1,par->ref_count=1


sstar_fb_open fb:0 info->fix.smem_start = 0x4421000,user=1


screen_base:c9f80000


sstar_FB_SetBlending 415 u8GOP=1,u8win=0 aType=1 u8constAlpha=255


sstar_fb_mmap vma->vm_start=b5a00000
 vma->vm_end=b5e00000
 vma->vm_pgoff =24421

client [798] connected, module:gfx
[Sstar_log]:Sstar_usb_module_init 0
[Sstar_log]:Sstar_init_firmware
[Sstar_log]:xxxx minstrel ht init
[Sstar_log]:SVN_VER=14606,DPLL_CLOCK=2,BUILD_TIME=[===USB-ARES_B==
usbcore: registered new interface driver Sstar_wlan
[Sstar_log]:[wtd] register.
usb 2-1: device descriptor read/64, error -110
client [798] connected, module:vdec
[MI WRN ]: MI_VDEC_IMPL_Init[6992]: Already Init

[WRN]: MI_VDEC_IMPL_CreateChn:7092 pts:18558 Create Vdec Chn 0.

[WRN]: _MI_VDEC_IMPL_LoadFirmware:1280 pts:18558 Load FW:/config/vdec_fw/normal/chagall.bin

[VPU INFO]: vdi_allocate_common_memory:637:[VDI] vdi_get_common_memory physaddr=0x5034000, size=1755136, virtaddr=0xca480000

[VPU INFO]: vdi_init:336:[VDI] success to init driver 

[VPU INFO]: Wave5VpuInit:331:
VPU INIT Start!!!

[VPU INFO]: PrintVpuProductInfo:81:VPU coreNum : [0]

[VPU INFO]: PrintVpuProductInfo:82:Firmware : CustomerCode: 0000 | version : rev.73552180

[VPU INFO]: PrintVpuProductInfo:83:Hardware : 0007

[VPU INFO]: PrintVpuProductInfo:84:API      : 5.5.51


[VPU INFO]: PrintVpuProductInfo:87:productId       : 00000007

[VPU INFO]: PrintVpuProductInfo:88:fwVersion       : 04625134(r73552180)

[VPU INFO]: PrintVpuProductInfo:91:productName     : WAVE5110

[VPU INFO]: PrintVpuProductInfo:166:==========================

[VPU INFO]: PrintVpuProductInfo:167:stdDef0          : 80cf0980

[VPU INFO]: PrintVpuProductInfo:168:stdDef1          : 08018001

[VPU INFO]: PrintVpuProductInfo:169:confFeature      : 00000103

[VPU INFO]: PrintVpuProductInfo:170:configDate       : 0133f0de

[VPU INFO]: PrintVpuProductInfo:171:configRevision   : 00027a8a

[VPU INFO]: PrintVpuProductInfo:172:configType       : 00000102

[VPU INFO]: PrintVpuProductInfo:173:==========================

[WRN]: MI_VDEC_IMPL_CreateChn:7196 pts:18585 Finish Create Vdec Chn 0.

[WRN]: MI_VDEC_IMPL_StartChn:7307 pts:18586 Start Chn(0)

[WRN]: MI_VDEC_IMPL_StartChn:7377 pts:18588 Start Chn(0) mapchn: 0, instIndex: 0.

[WRN]: MI_VDEC_IMPL_StartChn:7394 pts:18588 Finish Start Chn(0).

client [798] connected, module:ao
[AUDIO ERROR]DrvAudApiDtsInit, IS_MHAL_SUPPORT_ES_CODEC=0.
[_MI_AO_Init:1235] Init Ao Gain.
[WRN]: _MI_VDEC_IMPL_AllocateDecFrameBuffer:1680 pts:18648 chn:0, allocate fb, fbAllocated:0, instIndex:0

[WRN]: _MI_VDEC_IMPL_AllocateDecFrameBuffer:1885 pts:18648 chn:0, allocate fb, fbAllocated:1, instIndex:0

[MI_AO_IMPL_SendFrame:2630] Strat pcm out success!!!
usb 2-1: device descriptor read/64, error -110
hub_port_disable: 1  hub->err: 0 
==20180309==> hub_port_init 1 #1
Plug in USB Port1
Reduce wait reset time to 20
usb 2-1: new high-speed USB device number 3 using Sstar-ehci-1
Reduce wait reset time to 20
usb 2-1: New USB device found, idVendor=1b20, idProduct=8888
usb 2-1: New USB device strings: Mfr=16, Product=32, SerialNumber=0
usb 2-1: Product: SigmaStarWIFI
usb 2-1: Manufacturer: SigmaStar inc
[Sstar_log]:Probe called
[Sstar_log]:CONFIG_USE_DMA_ADDR_BUFFER TX_BUFFER_SIZE 800
[Sstar_log]:CONFIG_USB_AGGR_URB_TX enable cnt tx_dma_addr_buffer_end(  (null))tx_dma_addr_buffer(  (null)),0
[Sstar_log]:Sstar_usb_urb_malloc CONFIG_USE_DMA_ADDR_BUFFER max_num 4, total 131072
cma: cma_alloc(cma c047cef0, count 32, align 4)
cma: cma_alloc(): returned c417d800
[Sstar_log]:CONFIG_USB_AGGR_URB_TX enable cnt tx_dma_addr_buffer_end(c42c0000)tx_dma_addr_buffer(c42e0000),8
[Sstar_log]:CONFIG_TX_NO_CONFIRM
[Sstar_log]:self->tx_hwChanId 0
[Sstar_log]:Allocated hw_priv @ c26b70a0
[Sstar_log]:Sstarwifi USB_USE_TASTLET_TXRX enable
[Sstar_log]:Sstar_before_load_firmware++
[Sstar_log]:+++++++++++++++++1.1v++++++++++++++++++
[Sstar_log]:===================~_~====================
[Sstar_log]:Sstar_start_load_firmware++
[Sstar_log]:Sstar_start_load_firmware: used firmware.h=
[Sstar_log]:Sstar_set_firmare:fw_iccm(c854a000)
[Sstar_log]:Sstar_set_firmare:fw_dccm(c8d94000)
[Sstar_log]:Sstar_start_load_firmware: START DOWNLOAD ICCM=========
[Sstar_log]:Sstar_load_firmware_generic: addr 10000: len 20000
[Sstar_log]:Sstar_start_load_firmware: START DOWNLOAD DCCM=========
[Sstar_log]:Sstar_load_firmware_generic: addr 800000: len 8000
[Sstar_log]:Sstar_after_load_firmware++
[Sstar_log]:Sstar_after_load_firmware:0x1610102c=0x4020e
[Sstar_log]:Sstar_after_load_firmware:0x1610102c=0x1020f
[Sstar_log]:Sstar_after_load_firmware:0x16101000=0x8000e08
[Sstar_log]:set_block_size=256
[Sstar_log]:firmwareCap f58f
[Sstar_log]:firmwareCap2 888f
[Sstar_log]:wsm_caps.firmwareCap 888ff58f
[Sstar_log]:apollo wifi WSM init done.
   Input buffers: 32 x 2048 bytes
   Hardware: 7.2
   WSM firmware [=MODEM=RF=Ares_AX  2GHZ Dec 24 2019 19:59:25NOTXConfrim], ver: 8677, build: 2690, api: 1060, cap: 0x888FF58F Config[30008]  expection 900a5c0, ep0 cmd addr 901be2c NumOfS][Sstar_log]:EFUSE(8)                            [0]
[Sstar_log]:EFUSE(I)                                    [0]
[Sstar_log]:EFUSE(B)                    [1]
[Sstar_log]:CAPABILITIES_SSTAR_PRIVATE_IE      [1]
[Sstar_log]:CAPABILITIES_NVR_IPC              [1]
[Sstar_log]:CAPABILITIES_NO_CONFIRM           [1]
[Sstar_log]:CAPABILITIES_SDIO_PATCH           [0]
[Sstar_log]:CAPABILITIES_NO_BACKOFF           [0]
[Sstar_log]:CAPABILITIES_CFO                  [0]
[Sstar_log]:CAPABILITIES_AGC                  [1]
[Sstar_log]:CAPABILITIES_TXCAL                [1]
[Sstar_log]:CAPABILITIES_MONITOR              [0]
[Sstar_log]:CAPABILITIES_CUSTOM               [1]
[Sstar_log]:CAPABILITIES_SMARTCONFIG          [0]
[Sstar_log]:CAPABILITIES_ETF                  [1]
[Sstar_log]:CAPABILITIES_LMAC_RATECTL         [1]
[Sstar_log]:CAPABILITIES_LMAC_TPC             [1]
[Sstar_log]:CAPABILITIES_LMAC_TEMPC           [1]
[Sstar_log]:CAPABILITIES_CTS_BUG              [1]
[Sstar_log]:CAPABILITIES_USB_RECOVERY_BUG     [1]
[Sstar_log]:CAPABILITIES_USE_IPC              [1]
[Sstar_log]:CAPABILITIES_OUTER_PA             [0]
[Sstar_log]:CAPABILITIES_POWER_CONSUMPTION    [0]
[Sstar_log]:CAPABILITIES_RSSI_DECIDE_TXPOWER  [0]
[Sstar_log]:CAPABILITIES_RTS_LONG_DURATION    [1]
[Sstar_log]:CAPABILITIES_TX_CFO_PPM_CORRECTION[0]
[Sstar_log]:CAPABILITIES_SHARE_CRYSTAL       [0]
[Sstar_log]:CAPABILITIES_HW_CHECKSUM          [0]
[Sstar_log]:CAPABILITIES_SINGLE_CHANNEL_MULRX [1]
[Sstar_log]:CAPABILITIES_CFO_DCXO_CORRECTION  [0]
[Sstar_log]:mdelay wait wsm_startup_done  !!
[Sstar_log]:WSM_FIRMWARE_CHECK_ID
[Sstar_log]:wsm_generic_confirm:status(2)
[Sstar_log]:<WARNING> wsm_write_mib fail !!! mibId=4132
[Sstar_log]:apollo wifi : can't open /data/.mac.info
[Sstar_log]:efuse data is [0x1,0x3b,0x6,0x7,0x8,0x10,0x0,0x0,0xdc:0x29:0x19:0x8:0x1:0x6]
[Sstar_log]:apollo wifi : can't open /Sstar_txpwer_dcxo_cfg.txt
[Sstar_log]:ELOG_INIT len 64 
[Sstar_log]:[Sstar_wtd]:set wtd_probe = 1
/ # random: crng init done
```
