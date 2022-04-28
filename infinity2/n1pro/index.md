# N1PRO

## Specs

- SSD203D

## Boot log

```
IPL gb126610
D-1e
HW Reset
miupll_233MHz
MIU0 zq=0x003b
miu_bw_set
utmi_1_init done
utmi_2_init done
utmi_3_init done
usbpll init done......
cpupll init done
SPI 54M
clk_init done 
P1 USB_rterm trim=0x0000
P1 USB_HS_TX_CURRENT trim=0x000d
P2 USB_rterm trim=0x0000
P2 USB_HS_TX_CURRENT trim=0x0001
P3 USB_rterm trim=0x0000
P3 USB_HS_TX_CURRENT trim=0x0001
PM_vol_bgap trim=0x0000
GCR_SAR_DATA trim=0x0190
ETH 10T output swing trim=0x0010
ETH 100T output swing trim=0x0010
ETH RX input impedance trim=0x0000
ETH TX output impedance trim=0x0000
MIPI_HS_RTERM trim=0x0001
MIPI_LP_RTERM trim=0x0000
TX_current trimming trim[0x1A]=0x0045
TX_current trimming trim[0x1B]=0x0042
TX_current trimming trim[0x1C]=0x0041
HDMI2TX Rterm trim=0x0000
HDMI2TX_Ibias_CH0 trim=0x0019
HDMI2TX_Ibias_CH1 trim=0x001a
HDMI2TX_Ibias_CH2 trim=0x0019
HDMI2TX_Ibias_CH3 trim=0x001a
128MB
BIST0_0001-OK
Enable MMU and CACHE
Load IPL_CUST from NOR
offset:00010000
Flash:207018
XMC OTP QE = 1
Load time 834 us, 25860 KiB/s
Checksum OK

IPL_CUST gb126610
MXP found at 0x00020000
runUBOOT()
runUBOOT()
[SPI_NOR]
Load time 14018 us, 13268 KiB/s
 -Verify UBOOT CRC32 passed!
 -Decompress UBOOT XZ
  decomp_size=0x0007db00
Disable MMU and D-cache before jump to UBOOT�

U-Boot 2015.01 (Aug 05 2021 - 20:09:37)

Version: I2g#######
[WDT] Enalbe WATCHDOG 60s
       Watchdog enabled
I2C:   ready
DRAM:  
WARNING: Caches not enabled
nor_flash_mxp allocated success!!
Flash is detected (0x0C05, 0x20, 0x70, 0x18)
Not support quad mode!!!
SF: Detected nor0 with total size 16 MiB
MXP found at mxp_offset[4]=0x00020000, size=0x1000
env_offset=0x5F000 env_size=0x1000
Flash is detected (0x0C05, 0x20, 0x70, 0x18)
SF: Detected nor0 with total size 16 MiB
In:    serial
Out:   serial
Err:   serial
Net:   No ethernet found.
cutomerid = NEWLINK20X,rota = 0,gpio = 26,board = 95
do_customer_init: NONE
LOGO in flash offset=0x260000 size=0x20000
Header count 3
Name DISP Sub head sz 56 total sz 192 node cnt 4
First offset 116 out buf size 0x300000 out buf addr 0x7c00000 en 2
CONFIG_SSTAR_RGN enable, u32LogoId:0, gu32GOPorMOP:0
Total size 248
Total sz 30232, Node cnt 1
interface 1 w 1280 h 720 clock 60
gpio debug MHal_GPIO_Pad_Set: pin=48
gpio[48] is 0
Flash is detected (0x0C05, 0x20, 0x70, 0x18)
SF: Detected nor0 with total size 16 MiB
SF: 2097152 bytes @ 0x60000 Read: OK
gpio debug MHal_GPIO_Pad_Set: pin=48
gpio[48] is 1
##  Booting kernel from Legacy Image at 22000000 ...
   Image Name:   MVX4##I2M#g#######KL_LX409##[BR:
   Image Type:   ARM Linux Kernel Image (lzma compressed)
   Data Size:    1997188 Bytes = 1.9 MiB
   Load Address: 20008000
   Entry Point:  20008000
   Verifying Checksum ... OK
-usb_stop(USB_PORT0)
-usb_stop(USB_PORT1)
-usb_stop(USB_PORT2)
   Uncompressing Kernel Image ... 
[XZ] !!!reserved 0x21000000 length=0x 1000000 for xz!!
   XZ: uncompressed size=0x40a000, ret=7
OK
atags:0x20000000

Starting kernel ...

Booting Linux on physical CPU 0x0
Linux version 4.9.84 (bill@ubuntu) (gcc version 8.2.1 20180802 (GNU Toolchain for the A-profile Architecture 8.2-2018-08 (arm-rel-8.23)) ) #26 SMP PREEMPT Thu Aug 5 20:12:07 CST 2021
CPU: ARMv7 Processor [410fc075] revision 5 (ARMv7), cr=50c5387d
CPU: div instructions available: patching division code
CPU: PIPT / VIPT nonaliasing data cache, VIPT aliasing instruction cache
early_atags_to_fdt() success
OF: fdt:Machine model: INFINITY2M SSC010A-S01A-S
LXmem is 0x7f00000 PHYS_OFFSET is 0x20000000
Add mem start 0x20000000 size 0x7f00000!!!!

LX_MEM  = 0x20000000, 0x7f00000
LX_MEM2 = 0x0, 0x0
LX_MEM3 = 0x0, 0x0
EMAC_LEN= 0x0
DRAM_LEN= 0x0
no any mmap reserved
deal_with_reserve_mma_heap memblock_reserve success mma_config[0].reserved_start=
0x20800000

deal_with_reserve_mma_heap memblock_reserve success mma_config[1].reserved_start=
0x27500000

cma: Reserved 2 MiB at 0x27200000
Memory policy: Data cache writealloc
percpu: Embedded 14 pages/cpu @c71c6000 s25112 r8192 d24040 u57344
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 15382
Kernel command line: console=ttyS0,115200 root=/dev/mtdblock3 rootfstype=squashfs ro init=/linuxrc LX_MEM=0x7f00000 mma_heap=MMU_MMA,miu=0,sz=0x3800000 mma_heap=mma_heap_name0,miu=0,sz=0x1
PID hash table entries: 256 (order: -2, 1024 bytes)
Dentry cache hash table entries: 8192 (order: 3, 32768 bytes)
Inode-cache hash table entries: 4096 (order: 2, 16384 bytes)
Memory: 55300K/62464K available (2318K kernel code, 258K rwdata, 1252K rodata, 164K init, 155K bss, 5116K reserved, 2048K cma-reserved)
Virtual kernel memory layout:
    vector  : 0xffff0000 - 0xffff1000   (   4 kB)
    fixmap  : 0xffc00000 - 0xfff00000   (3072 kB)
    vmalloc : 0xc7800000 - 0xff800000   ( 896 MB)
    lowmem  : 0xc0000000 - 0xc7500000   ( 117 MB)
    modules : 0xbf800000 - 0xc0000000   (   8 MB)
      .text : 0xc0008000 - 0xc024bb30   (2319 kB)
      .init : 0xc03a7000 - 0xc03d0000   ( 164 kB)
      .data : 0xc03d0000 - 0xc0410848   ( 259 kB)
       .bss : 0xc0412000 - 0xc0438c10   ( 156 kB)
SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=2, Nodes=1
Preemptible hierarchical RCU implementation.
        Build-time adjustment of leaf fanout to 32.
        RCU restricting CPUs from NR_CPUS=4 to nr_cpu_ids=2.
RCU: Adjusting geometry for rcu_fanout_leaf=32, nr_cpu_ids=2
NR_IRQS:16 nr_irqs:16 16
ms_init_main_intc: np->name=ms_main_intc, parent=gic
ms_init_pm_intc: np->name=ms_pm_intc, parent=ms_main_intc
ss_init_gpi_intc: np->name=ms_gpi_intc, parent=ms_main_intc
Find CLK_cpupll_clk, hook ms_cpuclk_ops
arm_arch_timer: Architected cp15 timer(s) running at 6.00MHz (virt).
clocksource: arch_sys_counter: mask: 0xffffffffffffff max_cycles: 0x1623fa770, max_idle_ns: 440795202238 ns
sched_clock: 56 bits at 6MHz, resolution 166ns, wraps every 4398046511055ns
Switching to timer-based delay loop, resolution 166ns
Console: colour dummy device 80x30
console [ttyS0] enabled
Calibrating delay loop (skipped), value calculated using timer frequency.. 12.00 BogoMIPS (lpj=60000)
pid_max: default: 4096 minimum: 301
Mount-cache hash table entries: 1024 (order: 0, 4096 bytes)
Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes)
CPU: Testing write buffer coherency: ok
CPU0: update cpu_capacity 1024
CPU0: thread -1, cpu 0, socket 0, mpidr 80000000
Setting up static identity map for 0x20008240 - 0x20008270
CPU1: update cpu_capacity 1024
CPU1: thread -1, cpu 1, socket 0, mpidr 80000001
Brought up 2 CPUs
SMP: Total of 2 processors activated (24.00 BogoMIPS).
CPU: All CPU(s) started in SVC mode.
devtmpfs: initialized
VFP support v0.3: implementor 41 architecture 2 part 30 variant 7 rev 5
clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns
futex hash table entries: 16 (order: -2, 1024 bytes)
NET: Registered protocol family 16
DMA: preallocated 256 KiB pool for atomic coherent allocations


Version : MVX4##I2M#g#######KL_LX409##[BR:g]#XVM

GPIO: probe end[ss_gpi_intc_domain_alloc] hw:42 -> v:45
[MS_PM_INTC] hw:20 -> v:53
hw-breakpoint: found 5 (+1 reserved) breakpoint and 4 watchpoint registers.
hw-breakpoint: maximum watchpoint size is 8 bytes.
SCSI subsystem initialized
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
Linux video capture interface: v2.00
clocksource: Switched to clocksource arch_sys_counter
NET: Registered protocol family 2
TCP established hash table entries: 1024 (order: 0, 4096 bytes)
TCP bind hash table entries: 1024 (order: 2, 20480 bytes)
TCP: Hash tables configured (established 1024 bind 1024)
UDP hash table entries: 128 (order: 0, 6144 bytes)
UDP-Lite hash table entries: 128 (order: 0, 6144 bytes)
NET: Registered protocol family 1
hw perfevents: enabled with armv7_cortex_a7 PMU driver, 5 counters available
workingset: timestamp_bits=30 max_order=14 bucket_order=0
squashfs: version 4.0 (2009/01/31) Phillip Lougher
jffs2: version 2.2. © 2001-2006 Red Hat, Inc.
io scheduler noop registered
io scheduler deadline registered (default)
libphy: Fixed MDIO Bus: probed
mousedev: PS/2 mouse device common for all mice
i2c /dev entries driver
IR NEC protocol handler initialized
usbcore: registered new interface driver uvcvideo
USB Video Class driver (1.1.1)
usbcore: registered new interface driver usbhid
usbhid: USB HID core driver
1f221000.uart0: ttyS0 at MMIO 0x0 (irq = 30, base_baud = 10800000) is a unknown
1f221200.uart1: ttyS1 at MMIO 0x0 (irq = 31, base_baud = 10800000) is a unknown
1f220400.uart2: ttyS2 at MMIO 0x0 (irq = 33, base_baud = 10800000) is a unknown
1f221400.uart2: ttyS3 at MMIO 0x0 (irq = 34, base_baud = 10800000) is a unknown
[Core Voltage] check_voltage_valid: Not support 0mV, use 950mV
Registered IR keymap rc-mstar-dtv
input: mstar ir as /devices/virtual/rc/rc0/input0
rc rc0: mstar ir as /devices/virtual/rc/rc0
ms_rtcpwc 1f006800.rtcpwc: rtc core: registered 1f006800.rtcpwc as rtc0
MSYS: DMEM request: [BDMA_FSP_WBUFF]:0x00010040
MSYS: DMEM request: [BDMA_FSP_WBUFF]:0x00010040 success, CPU phy:@0x27250000, virt:@0xC7250000
[Ser flash] phys=0x27250000, virt=0xc7250000, bus=0x07250000 len:0x10040
[FSP] Flash is detected (0x1200, 0x20, 0x70, 0x18) ver1.1
[FSP] 1-1-4 QUAD_READ MODE
mtd .name = NOR_FLASH, .size = 0x01000000 (16MiB)
 .erasesize = 0x00010000 .numeraseregions = 0
MXP_PARTS!!
MXP found at mxp_offset[4]=0x00020000, size=0x1000
Creating 7 MTD partitions on "NOR_FLASH":
0x000000000000-0x000000060000 : "BOOT"
0x000000060000-0x000000260000 : "KERNEL"
0x000000260000-0x000000280000 : "LOGO"
0x000000280000-0x000000400000 : "rootfs"
0x000000400000-0x000000720000 : "miservice"
0x000000720000-0x000000f00000 : "customer"
0x000000f00000-0x000001000000 : "appconfigs"
[ms_cpufreq_init] Current clk=1005326304
[Core Voltage] check_voltage_valid: Not support 900mV, use 950mV
NET: Registered protocol family 17
ThumbEE CPU extension supported.
Registering SWP/SWPB emulation handler
Please set rtc timer (hwclock -w) 
ms_rtcpwc 1f006800.rtcpwc: setting system clock to 1970-01-01 00:00:00 UTC (0)
OF: fdt:not creating '/sys/firmware/fdt': CRC check failed
VFS: Mounted root (squashfs filesystem) readonly on device 31:3.
devtmpfs: mounted
This architecture does not have kernel memory protection.
mount: can't find devpts in /etc/fstab
/etc/init.d/rcS: line 12: telnetd: not found
mount: mounting none on /sys failed: Device or resource busy
mount: mounting none on /sys/kernel/debug/ failed: Device or resource busy
telnetd: applet not found
>> [sdmmc] ms_sdmmc_probe 
[Padmux]reset Pad_51(reg 0x101e09; mask0x70) to GPIO(org: I2C1_MODE_5)
[Padmux]reset Pad_51(reg 0x101e08; mask0x300) to GPIO(org: SDIO_MODE_1)
>> [sdmmc_0] Probe Platform Devices
ntfs: driver 2.1.32 [Flags: R/O MODULE].
insmod: can't read '/config/modules/4.9.84/usb-common.ko': No such file or directory
insmod: can't read '/config/modules/4.9.84/usbcore.ko': No such file or directory
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
Sstar-ehci-1 soc:Sstar-ehci-1: irq 39, io mem 0xfd284800
usb usb2: New USB device found, idVendor=1d6b, idProduct=0002
usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1
usb usb2: Product: EHCI Host Controller
usb usb2: Manufacturer: Linux 4.9.84 ehci_hcd
usb usb2: SerialNumber: mstar
hub 2-0:1.0: USB hub found
hub 2-0:1.0: 1 port detected
Sstar-ehci-3 H.W init
Titania3_series_start_ehc start
[USB] config miu select [70] [e8] [ef] [ef]
[USB] enable miu lower bound address subtraction
[USB] init squelch level 0x2
[USB] no platform_data, device tree coming
[USB][EHC] dma coherent_mask 0xffffffffffffffff mask 0xffffffffffffffff
BC disable 
[USB] soc:Sstar-ehci-3 irq --> 57
Sstar-ehci-3 soc:Sstar-ehci-3: EHCI Host Controller
Sstar-ehci-3 soc:Sstar-ehci-3: new USB bus registered, assigned bus number 3
Sstar-ehci-3 soc:Sstar-ehci-3: irq 57, io mem 0xfd286400
usb usb3: New USB device found, idVendor=1d6b, idProduct=0002
usb usb3: New USB device strings: Mfr=3, Product=2, SerialNumber=1
usb usb3: Product: EHCI Host Controller
usb usb3: Manufacturer: Linux 4.9.84 ehci_hcd
usb usb3: SerialNumber: mstar
hub 3-0:1.0: USB hub found
hub 3-0:1.0: 1 port detected
insmod: can't read '/config/modules/4.9.84/scsi_mod.ko': No such file or directousbcore: registered new interface driver usb-storage
ry
insmod: can't read '/config/modules/4.9.84/usbhid.ko': No such file or directory
MSYS: DMEM request: [AESDMA_ENG]:0x00001000
MSYS: DMEM request: [AESDMA_ENG]:0x00001000 success, CPU phy:@0x2724E000, virt:@0xC724E000
MSYS: DMEM request: [AESDMA_ENG1]:0x00001000
MSYS: DMEM request: [AESDMA_ENG1]:0x00001000 success, CPU phy:@0x2724F000, virt:@0xC724F000
mhal: loading out-of-tree module taints kernel.
mhal: module license 'PROPRIETARY' taints kernel.
Disabling lock debugging due to kernel taint
mhal driver init
jpe driver probed
DivpProcInit 514
module [sys] init
MI_SYSCFG_SetupMmapLoader default_config_path:/config/config_tool, argv1:/config/load_mmap,argv2:/config/mmap.ini
Function = init_glob_miu_kranges, Line = 603, Insert KProtect for LX @ MIU: 0
Function = init_glob_miu_kranges, Line = 612, [INIT] for LX0 kprotect: from 0x20000000 to 0x27F00000, using block 0
config...... strPath:/config/config_tool, argv0:/config/load_config
function:parese_Cmdline,pCmd_Section:0x7f00000
MM
U_
MM
A    miu=0,sz=3800000  reserved_start=20800000
[MDrv_MMU_SetPageSize] not support u8PgSz256En = 1 
r_front->miuBlockIndex:0,r_front->start_cpu_bus_pa:0x20000000,r_front->start_cpu_bus_pa+r_front->length:0x20800000
r_back->miuBlockIndex:1,r_back->start_cpu_bus_pa:0x24000000,r_back->start_cpu_bus_pa+r_back->length:0x27f00000
mi_sys_mma_allocator_create success, heap_base_addr=20800000 length=3800000 
mm
a_
he
ap
_n
am
e0
    miu=0,sz=a00000  reserved_start=27500000
r_front->miuBlockIndex:1,r_front->start_cpu_bus_pa:0x24000000,r_front->start_cpu_bus_pa+r_front->length:0x27500000
mi_sys_mma_allocator_create success, heap_base_addr=27500000 length=a00000 
Kernel CONFIG_HZ = 100
Sigmastar Module version: project_commit.f07895a sdk_commit.aac7433 build_time.20200819195036
module [ao] init
module [gfx] init
[MDrv_MMU_AddClientId] not support , chipId = 2 
GE_EnableDynaClkGate
 MI_Moduledev_RegisterDev  
module [divp] init
module [vdec] init
module [hdmi] init
module [disp] init
[GOP]HalGopUpdateGwinParam 719: GOP_id=011 not support
[GOP]HalGopSetArgb1555Alpha 1207: GOPId=0x11 not support
[GOP]HalGopSetArgb1555Alpha 1207: GOPId=0x11 not support
[ss_gpi_intc_domain_alloc] hw:57 -> v:61
[1]+  Done(127)                  busybox telnetd
/ # ###main client [671] connected, module:sys
line 493 otasrv main enter
client [671] connected, module:disp
[MI_SYSCFG_GetPanelInfo 41] eTiming = 4, hdmiTx = 0 [DACOUT_576I_50]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 2, hdmiTx = 0 [DACOUT_480I_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 8, hdmiTx = 0 [DACOUT_1080P_24]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 9, hdmiTx = 0 [DACOUT_1080P_25]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 10, hdmiTx = 0 [DACOUT_1080P_30]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 6, hdmiTx = 0 [DACOUT_720P_50]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 7, hdmiTx = 0 [DACOUT_720P_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 11, hdmiTx = 0 [DACOUT_1080I_50]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 13, hdmiTx = 0 [DACOUT_1080I_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 12, hdmiTx = 0 [DACOUT_1080P_50]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 14, hdmiTx = 0 [DACOUT_1080P_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 5, hdmiTx = 0 [DACOUT_576P_50]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 3, hdmiTx = 0 [DACOUT_480P_60]
[MI_SYSCFG_GetPanelInfo 49] eTiming = 38, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 50, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 41] eTiming = 40, hdmiTx = 0 [DACOUT_1024X768P_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 43, hdmiTx = 0 [DACOUT_1280X1024P_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 41, hdmiTx = 0 [DACOUT_1366X768P_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 44, hdmiTx = 0 [DACOUT_1440X900P_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 42, hdmiTx = 0 [DACOUT_1280X800P_60]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 46, hdmiTx = 0 [DACOUT_1600X1050P_60]
[MI_SYSCFG_GetPanelInfo 49] eTiming = 50, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 41] eTiming = 45, hdmiTx = 0 [DACOUT_1600X1200P_60]
[MI_SYSCFG_GetPanelInfo 49] eTiming = 50, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 22, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 49] eTiming = 23, hdmiTx = 1  Not Fund!!!
[MI_SYSCFG_GetPanelInfo 41] eTiming = 30, hdmiTx = 0 [DACOUT_4K2KP_30]
[MI_SYSCFG_GetPanelInfo 41] eTiming = 32, hdmiTx = 0 [DACOUT_4K2KP_60]
[MDrv_MMU_AddClientId] not support , chipId = 2 
[MDrv_MMU_AddClientId] not support , chipId = 2 
BANK:0x112A 16bit-offset 0x12
0x0400
BANK:0x112A 16bit-offset 0x13
0x080B
BANK:0x112A 16bit-offset 0x15
0x0803
[Padmux]reset Pad_88(reg 0x101e09; mask0x7) to GPIO(org: I2C0_MODE_1)
_HDMITXOpen 112, HDMITx Alrad Open
DrvHdmitxOsSetClkOn 1216 num_parents:3 
DrvHdmitxOsSetClkOn 1219, CLK_0 = 0
DrvHdmitxOsSetClkOn 1219, CLK_1 = 432000000
DrvHdmitxOsSetClkOn 1219, CLK_2 = 216000000
DrvHdmitxOsSetClkOn 1256, [Hdmitx] num_parents:3-1        CLK_hdmi 0
DrvHdmitxOsSetClkOn 1256, [Hdmitx] num_parents:3-2    CLK_disp_432 432000000
DrvHdmitxOsSetClkOn 1256, [Hdmitx] num_parents:3-3    CLK_disp_216 216000000
client [671] connected, module:hdmi
AnalogDrvCur: Tap1(0x14, 0x14, 0x14, 0x14) Tap1(0x00, 0x00, 0x00, 0x00)
_HalHdmitxIfGetInfoSinkInfoConfig 772, Check Edid Data Fail
_DrvHdmitxIfExecuteQuery 524, Query:SINK_INFO, Ret:ERR

DrvHdmitxIfGetSinkInfo 889, Get Sink Info Fail
random: fast init done
_HalHdmitxIfGetInfoSinkInfoConfig 723, Check Edid Data Fail
_DrvHdmitxIfExecuteQuery 524, Query:SINK_INFO, Ret:ERR

DrvHdmitxIfGetSinkInfo 889, Get Sink Info Fail
[MI ERR ]: _MI_HDMI_ChkColorFormatForSpecTiming[1198]: Failed To Check Color Format

MDrv_HDMITx_SetHDMITxMode: HDMI mode = 2 
B InColor = 0, OutColor = 0
MDrv_HDMITx_SetHDMITxMode: HDMI mode = 2 
B InColor = 0, OutColor = 0
MDrv_HDMITx_SetHDMITxMode: HDMI mode = 2 
MDrv_HDMITx_Exhibit: Create Check Rx timer success!
E_HDMITX_FSM_CHECK_HPD:: pre= 0, cur = 1
HDMITx_Handler 5368, TMDS=0
HDMITx_Handler 5370, TMDS=f0

HDMI handler preState:curState = 0 : 1
sd203_ver:1.1.19-rcb16[Aug  5 2021:20:51:35-board:95]
###ZMInitMmalloc###
[ss_gpi_intc_domain_alloc] hw:11 -> v:62
[ss_gpi_intc_domain_alloc] hw:10 -> v:63
###sd20xclient [672] connected, module:disp
_proj_informatio_HalDispIfSetDeviceHdmiParam 2333, Peaking is not set
n line 542 env.proj_info=NEWLINK20X 0 26 95
###sstar_system_setParam line 807 luma_value[50],Contrast_value[50]
###hdmi_get_4kEableVal line 397 hdmi_get_4kEableVal=0###sd20x_hdmi_init line 477 E_MI_DISP_INTF_HDMI[16]
###uicommoncmd line 1178 prev frame is null
###uicommoncmd line 1245 prv[-1]2cur[0]:bitmain[0]timeout[0]
###usbenvdisbale line 2089 usbautoupgrade:0
enter usb monitor
###fuart_monitor_thread line 583 enter uart monitor
###lollipop_prop_handle_thread line 1911 receive prop_ipc event:IPC_PROP_GET sd20x_type unkown
###open_port line 260 open ttyS2 .....
###open_port line 271 fcntl=0
###open_port line 276 standard input is not a STDIN_FILENO
###open_port line 282 fd-open=8
###set_opt line 214 set done!
###fuart_monitor_thread line 607 fd[8]begin.read:1,5
###mainloop_mix line 1405 sd20x_type[sd203]
###m_wifi_load_driver line 1113 lsusb[1]tofind[1b20:8888]
###mLaunchSystemCmd line 1145 ssw01bInit.sh
BANK:0xE 16bit-offset 0x30
0x0011
BANK:0x103C 16bit-offset 0x08
0x0000
BANK:0x103C 16bit-offset 0x08
0x0011
###initwifisignalindex line 533 6,1
###set_rate_txpower_mode line 386 iwpriv wlan0 fwcmd set_rate_txpower_mode,6
###check_wifi_efuse line 431 efuse is[80] not change
###reset_interface line 1068 reset_interface[1]
###createp2pconf line 158 /appconfigs/p2p_supplicant.conf.st_size[235]
###getDeviceName line 71 rm hostapd.conf by:NETLINK-C1E1,C011
###getDeviceName line 87 device name not found in config file, generate it by wifi mac: NETLINK-C011
!!!chechZMCast line 174 1,,C011,C0:11
###sm_switch_mode line 869 cur = SM_MODE_NONE, next = SM_MODE_SOFTAP_P2P
###m_wifi_start_supplicant line 1517 [4]
###mLaunchSystemCmd line 1145 p2p_supplicant -ip2p0 -Dnl80211  -c/appconfigs/p2p_supplicant.conf   &
###mainloop_mix line 1484 WAIT.SM_MODE_NONE
###wifi_connect_to_supplicant line 689 ifname = p2p0, path = /var/run/mcast/p2p0
###p2p_init line 160 enter
###doBooleanCommand line 748 [SET persistent_reconnect 1]reply[OK]
###doBooleanCommand line 748 [SET device_name NETLINK-C011]reply[OK]
###doBooleanCommand line 748 [SET p2p_ssid_postfix -NETLINK-C011]reply[OK]
###doBooleanCommand line 748 [SET device_type 10-0050F204-5]reply[OK]
###doBooleanCommand line 748 [SET config_methods virtual_push_button physical_display keypad]reply[OK]
###doBooleanCommand line 748 [SET wifi_display 1]reply[OK]
###doBooleanCommand line 748 [WFD_SUBELEM_SET 0 000600111c440032]reply[OK]
###doBooleanCommand line 748 [P2P_FLUSH]reply[OK]
###p2p_set_listen_channel line 245 [0,6]
###doBooleanCommand line 748 [P2P_SET listen_channel 6]reply[OK]
###p2p_init line 189 leave1
register callback
MSrv.MiracastService version:May 28 2021,20:44:24
###P2PInit line 648 bypass
statemachine init
###connectSupplicant line 697 bypass
Enable MiracastService success
MiracastService set name:NETLINK-C011
###startZMcast line 208 mcast v2.1-plus
Copyright (c) 2020-2030, newlink-sn May 28 2021 20:44:25 contributors start

###p2p_init line 192 leave2
###softap_ui_thread line 902 p2pstate=1
Receive SUP_CONNECTION_EVENT
transitionTo:InactiveState
state:from DefaultState to InactiveState
###Status line 235 bypass
###listNetworks line 114 sd20x
###saveConfig line 135 sd20x.bypass
###doBooleanCommand line 748 [P2P_LISTEN]reply[network id / ssid / bssid / flags]
!!!p2pFindorListen line 210 p2pListen failed
wfdinfo: WFD enabled: true
WFD DeviceInfo: 17
 WFD CtrlPort: 7236
 WFD MaxThroughput: 50
###setWfdEnable line 1056 bypass
###setWfdDeviceInfo line 1067 bypass[000600111c440032]
###setDeviceName line 1078 bypass
###setP2pSsidPostfix line 1010 sd20x
###doBooleanCommand line 492 P2PNative.doBooleanCommand:[SET p2p_ssid_postfix -NETLINK-C011]Rep[OK]
###mainloop_mix line 1484 WAIT.SM_MODE_NONE
###doBooleanCommand line 748 [P2P_LISTEN]reply[OK]
###p2p_find_alert line 233 [1,1]
###mainloop_mix line 1484 WAIT.SM_MODE_NONE
###mLaunchSystemCmd line 1145 ifconfig wlan0 up
###mLaunchSystemCmd line 1145 ifconfig wlan0 192.168.203.1  netmask 255.255.255.0
###mLaunchSystemCmd line 1145 hostapd   -B /appconfigs/hostapd.conf &
Configuration file: /appconfigs/hostapd.conf
###mainloop_mix line 1484 WAIT.SM_MODE_NONE
###mLaunchSystemCmd line 1145 udhcpd -S /config/wifi/udhcpd_wlan0.conf  -a 100
###startDhcpServer line 287 udhcpd -S /config/wifi/udhcpd_wlan0.conf  -a 100
###start_softap_service line 804 deviceName = NETLINK-C011, channel = 6, passwd = 12345678
!!!stop_dlna_service line 288 dlna has stopped
###########uuid(e6572b54-c011-2d91-2fb5-b757f2537e21)(NETLINK-C011-(dlna))(1)###########.
###qrencode line 1034 [http://192.168.203.1][20]
!!!stop_icast_service line 67 icast has stopped
###start_icast_service line 39 start_icast_service[1]
###NewLink_StartAirplayServer[NETLINK-C011-(icast),Oct 13 2020,09:53:33][1920,1080,60]###
rfkill: Cannot open RFKILL control device
wlan0: interface state UNINITIALIZED->HT_SCAN
ZMSocket_Connect error: Network is unreachable(errno: 101)
ZMSocket_Connect error: Network is unreachable(errno: 101)
###ZMPost_LimitRegist.Err###
###mainloop_mix line 1484 WAIT.SM_MODE_NONE
###start_icast_service line 45 AirplayServiceStart[0]
###sm_switch_mode line 881 softap finish
###mainloop_mix line 1484 WAIT.SM_MODE_NONE
###ssd20x_postinit line 1384 exit
[01/Jan/1970:00:00:15 +0000] boa: server version Boa/0.94.13
[01/Jan/1970:00:00:15 +0000] boa: server built Apr 20 2020 at 10:23:27.
[01/Jan/1970:00:00:15 +0000] boa: starting server pid=805, port 80

/ # main_1654_0
* daemon not running. starting it now on port 5037 *
* daemon started successfully *
main_1654_0
###ancable_cb_event line 2130 ancable_cb_event[1]
###ancable_cb_event line 2130 ancable_cb_event[6]
!!!getStr line 231 error: string(name=usbconnstatus, subname=fail) not found in xml file
!!!show_text2 line 475 strl null
```

### GPIO

```
/ # cat /sys/kernel/debug/gpio 
gpiochip0: GPIOs 0-90, gpio:
 gpio-12  (                    |sysfs               ) out hi    
 gpio-25  (                    |sysfs               ) out lo    
 gpio-26  (                    |sysfs               ) out hi    
 gpio-72  (                    |                    ) out lo
 ```
