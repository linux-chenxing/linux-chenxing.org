# infinity 6

This seems to be an updated version of the infinity3 IP camera SoCs.
The vendor kernel for these seems to be 4.9.84.

## Specs

- 16KB Boot ROM

## SSC323

- Single Cortex A7 with 64MB of DDR2
- Apparently no ethernet.
- [pinout](pinouts.md#88-pin-qfn)

### Known devices

- [IMILAB Home Security Camera A1](https://fccid.io/2APA9-IPC019E/Internal-Photos/Internal-Photos-4644200)

## SSC325(D)

- [Sigmastar page](http://www.sigmastarsemi.com/en/products/info.aspx?itemid=378&lcid=55&pid=)
- Single Cortex A7 with 64MB of DDR2 or 128MB of DDR3
- Chip id: 0xef
- [pinout](pinouts.md#88-pin-qfn)

### BootROM tag

```MVX1##I6g4d97980CMN_ROM######XVM```

## SSC326D

- [Sigmastar page](http://www.sigmastarsemi.com/en/products/info.aspx?itemid=380&lcid=55&pid=)

![SSC326D block diagram](ssc326d_blockdiagram.png)

## SSC333

[Databrief](ssc333_pb_v01.pdf)

## SSC335

[Databrief](ssc335_pb_v03.pdf)

## SSC335DE

## SSC336

[Databrief](ssc336d_ssc336q_pb_v03.pdf)

## SSC336Q

- Chip id: 0xf1
- dual core.
- Machine model: INFINITY6E SSC012B-S01A
- BROM (32Kb) Tag MVX4######gce02feaI6e_ROM####XVM

## SSC337

- Chip id: 0xf2

### SSC337DE

[Databrief](SSC337D_brief_datasheet.pdf)

### SSC30KQ

- Infinity6e 
- Chip id: 0xf1
- dual core.
- RAM 256MB
- Machine model: INFINITY6E SSC012B-S01A
- BROM (32Kb) Tag MVX4######gce02feaI6e_ROM####XVM

### SSC339G

- Infinity6e 

<details>
<summary>Boot log:</summary>
 

```
IPL 1fb0433
D-b7

MCP32_1866_4X
== miu settings for 6 layer board ==
miupll_400MHz
512MB

BIST0_0001-OK

HS on
Load IPL_CUST from SPINAND

 BlSize 00006380
CUST_KEY
Checksum OK

JMP+++ 
IPL_CUST 1fb0433
_IPLCustSNandOp
Load BL from SPINAND
CUST Key
KEYN_SIZE(0x0100)

KEYN_ADDRESS(0x23c06180)

  decomp_size=0x000418c4


DH-Boot ver001.001.001-svn8128 (May 21 2020 - 15:34:49 +0800)

SPINAND: _MDrv_SPINAND_GET_INFO: Found SPINAND INFO 
(0xC8) (0x1) (0x0) (0x0) (0x6) 

SPINAND: board_nand_init: CIS contains part info
128 MiB
DH-BOOT_commonSwRsaVerify run successfully!
rootfstype squashfs root /dev/mtdblock12
fdt dec init bootargs, get HWID failed
**warning! init boot args info, init bootargs failed.
error count:0
power magic=0x7ffe00
after flush cache, power magic = 0x424f4f54
 Booting kernel from Legacy Image at 22000000 ...
   Image Name:   Linux-4.9.84
   Image Type:   ARM Linux Kernel Image (uncompressed)
   Data Size:    4119724 Bytes = 3.9 MiB
   Load Address: 20008000
   Entry Point:  20008000
DH-BOOT_commonSwRsaVerify run successfully!
   Loading Kernel Image ... OK

Starting kernel ...

Booting Linux on physical CPU 0x0
Linux version 4.9.84 (svn version 5139) (jenkins@21ab06e66b83) (gcc version 9.1.0 (GCC) ) #2 SMP PREEMPT Thu May 21 15:37:33 CST 2020
CPU: ARMv7 Processor [410fc075] revision 5 (ARMv7), cr=50c5387d
CPU: div instructions available: patching division code
CPU: PIPT / VIPT nonaliasing data cache, VIPT aliasing instruction cache
OF: fdt:Machine model: INFINITY6E SSC013A-S01A
LXmem is 0x0 PHYS_OFFSET is 0x20000000

LX_MEM  = 0x20000000, 0x0
LX_MEM2 = 0x0, 0x0
LX_MEM3 = 0x0, 0x0
EMAC_LEN= 0x0
DRAM_LEN= 0x0
no any mma heap
cma: Reserved 2 MiB at 0x27c00000
Memory policy: Data cache writealloc
[infinity6e_smp_init_cpus]
percpu: Embedded 13 pages/cpu @c7e34000 s21208 r8192 d23848 u53248
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 32512
Kernel command line: mem=128M mtdparts=nand0:4M@0(mini-Boot),1M@4M(updateflag),1M@5M(hwid),1M@6M(dtb),4M@7M(syslog),4M@11M(config),4M@15M(backup),4M@19M(appdata),1M@23M(dgs),9728K@24M(firmware),2M@34304K(product),6M@36352K(Kernel),26M@42496K(romfs),8M@69120K(web),1M@77312K(backdtb),9728K@78336K(backfirmware),2M@86M(backproduct),6M@88M(backkernel),26M@94M(backromfs),8M@120M(backweb) console=ttyS0,115200 root=/dev/mtdblock12 rootfstype=squashfs
PID hash table entries: 512 (order: -1, 2048 bytes)
Dentry cache hash table entries: 16384 (order: 4, 65536 bytes)
Inode-cache hash table entries: 8192 (order: 3, 32768 bytes)
Memory: 120916K/131072K available (2825K kernel code, 156K rwdata, 1420K rodata, 1352K init, 186K bss, 8108K reserved, 2048K cma-reserved)
Virtual kernel memory layout:
    vector  : 0xffff0000 - 0xffff1000   (   4 kB)
    fixmap  : 0xffc00000 - 0xfff00000   (3072 kB)
    vmalloc : 0xc8800000 - 0xff800000   ( 880 MB)
    lowmem  : 0xc0000000 - 0xc8000000   ( 128 MB)
    modules : 0xbf800000 - 0xc0000000   (   8 MB)
      .text : 0xc0008000 - 0xc02ca928   (2827 kB)
      .init : 0xc0456000 - 0xc05a8000   (1352 kB)
      .data : 0xc05a8000 - 0xc05cf360   ( 157 kB)
       .bss : 0xc05d11a0 - 0xc05ff9c8   ( 187 kB)
SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=2, Nodes=1
Preemptible hierarchical RCU implementation.
Build-time adjustment of leaf fanout to 32.
RCU restricting CPUs from NR_CPUS=4 to nr_cpu_ids=2.
RCU: Adjusting geometry for rcu_fanout_leaf=32, nr_cpu_ids=2
NR_IRQS:16 nr_irqs:16 16
ms_init_main_intc: np->name=ms_main_intc, parent=gic
ms_init_pm_intc: np->name=ms_pm_intc, parent=ms_main_intc
ss_init_gpi_intc: np->name=ms_gpi_intc, parent=ms_main_intc
Find CLK_ven_pll, hook ms_venpll_ops
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
Version : MVX4##I6E#g#######KL_LX409##[BR:g]#XVM
GPIO: probe end[Padmux]reset PAD56(reg 0x103c00:2c; mask0x8) t0 SD1_MODE_1 (org: GPIO)
hw-breakpoint: found 5 (+1 reserved) breakpoint and 4 watchpoint registers.
hw-breakpoint: maximum watchpoint size is 8 bytes.
clocksource: Switched to clocksource arch_sys_counter
FS-Cache: Loaded
NET: Registered protocol family 2
TCP established hash table entries: 1024 (order: 0, 4096 bytes)
TCP bind hash table entries: 1024 (order: 2, 20480 bytes)
TCP: Hash tables configured (established 1024 bind 1024)
UDP hash table entries: 128 (order: 0, 6144 bytes)
UDP-Lite hash table entries: 128 (order: 0, 6144 bytes)
NET: Registered protocol family 1
RPC: Registered named UNIX socket transport module.
RPC: Registered udp transport module.
RPC: Registered tcp transport module.
RPC: Registered tcp NFSv4.1 backchannel transport module.
firmware_crypto partition firmware 
firmware_crypto partition product 
firmware_crypto partition Kernel 
firmware_crypto partition romfs 
firmware_crypto partition web 
firmware_crypto partition backfirmware 
firmware_crypto partition backproduct 
firmware_crypto partition backkernel 
firmware_crypto partition backromfs 
firmware_crypto partition backweb 
hw perfevents: enabled with armv7_cortex_a7 PMU driver, 5 counters available
workingset: timestamp_bits=30 max_order=15 bucket_order=0
squashfs: version 4.0 (2009/01/31) Phillip Lougher
io scheduler noop registered
io scheduler deadline registered (default)
D****a read-only mtdblock
libphy: Fixed MDIO Bus: probed
PPP generic driver version 2.4.2
NET: Registered protocol family 24
i2c /dev entries driver
1f221000.uart0: ttyS0 at MMIO 0x0 (irq = 44, base_baud = 10800000) is a unknown
1f221200.uart1: ttyS1 at MMIO 0x0 (irq = 45, base_baud = 10800000) is a unknown
1f220400.uart2: ttyS2 at MMIO 0x0 (irq = 47, base_baud = 10800000) is a unknown
[MS_PM_INTC] hw:9 -> v:68
[MS_PM_INTC] hw:10 -> v:69
MSYS: DMEM request: [emac0_buff]:0x00000812
MSYS: DMEM request: [emac0_buff]:0x00000812 success, CPU phy:@0x27C45000, virt:@0xC7C45000
libphy: mdio: probed
mdio_bus mdio-bus@emac0: /soc/emac0/mdio-bus/ethernet-phy@0 has invalid PHY address
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 0
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 1
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 2
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 3
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 4
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 5
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 6
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 7
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 8
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 9
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 10
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 11
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 12
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 13
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 14
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 15
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 16
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 17
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 18
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 19
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 20
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 21
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 22
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 23
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 24
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 25
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 26
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 27
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 28
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 29
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 30
mdio_bus mdio-bus@emac0: scan phy ethernet-phy at address 31
[emac_phy_connect][3248] connected mac emac0 to PHY at mdio-bus@emac0:00 [uid=11112222, driver=SStar 10/100 Ethernet Phy]
ms_rtcpwc 1f006800.rtcpwc: rtc core: registered 1f006800.rtcpwc as rtc0
MSYS: DMEM request: [AESDMA_ENG]:0x00001000
MSYS: DMEM request: [AESDMA_ENG]:0x00001000 success, CPU phy:@0x27C46000, virt:@0xC7C46000
MSYS: DMEM request: [AESDMA_ENG1]:0x00001000
MSYS: DMEM request: [AESDMA_ENG1]:0x00001000 success, CPU phy:@0x27C47000, virt:@0xC7C47000
[ms_cpufreq_init] Current clk=796917760
[i6e][pwm] use ms_pwm->group_data
[NOT ICE]Each grp bit0 must be enabled!
[NOT ICE]pwm-isr(60) success. If not i6e or i6b0, pls confirm it on .dtsi
mstar_spinand_probe: mstar_spinand enableClock
MSYS: DMEM request: [BDMA]:0x00000840
MSYS: DMEM request: [BDMA]:0x00000840 success, CPU phy:@0x27C48000, virt:@0xC7C48000
MDrv_SPINAND_Init: Detected ID: MID =ee, DID =ee
_dumpNandInformation:warning, Bytes / Page :  2048
_dumpNandInformation:warning, Pages / Block:  64
_dumpNandInformation:warning, Sector/ Page :  512
_dumpNandInformation:warning, Spare / Page :  64
_dumpNandInformation:warning, Current config r:1 w:1 drv:1
mstar_spinand_probe: Magic memcmp pass
mstar_spinand_probe: Get partition (Block 0 : page 1)
mstar_spinand_probe: CIS contains part info
mstar_spinand_probe: Before nand_scan()...
20 cmdlinepart partitions found on MTD device nand0
mstar_spinand_probe: Mtd parts parse
Creating 20 MTD partitions on "nand0":
0x000000000000-0x000000400000 : "mini-Boot"
0x000000400000-0x000000500000 : "updateflag"
0x000000500000-0x000000600000 : "hwid"
0x000000600000-0x000000700000 : "dtb"
0x000000700000-0x000000b00000 : "syslog"
0x000000b00000-0x000000f00000 : "config"
0x000000f00000-0x000001300000 : "backup"
0x000001300000-0x000001700000 : "appdata"
0x000001700000-0x000001800000 : "dgs"
0x000001800000-0x000002180000 : "firmware"
0x000002180000-0x000002380000 : "product"
0x000002380000-0x000002980000 : "Kernel"
0x000002980000-0x000004380000 : "romfs"
0x000004380000-0x000004b80000 : "web"
0x000004b80000-0x000004c80000 : "backdtb"
0x000004c80000-0x000005600000 : "backfirmware"
0x000005600000-0x000005800000 : "backproduct"
0x000005800000-0x000005e00000 : "backkernel"
0x000005e00000-0x000007800000 : "backromfs"
0x000007800000-0x000008000000 : "backweb"
=================
mstar notify driver install successfully
ip_tables: (C) 2000-2006 Netfilter Core Team
NET: Registered protocol family 10
sit: IPv6, IPv4 and MPLS over IPv4 tunneling driver
NET: Registered protocol family 17
Key type dns_resolver registered
ThumbEE CPU extension supported.
Registering SWP/SWPB emulation handler
ms_rtcpwc 1f006800.rtcpwc: setting system clock to 1970-01-04 12:36:05 UTC (304565)
This architecture does not have kernel memory protection.`
```

</details>
