# GW300

![board](board_in_case.jpg)

## Hardware

- Winbond 128MiB SPI NAND 
- LongSung M5710 LTE cat 1 module.
  - CONFIG_USB_NET_RNDIS_HOST
  - CONFIG_USB_SERIAL_OPTION
- ISL1208 RTC
- SIPEX 3232EE RS232 transceiver.
- SP3485 RS485 transceiver.
- p5: seems to be another RS232 serial port
  - 1 ??? 
  - 2 t1out
  - 3 r1in
  - 4 gnd
- dip socket might be for a DTMF generator?

lsusb

```
root@myzr:~# lsusb 
Bus 002 Device 003: ID 2df3:9d03
Bus 001 Device 001: ID 1d6b:0002
Bus 002 Device 001: ID 1d6b:0002
```

## Mainline (+ mstar tree) dmesg

```
[    0.000000] Booting Linux on physical CPU 0x0
[    0.000000] Linux version 5.10.0+ (daniel@shiro) (arm-buildroot-linux-gnueabihf-gcc.br_real (Buildroot 2020.08-1318-ge7000b15fe) 10.2.0, GNU ld (GNU Binutils) 2.35.10
[    0.000000] CPU: ARMv7 Processor [410fc075] revision 5 (ARMv7), cr=10c5387d
[    0.000000] CPU: div instructions available: patching division code
[    0.000000] CPU: PIPT / VIPT nonaliasing data cache, VIPT aliasing instruction cache
[    0.000000] OF: fdt: Machine model: GW302
[    0.000000] Memory policy: Data cache writealloc
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x0000000020000000-0x0000000027ffffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000020000000-0x0000000027ffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000020000000-0x0000000027ffffff]
[    0.000000] On node 0 totalpages: 32768
[    0.000000]   Normal zone: 256 pages used for memmap
[    0.000000]   Normal zone: 0 pages reserved
[    0.000000]   Normal zone: 32768 pages, LIFO batch:7
[    0.000000] percpu: Embedded 13 pages/cpu s32460 r0 d20788 u53248
[    0.000000] pcpu-alloc: s32460 r0 d20788 u53248 alloc=13*4096
[    0.000000] pcpu-alloc: [0] 0 [0] 1 
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 32512
[    0.000000] Kernel command line: console=ttyS0,115200 clk_ignore_unused earlyprintk ubi.mtd=1 ubi.block=0,root root=/dev/ubiblock0_1
[    0.000000] Dentry cache hash table entries: 16384 (order: 4, 65536 bytes, linear)
[    0.000000] Inode-cache hash table entries: 8192 (order: 3, 32768 bytes, linear)
[    0.000000] mem auto-init: stack:off, heap alloc:off, heap free:off
[    0.000000] Memory: 117452K/131072K available (7168K kernel code, 703K rwdata, 1832K rodata, 1024K init, 241K bss, 13620K reserved, 0K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=2, Nodes=1
[    0.000000] rcu: Hierarchical RCU implementation.
[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=4 to nr_cpu_ids=2.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 10 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=2
[    0.000000] NR_IRQS: 16, nr_irqs: 16, preallocated irqs: 16
[    0.000000] gicint: 25
[    0.000000] arch_timer: cp15 timer(s) running at 6.00MHz (phys).
[    0.000000] clocksource: arch_sys_counter: mask: 0xffffffffffffff max_cycles: 0x1623fa770, max_idle_ns: 440795202238 ns
[    0.000001] sched_clock: 56 bits at 6MHz, resolution 166ns, wraps every 4398046511055ns
[    0.000019] Switching to timer-based delay loop, resolution 166ns
[    0.000166] clocksource: timer: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 159271703898 ns
[    0.000207] clocksource: timer: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 159271703898 ns
[    0.000255] clocksource: timer: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 159271703898 ns
[    0.000630] Console: colour dummy device 80x30
[    0.000676] Calibrating delay loop (skipped), value calculated using timer frequency.. 12.00 BogoMIPS (lpj=60000)
[    0.000696] pid_max: default: 32768 minimum: 301
[    0.000828] Mount-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.000847] Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.001487] CPU: Testing write buffer coherency: ok
[    0.001737] /cpus/cpu@0 missing clock-frequency property
[    0.001772] /cpus/cpu@1 missing clock-frequency property
[    0.001788] CPU0: thread -1, cpu 0, socket 0, mpidr 80000000
[    0.002308] Setting up static identity map for 0x20100000 - 0x20100060
[    0.002429] rcu: Hierarchical SRCU implementation.
[    0.003078] smp: Bringing up secondary CPUs ...
[    0.003699] CPU1: thread -1, cpu 1, socket 0, mpidr 80000001
[    0.003843] smp: Brought up 1 node, 2 CPUs
[    0.003866] SMP: Total of 2 processors activated (24.00 BogoMIPS).
[    0.003878] CPU: All CPU(s) started in SVC mode.
[    0.004308] devtmpfs: initialized
[    0.012225] random: get_random_bytes called from setup_net+0x30/0x168 with crng_init=0
[    0.012570] VFP support v0.3: implementor 41 architecture 2 part 30 variant 7 rev 5
[    0.012814] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns
[    0.012843] futex hash table entries: 512 (order: 3, 32768 bytes, linear)
[    0.012971] pinctrl core: initialized pinctrl subsystem
[    0.013330] regulator-dummy: no parameters, enabled
[    0.013865] NET: Registered protocol family 16
[    0.014295] DMA: preallocated 256 KiB pool for atomic coherent allocations
[    0.015527] cpuidle: using governor ladder
[    0.015573] cpuidle: using governor menu
[    0.036799] pm code is at c8879000, pm info is at c8878000, pmsleep is at c885ec00, pmgpio is at c887de00
[    0.036933] hw-breakpoint: found 5 (+1 reserved) breakpoint and 4 watchpoint registers.
[    0.036952] hw-breakpoint: maximum watchpoint size is 8 bytes.
[    0.047355] cryptd: max_cpu_qlen set to 1000
[    0.049466] vcc_dram: 1800 mV, enabled
[    0.049652] reg-fixed-voltage fixedregulator@1: vcc_dram supplying 1800000uV
[    0.050220] SCSI subsystem initialized
[    0.050415] usbcore: registered new interface driver usbfs
[    0.050457] usbcore: registered new interface driver hub
[    0.050525] usbcore: registered new device driver usb
[    0.050809] usb_phy_generic soc:fakephy@0: Looking up vcc-supply from device tree
[    0.050827] usb_phy_generic soc:fakephy@0: Looking up vcc-supply property in node /soc/fakephy@0 failed
[    0.050854] usb_phy_generic soc:fakephy@0: supply vcc not found, using dummy regulator
[    0.051139] mc: Linux media interface: v0.10
[    0.051180] videodev: Linux video capture interface: v2.00
[    0.051464] FPGA manager framework
[    0.051533] Advanced Linux Sound Architecture Driver Initialized.
[    0.052420] clocksource: Switched to clocksource arch_sys_counter
[    0.060214] NET: Registered protocol family 2
[    0.060782] tcp_listen_portaddr_hash hash table entries: 512 (order: 0, 6144 bytes, linear)
[    0.060827] TCP established hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.060853] TCP bind hash table entries: 1024 (order: 1, 8192 bytes, linear)
[    0.060880] TCP: Hash tables configured (established 1024 bind 1024)
[    0.060973] UDP hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.061012] UDP-Lite hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.061156] NET: Registered protocol family 1
[    0.061840] RPC: Registered named UNIX socket transport module.
[    0.061864] RPC: Registered udp transport module.
[    0.061872] RPC: Registered tcp transport module.
[    0.061880] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.063748] hw perfevents: enabled with armv7_cortex_a7 PMU driver, 5 counters available
[    0.067257] Initialise system trusted keyrings
[    0.067513] workingset: timestamp_bits=30 max_order=15 bucket_order=0
[    0.075759] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    0.076750] jffs2: version 2.2. (NAND) © 2001-2006 Red Hat, Inc.
[    0.170785] Key type asymmetric registered
[    0.170811] Asymmetric key parser 'x509' registered
[    0.170870] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)
[    0.172684] msc313-usb-phy soc:usbphy@0: Switching to UHC port
[    0.172717] msc313-usb-phy soc:usbphy@0: starting calibration...
[    0.173732] msc313-usb-phy soc:usbphy@0: calibration finished.
[    0.173760] phy phy-soc:usbphy@0.0: Looking up phy-supply from device tree
[    0.173771] phy phy-soc:usbphy@0.0: Looking up phy-supply property in node /soc/usbphy@0 failed
[    0.173904] phy phy-soc:usbphy@0.1: Looking up phy-supply from device tree
[    0.173916] phy phy-soc:usbphy@0.1: Looking up phy-supply property in node /soc/usbphy@0 failed
[    0.179704] msc313e-clkgen-mux 1f001c80.clkgen_mux: deglitch at 7
[    0.179771] msc313e-clkgen-mux 1f001c80.clkgen_mux: deglitch at 14
[    0.180501] msc313e-clkgen-mux 1f20705c.clkgen_mux: deglitch at 4
[    0.181698] msc313e-clkgen-mux 1f207180.clkgen_mux: deglitch at 4
[    0.182579] msc313e-clkgen-mux 1f207004.clkgen_mux: deglitch at 4
[    0.183675] msc313e-clkgen-mux: probe of 1f2070c0.clkgen_mux failed with error -22
[    0.184012] msc313e-clkgen-mux 1f2070c8.clkgen_mux: deglitch at 4
[    0.185050] msc313e-clkgen-mux 1f207184.clkgen_mux: deglitch at 4
[    0.185104] msc313e-clkgen-mux 1f207184.clkgen_mux: deglitch at 12
[    0.185134] msc313e-clkgen-mux 1f207184.clkgen_mux: deglitch clock is selected
[    0.186716] msc313e-clkgen-mux: probe of 1f226680.clkgen_mux failed with error -22
[    0.189342] msc313-bdma 1f200400.bdma: WARN: Device release is not defined so it is not safe to unbind this driver while in use
[    0.190126] cmdq probe
[    0.190295] msc313-cmdq 1f224000.cmdq: WARN: Device release is not defined so it is not safe to unbind this driver while in use
[    0.190980] Serial: 8250/16550 driver, 8 ports, IRQ sharing disabled
[    0.193283] printk: console [ttyS0] disabled
[    0.193381] 1f221000.uart: ttyS0 at MMIO 0x1f221000 (irq = 54, base_baud = 10800000) is a 16550A
[    0.899559] printk: console [ttyS0] enabled
[    0.904729] 1f221200.uart: ttyS1 at MMIO 0x1f221200 (irq = 55, base_baud = 10800000) is a 16550A
[    0.915823] mstar-drm soc:display@0: probe
[    0.920271] mstar-gop 1f246200.gop: 1f246200.gop -> �Q��U
[    0.925749] mstar-gop 1f246200.gop: 1f246200.gop -> ,J�ǯ
[    0.931354] mstar-gop 1f246200.gop: binding
[    0.935746] mstar-gop 1f246200.gop: reset
[    0.949785] mstar-gop 1f246200.gop: dst: ip_main
[    0.954440] mstar-drm soc:display@0: bound 1f246200.gop (ops 0xc084817c)
[    0.961447] [drm] Initialized mstar-drm 1.0.0 20191208 for soc:display@0 on minor 0
[    0.970013] dummy-irq: no IRQ given.  Use irq=N
[    0.976708] spi-nand spi0.0: Winbond SPI NAND was found.
[    0.982058] spi-nand spi0.0: 128 MiB, block size: 128 KiB, page size: 2048, OOB size: 64
[    0.991395] 1 fixed-partitions partitions found on MTD device spi0.0
[    0.997830] Creating 1 MTD partitions on "spi0.0":
[    1.002673] 0x000000f20000-0x000008000000 : "root"
[    1.208563] libphy: Fixed MDIO Bus: probed
[    1.214054] libphy: MACB_mii_bus: probed
[    1.218270] phy probe
[    1.221277] macb 1f2a2000.emac eth0: Cadence MACB rev 0x00000000 at 0x1f2a2000 irq 58 (00:30:00:00:02:db)
[    1.231864] usbcore: registered new interface driver rtl8192cu
[    1.237805] usbcore: registered new interface driver asix
[    1.243274] usbcore: registered new interface driver ax88179_178a
[    1.249413] usbcore: registered new interface driver cdc_ether
[    1.255310] usbcore: registered new interface driver rndis_host
[    1.261256] fotg210_hcd: FOTG210 Host Controller (EHCI) Driver
[    1.267504] need fusbh200 code here 5600
[    1.271464] getting port 0
[    1.274308] fotg210-hcd 1f284800.uhc: Faraday USB2.0 Host Controller
[    1.280702] fotg210-hcd 1f284800.uhc: new USB bus registered, assigned bus number 1
[    1.288520] fotg210-hcd 1f284800.uhc: irq 62, io mem 0x1f284800
[    1.304537] fotg210-hcd 1f284800.uhc: USB 2.0 started, EHCI 1.00
[    1.311371] hub 1-0:1.0: USB hub found
[    1.315245] hub 1-0:1.0: 1 port detected
[    1.319772] usbcore: registered new interface driver cdc_acm
[    1.325485] cdc_acm: USB Abstract Control Model driver for USB modems and ISDN adapters
[    1.333575] usbcore: registered new interface driver cdc_wdm
[    1.339308] usbcore: registered new interface driver usb-storage
[    1.345448] usbcore: registered new interface driver usbserial_generic
[    1.352023] usbserial: USB Serial support registered for generic
[    1.358114] usbcore: registered new interface driver cp210x
[    1.363747] usbserial: USB Serial support registered for cp210x
[    1.369718] usbcore: registered new interface driver option
[    1.375354] usbserial: USB Serial support registered for GSM modem (1-port)
[    1.382444] usbcore: registered new interface driver usb_serial_simple
[    1.389020] usbserial: USB Serial support registered for carelink
[    1.395174] usbserial: USB Serial support registered for zio
[    1.400871] usbserial: USB Serial support registered for funsoft
[    1.406932] usbserial: USB Serial support registered for flashloader
[    1.413352] usbserial: USB Serial support registered for google
[    1.419322] usbserial: USB Serial support registered for libtransistor
[    1.425919] usbserial: USB Serial support registered for vivopay
[    1.431972] usbserial: USB Serial support registered for moto_modem
[    1.438304] usbserial: USB Serial support registered for motorola_tetra
[    1.444978] usbserial: USB Serial support registered for novatel_gps
[    1.451374] usbserial: USB Serial support registered for hp4x
[    1.457175] usbserial: USB Serial support registered for suunto
[    1.463149] usbserial: USB Serial support registered for siemens_mpi
[    1.470954] msc313e-rtc 1f002400.rtc: char device (253:0)
[    1.470984] msc313e-rtc 1f002400.rtc: registered as rtc0
[    1.476391] msc313e-rtc 1f002400.rtc: setting system clock to 2020-12-29T14:04:23 UTC (1609250663)
[    1.485765] i2c /dev entries driver
[    1.695421] rtc rtc1: alarm rollover: day
[    1.736591] rtc-isl1208 1-006f: char device (253:1)
[    1.736607] rtc-isl1208 1-006f: registered as rtc1
[    1.742151] Driver for 1-wire Dallas network protocol.
[    1.749780] cpufreq: cpufreq_online: CPU0: Running at unlisted initial frequency: 999999 KHz, changing to: 1000000 KHz
[    1.762491] msc313-sha 1f224420.sha: will run requests pump with realtime priority
[    1.780295] value 0:d5ca
[    1.782873] value 1:935f
[    1.785417] value 2:341e
[    1.787958] value 3:839d
[    1.790498] value 4:a23c
[    1.793053] value 5:bd10
[    1.795595] value 6:69a7
[    1.798135] value 7:898f
[    1.800676] value 8:944e
[    1.803232] value 9:8209
[    1.805774] value 10:dc00
[    1.808403] value 11:7950
[    1.811031] value 12:17aa
[    1.813669] value 13:5e8a
[    1.816301] value 14:3a2e
[    1.818930] value 15:3872
[    1.922156] in: 00 out: 00
[    1.924900] in: 00 out: 00
[    1.927616] in: 00 out: 00
[    1.930330] in: 00 out: 00
[    1.933055] in: 00 out: 00
[    1.935770] in: 00 out: 00
[    1.938484] in: 00 out: 00
[    1.941198] in: 00 out: 00
[    1.943922] in: 00 out: 00
[    1.946637] in: 00 out: 00
[    1.949352] in: 00 out: 00
[    1.952066] in: 00 out: 00
[    1.954789] in: 00 out: 00
[    1.957505] in: 00 out: 00
[    1.960218] in: 00 out: 00
[    1.962941] in: 00 out: 00
[    1.965656] in: 00 out: 00
[    1.968371] in: 00 out: 00
[    1.971086] in: 00 out: 00
[    1.973809] in: 00 out: 00
[    1.976523] in: 00 out: 00
[    1.979238] in: 00 out: 00
[    1.981953] in: 00 out: 00
[    1.984682] in: 00 out: 00
[    1.987397] in: 00 out: 00
[    1.990112] in: 00 out: 00
[    1.992835] in: 00 out: 00
[    1.995551] in: 00 out: 00
[    1.998265] in: 00 out: 00
[    2.000978] in: 00 out: 00
[    2.003701] in: 00 out: 00
[    2.006417] in: 00 out: 00
[    2.009130] in: 00 out: 00
[    2.011844] in: 00 out: 00
[    2.014567] in: 00 out: 00
[    2.017282] in: 00 out: 00
[    2.019995] in: 00 out: 00
[    2.022718] in: 00 out: 00
[    2.025432] in: 00 out: 00
[    2.028147] in: 00 out: 00
[    2.030862] in: 00 out: 00
[    2.033585] in: 00 out: 00
[    2.036299] in: 00 out: 00
[    2.039014] in: 00 out: 00
[    2.041728] in: 00 out: 00
[    2.044455] in: 00 out: 00
[    2.047171] in: 00 out: 00
[    2.049885] in: 00 out: 00
[    2.052608] in: 00 out: 00
[    2.055323] in: 00 out: 00
[    2.058037] in: 00 out: 00
[    2.060752] in: 00 out: 00
[    2.063475] in: 00 out: 00
[    2.066190] in: 00 out: 00
[    2.068905] in: 00 out: 00
[    2.071619] in: 00 out: 00
[    2.074350] in: 00 out: 00
[    2.077066] in: 00 out: 00
[    2.079779] in: 00 out: 00
[    2.082508] in: 00 out: 00
[    2.085225] in: 00 out: 00
[    2.087939] in: 00 out: 00
[    2.090652] in: 00 out: 00
[    2.093376] in: 00 out: 00
[    2.096091] in: 00 out: 00
[    2.098805] in: 00 out: 00
[    2.101520] in: 00 out: 00
[    2.104248] in: 00 out: 00
[    2.106963] in: 00 out: 00
[    2.109677] in: 00 out: 00
[    2.112390] in: 00 out: 00
[    2.115113] in: 00 out: 00
[    2.117828] in: 00 out: 00
[    2.120543] in: 00 out: 00
[    2.123266] in: 00 out: 00
[    2.125981] in: 00 out: 00
[    2.128695] in: 00 out: 00
[    2.131409] in: 00 out: 00
[    2.134133] in: 00 out: 00
[    2.136848] in: 00 out: 00
[    2.139562] in: 00 out: 00
[    2.142275] in: 00 out: 00
[    2.144999] in: 00 out: 00
[    2.147714] in: 00 out: 00
[    2.150428] in: 00 out: 00
[    2.153151] in: 00 out: 00
[    2.155866] in: 00 out: 00
[    2.158580] in: 00 out: 00
[    2.161295] in: 00 out: 00
[    2.164025] in: 00 out: 00
[    2.166741] in: 00 out: 00
[    2.169455] in: 00 out: 00
[    2.172168] in: 00 out: 00
[    2.174893] in: 00 out: 00
[    2.177609] in: 00 out: 00
[    2.180323] in: 00 out: 00
[    2.183047] in: 00 out: 00
[    2.185762] in: 00 out: 00
[    2.188476] in: 00 out: 00
[    2.191190] in: 00 out: 00
[    2.193913] in: 00 out: 00
[    2.196628] in: 00 out: 00
[    2.199342] in: 00 out: 00
[    2.202056] in: 00 out: 00
[    2.204779] in: 00 out: 00
[    2.207493] in: 00 out: 00
[    2.210207] in: 00 out: 00
[    2.212931] in: 00 out: 00
[    2.215646] in: 00 out: 00
[    2.218360] in: 00 out: 00
[    2.221073] in: 00 out: 00
[    2.223802] in: 00 out: 00
[    2.226518] in: 00 out: 00
[    2.229232] in: 00 out: 00
[    2.231946] in: 00 out: 00
[    2.234670] in: 00 out: 00
[    2.237385] in: 00 out: 00
[    2.240098] in: 00 out: 00
[    2.242822] in: 00 out: 00
[    2.245537] in: 00 out: 00
[    2.248251] in: 00 out: 00
[    2.250965] in: 00 out: 00
[    2.253688] in: 00 out: 00
[    2.256402] in: 00 out: 00
[    2.259116] in: 00 out: 00
[    2.261830] in: 00 out: 00
[    2.264552] in: 00 out: 00
[    2.267267] in: 00 out: 00
[    2.290520] 0 0
[    2.292291] l 49859
[    2.294409] l 0
[    2.296168] 4 0
[    2.297925] l 49859
[    2.300029] l 0
[    2.301785] 8 0
[    2.303551] l 49859
[    2.305658] l 0
[    2.307414] 12 0
[    2.309257] l 49859
[    2.311362] l 0
[    2.313128] 16 0
[    2.314973] l 49859
[    2.317077] l 0
[    2.318834] 20 0
[    2.320677] l 49859
[    2.322791] l 0
[    2.324548] 24 0
[    2.326392] l 49859
[    2.328496] l 0
[    2.330252] 28 0
[    2.332095] l 49859
[    2.334209] l 0
[    2.335966] 32 0
[    2.337810] l 49859
[    2.339915] l 0
[    2.341671] 36 0
[    2.343529] l 49859
[    2.345634] l 0
[    2.347390] 40 0
[    2.349233] l 49859
[    2.351338] l 0
[    2.353103] 44 0
[    2.354947] l 49859
[    2.357052] l 0
[    2.358808] 48 0
[    2.360651] l 49859
[    2.362765] l 0
[    2.364521] 52 0
[    2.366366] l 49859
[    2.368470] l 0
[    2.370226] 56 0
[    2.372070] l 49859
[    2.374184] l 0
[    2.375942] 60 0
[    2.377785] l 49859
[    2.379890] l 0
[    2.381645] rsa: 0 ff:c3
[    2.384196] rsa: 1 fe:c2
[    2.386738] rsa: 2 fd:0
[    2.389192] rsa: 3 fc:0
[    2.391645] rsa: 4 fb:c3
[    2.394195] rsa: 5 fa:c2
[    2.396736] rsa: 6 f9:0
[    2.399190] rsa: 7 f8:0
[    2.401643] rsa: 8 f7:c3
[    2.404197] rsa: 9 f6:c2
[    2.406740] rsa: 10 f5:0
[    2.409281] rsa: 11 f4:0
[    2.411822] rsa: 12 f3:c3
[    2.414459] rsa: 13 f2:c2
[    2.417089] rsa: 14 f1:0
[    2.419629] rsa: 15 f0:0
[    2.422170] rsa: 16 ef:c3
[    2.424808] rsa: 17 ee:c2
[    2.427437] rsa: 18 ed:0
[    2.429978] rsa: 19 ec:0
[    2.432528] rsa: 20 eb:c3
[    2.435157] rsa: 21 ea:c2
[    2.437785] rsa: 22 e9:0
[    2.440326] rsa: 23 e8:0
[    2.442876] rsa: 24 e7:c3
[    2.445506] rsa: 25 e6:c2
[    2.448134] rsa: 26 e5:0
[    2.450675] rsa: 27 e4:0
[    2.453224] rsa: 28 e3:c3
[    2.455853] rsa: 29 e2:c2
[    2.458481] rsa: 30 e1:0
[    2.461022] rsa: 31 e0:0
[    2.463576] rsa: 32 df:c3
[    2.466205] rsa: 33 de:c2
[    2.468833] rsa: 34 dd:0
[    2.471374] rsa: 35 dc:0
[    2.473925] rsa: 36 db:c3
[    2.476554] rsa: 37 da:c2
[    2.479181] rsa: 38 d9:0
[    2.481722] rsa: 39 d8:0
[    2.484272] rsa: 40 d7:c3
[    2.486902] rsa: 41 d6:c2
[    2.489530] rsa: 42 d5:0
[    2.492071] rsa: 43 d4:0
[    2.494621] rsa: 44 d3:c3
[    2.497250] rsa: 45 d2:c2
[    2.499878] rsa: 46 d1:0
[    2.502429] rsa: 47 d0:0
[    2.504971] rsa: 48 cf:c3
[    2.507599] rsa: 49 ce:c2
[    2.510227] rsa: 50 cd:0
[    2.512777] rsa: 51 cc:0
[    2.515319] rsa: 52 cb:c3
[    2.517947] rsa: 53 ca:c2
[    2.520575] rsa: 54 c9:0
[    2.523130] rsa: 55 c8:0
[    2.525672] rsa: 56 c7:c3
[    2.528299] rsa: 57 c6:c2
[    2.530927] rsa: 58 c5:0
[    2.533478] rsa: 59 c4:0
[    2.536020] rsa: 60 c3:c3
[    2.538648] rsa: 61 c2:c2
[    2.541276] rsa: 62 c1:0
[    2.543827] rsa: 63 c0:0
[    2.547264] remoteproc remoteproc0: pm51 is available
[    2.553034] msc313-miu 1f202000.miu: Looking up ddr-supply from device tree
[    2.553195] msc313-miu 1f202000.miu: Memory type is DDR3, 8 banks and 10 columns, 16 bit bus
[    2.561670] msc313-miu 1f202000.miu: trcd: 13, trp: 13, tras: 32, trrd: 6, trtp: 7, trc: 45
[    2.571632] sar: int: 7
[    2.574317] usbcore: registered new interface driver snd-usb-audio
[    2.581635] NET: Registered protocol family 10
[    2.587226] Segment Routing with IPv6
[    2.590989] NET: Registered protocol family 17
[    2.595666] Registering SWP/SWPB emulation handler
[    2.601437] Loading compiled-in X.509 certificates
[    2.613309] sd_vdd: 3300 mV, disabled
[    2.613496] reg-fixed-voltage fixedregulator@0: sd_vdd supplying 3300000uV
[    2.613877] ubi0: attaching mtd1
[    9.949199] ubi0: scanning is finished
[   10.045005] ubi0: attached mtd1 (name "root", size 112 MiB)
[   10.050617] ubi0: PEB size: 131072 bytes (128 KiB), LEB size: 126976 bytes
[   10.057553] ubi0: min./max. I/O unit sizes: 2048/2048, sub-page size 2048
[   10.064387] ubi0: VID header offset: 2048 (aligned 2048), data offset: 4096
[   10.071373] ubi0: good PEBs: 903, bad PEBs: 0, corrupted PEBs: 0
[   10.077419] ubi0: user volume: 2, internal volumes: 1, max. volumes count: 128
[   10.084684] ubi0: max/mean erase counter: 1/0, WL threshold: 4096, image sequence number: 1103272162
[   10.093856] ubi0: available PEBs: 217, total reserved PEBs: 686, PEBs reserved for bad PEB handling: 20
[   10.103307] ubi0: background thread "ubi_bgt0d" started, PID 88
[   10.109799] block ubiblock0_1: created from ubi0:1(root)
[   10.115708] cfg80211: Loading compiled-in X.509 certificates for regulatory database
[   10.125411] cfg80211: Loaded X.509 cert 'sforshee: 00b28ddf47aef9cea7'
[   10.131998] clk: Not disabling unused clocks
[   10.136328] ALSA device list:
[   10.139308]   No soundcards found.
[   10.142945] platform regulatory.0: Direct firmware load for regulatory.db failed with error -2
[   10.151595] cfg80211: failed to load regulatory.db
[   10.207286] VFS: Mounted root (squashfs filesystem) readonly on device 254:0.
[   10.241282] devtmpfs: mounted
[   10.245250] Freeing unused kernel memory: 1024K
[   10.249960] Run /sbin/init as init process
[   10.254089]   with arguments:
[   10.254097]     /sbin/init
[   10.254102]     earlyprintk
[   10.254107]   with environment:
[   10.254112]     HOME=/
[   10.254117]     TERM=linux
[   12.525462] MTD: Couldn't look up '/dev/mtdblock5': -2
[   13.143124] Doing phy power up
[   13.146233] macb 1f2a2000.emac eth0: PHY [1f2a2000.emac-ffffffff:00] driver [msc313 phy] (irq=POLL)
[   13.155482] macb 1f2a2000.emac eth0: configuring for phy/mii link mode
[   13.162093] Doing phy power up
[   14.361141] random: crng init done
[   15.272817] macb 1f2a2000.emac eth0: Link is Up - 100Mbps/Full - flow control tx
[   15.280380] IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready
[   40.152574] sd_vdd: disabling
```
