# VDEC

https://github.com/ZYCX8888/Democode-TAKOYAKI-BETA001-0312/blob/d5841ab9fde1771b72aa842fc48a01bb832d4a0a/sdk/verify/feature/vdec/cnm_sw/vpuapi/wave/wave5_regdefine.h

## Memory map

For i2m:

- 0x1f344000 - SRAM? mm maybe not

my u-boot

```
=> md.l 0x1f344000
1f344000: b06e0000 b06e0000 59461677 59461677    ..n...n.w.FYw.FY
1f344010: 5fe40000 5fe40000 93b614e8 93b614e8    ..._..._........
1f344020: 2fd30000 2fd30000 5bf53123 5bf53123    .../.../#1.[#1.[
1f344030: 228c0000 228c0000 6954f1d4 6954f1d4    ..."..."..Ti..Ti
1f344040: a7940000 a7940000 bee37f57 bee37f57    ........W...W...
1f344050: 54910000 54910000 8f500db3 8f500db3    ...T...T..P...P.
1f344060: e9550000 e9550000 d4f6ff15 d4f6ff15    ..U...U.........
1f344070: ff350000 ff350000 4778c55c 4778c55c    ..5...5.\.xG\.xG
1f344080: d1930000 d1930000 c0538022 c0538022    ........".S.".S.
1f344090: 84cd0000 84cd0000 6b97f57f 6b97f57f    ...........k...k
1f3440a0: 29150000 29150000 cc019049 cc019049    ...)...)I...I...
1f3440b0: 4d170000 4d170000 596db758 596db758    ...M...MX.mYX.mY
1f3440c0: 4f120000 4f120000 90f517d5 90f517d5    ...O...O........
1f3440d0: f0db0000 f0db0000 7300b6d3 7300b6d3    ...........s...s
1f3440e0: 075e0000 075e0000 bd24ed14 bd24ed14    ..^...^...$...$.
1f3440f0: 182f0000 182f0000 72d045a3 72d045a3    ../.../..E.r.E.r
```

their u-boot

```
SigmaStar # md.l 0x1f344000
1f344000: dd760000 dd760000 bbe72e07 bbe72e07    ..v...v.........
1f344010: fa0d0000 fa0d0000 663fea9c 663fea9c    ..........?f..?f
1f344020: 05080000 05080000 dab2ed7d dab2ed7d    ........}...}...
1f344030: a2540000 a2540000 555f15cf 555f15cf    ..T...T..._U.._U
1f344040: 06920000 06920000 7df92b94 7df92b94    .........+.}.+.}
1f344050: 55910000 55910000 58fb1266 58fb1266    ...U...Uf..Xf..X
1f344060: 77280000 77280000 5567936d 5567936d    ..(w..(wm.gUm.gU
1f344070: 7c560000 7c560000 095feafc 095feafc    ..V|..V|.._..._.
1f344080: ddcc0000 ddcc0000 9bb345e8 9bb345e8    .........E...E..
1f344090: d63c0000 d63c0000 0e6d2a98 0e6d2a98    ..<...<..*m..*m.
1f3440a0: 79240000 79240000 6983bc19 6983bc19    ..$y..$y...i...i
1f3440b0: 3b650000 3b650000 7847a7d1 7847a7d1    ..e;..e;..Gx..Gx
1f3440c0: 3b6a0000 3b6a0000 7d1a7087 7d1a7087    ..j;..j;.p.}.p.}
1f3440d0: 1b920000 1b920000 7d6c75e6 7d6c75e6    .........ul}.ul}
1f3440e0: 53290000 53290000 3b890f99 3b890f99    ..)S..)S...;...;
1f3440f0: 534a0000 534a0000 feb3516c feb3516c    ..JS..JSlQ..lQ..
```

their kernel before playing

```
/ # BASE=0x1f344000; for X in `seq 0 63`; do A=$(($BASE + (4 * $X))); V=`devmem $A`; printf "0x%X - %s\n" $A $V; done
0x1F344000 - 0x534A0000
0x1F344004 - 0x534A0000
0x1F344008 - 0xFEB3516C
0x1F34400C - 0xFEB3516C
0x1F344010 - 0x534A0000
0x1F344014 - 0x534A0000
0x1F344018 - 0xFEB3516C
0x1F34401C - 0xFEB3516C
0x1F344020 - 0x534A0000
0x1F344024 - 0x534A0000
0x1F344028 - 0xFEB3516C
0x1F34402C - 0xFEB3516C
0x1F344030 - 0x534A0000
0x1F344034 - 0x534A0000
0x1F344038 - 0xFEB3516C
0x1F34403C - 0xFEB3516C
0x1F344040 - 0x534A0000
0x1F344044 - 0x534A0000
0x1F344048 - 0xFEB3516C
0x1F34404C - 0xFEB3516C
0x1F344050 - 0x534A0000
0x1F344054 - 0x534A0000
0x1F344058 - 0xFEB3516C
0x1F34405C - 0xFEB3516C
0x1F344060 - 0x534A0000
0x1F344064 - 0x534A0000
0x1F344068 - 0xFEB3516C
0x1F34406C - 0xFEB3516C
0x1F344070 - 0x534A0000
0x1F344074 - 0x534A0000
0x1F344078 - 0xFEB3516C
0x1F34407C - 0xFEB3516C
0x1F344080 - 0x534A0000
0x1F344084 - 0x534A0000
0x1F344088 - 0xFEB3516C
0x1F34408C - 0xFEB3516C
0x1F344090 - 0x534A0000
0x1F344094 - 0x534A0000
0x1F344098 - 0xFEB3516C
0x1F34409C - 0xFEB3516C
0x1F3440A0 - 0x534A0000
0x1F3440A4 - 0x534A0000
0x1F3440A8 - 0xFEB3516C
0x1F3440AC - 0xFEB3516C
0x1F3440B0 - 0x534A0000
0x1F3440B4 - 0x534A0000
0x1F3440B8 - 0xFEB3516C
0x1F3440BC - 0xFEB3516C
0x1F3440C0 - 0x534A0000
0x1F3440C4 - 0x534A0000
0x1F3440C8 - 0xFEB3516C
0x1F3440CC - 0xFEB3516C
0x1F3440D0 - 0x534A0000
0x1F3440D4 - 0x534A0000
0x1F3440D8 - 0xFEB3516C
0x1F3440DC - 0xFEB3516C
0x1F3440E0 - 0x534A0000
0x1F3440E4 - 0x534A0000
0x1F3440E8 - 0xFEB3516C
0x1F3440EC - 0xFEB3516C
0x1F3440F0 - 0x534A0000
0x1F3440F4 - 0x534A0000
0x1F3440F8 - 0xFEB3516C
0x1F3440FC - 0xFEB3516C
```

their kernel, playing

```
/ # BASE=0x1f344000; for X in `seq 0 63`; do A=$(($BASE + (4 * $X))); V=`devmem $A`; printf "0x%X - %s\n" $A $V; done
0x1F344000 - 0x534A0000
0x1F344004 - 0x534A0000
0x1F344008 - 0xFEB3516C
0x1F34400C - 0xFEB3516C
0x1F344010 - 0x534A0000
0x1F344014 - 0x534A0000
0x1F344018 - 0xFEB3516C
0x1F34401C - 0xFEB3516C
0x1F344020 - 0x534A0000
0x1F344024 - 0x534A0000
0x1F344028 - 0xFEB3516C
0x1F34402C - 0xFEB3516C
0x1F344030 - 0x534A0000
0x1F344034 - 0x534A0000
0x1F344038 - 0xFEB3516C
0x1F34403C - 0xFEB3516C
0x1F344040 - 0x534A0000
0x1F344044 - 0x534A0000
0x1F344048 - 0xFEB3516C
0x1F34404C - 0xFEB3516C
0x1F344050 - 0x534A0000
0x1F344054 - 0x534A0000
0x1F344058 - 0xFEB3516C
0x1F34405C - 0xFEB3516C
0x1F344060 - 0x534A0000
0x1F344064 - 0x534A0000
0x1F344068 - 0xFEB3516C
0x1F34406C - 0xFEB3516C
0x1F344070 - 0x534A0000
0x1F344074 - 0x534A0000
0x1F344078 - 0xFEB3516C
0x1F34407C - 0xFEB3516C
0x1F344080 - 0x534A0000
0x1F344084 - 0x534A0000
0x1F344088 - 0xFEB3516C
0x1F34408C - 0xFEB3516C
0x1F344090 - 0x534A0000
0x1F344094 - 0x534A0000
0x1F344098 - 0xFEB3516C
0x1F34409C - 0xFEB3516C
0x1F3440A0 - 0x534A0000
0x1F3440A4 - 0x534A0000
0x1F3440A8 - 0xFEB3516C
0x1F3440AC - 0xFEB3516C
0x1F3440B0 - 0x534A0000
0x1F3440B4 - 0x534A0000
0x1F3440B8 - 0xFEB3516C
0x1F3440BC - 0xFEB3516C
0x1F3440C0 - 0x534A0000
0x1F3440C4 - 0x534A0000
0x1F3440C8 - 0xFEB3516C
0x1F3440CC - 0xFEB3516C
0x1F3440D0 - 0x534A0000
0x1F3440D4 - 0x534A0000
0x1F3440D8 - 0xFEB3516C
0x1F3440DC - 0xFEB3516C
0x1F3440E0 - 0x534A0000
0x1F3440E4 - 0x534A0000
0x1F3440E8 - 0xFEB3516C
0x1F3440EC - 0xFEB3516C
0x1F3440F0 - 0x534A0000
0x1F3440F4 - 0x534A0000
0x1F3440F8 - 0xFEB3516C
0x1F3440FC - 0xFEB3516C
```



- 0x1f344800 - Registers?

| offset | name        | 31 | 30 | 29 | 28                    | 27 | 26 | 25 | 24 | 23 | 22                     | 21 | 20 | 19 | 18 | 17 | 16               | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | value      | notes                            |
|--------|-------------|----|----|----|-----------------------|----|----|----|----|----|------------------------|----|----|----|----|----|------------------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|---|------------|----------------------------------|
| 0x4    | VCPU_CUR_PC |    |    |    |                       |    |    |    |    |    |                        |    |    |    |    |    |                  |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |            |                                  |
| 0x98   | CONFIG0     |    |    |    | support vcpu backbone |    |    |    |    |    | support vcore backbone |    |    |    |    |    | support backbone |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | 0x80cf0980 | have vcore backbone and backbone |
| 0x9c   | CONFIG1     |    |    |    | support dual core     |    |    |    |    |    |                        |    |    |    |    |    |                  |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | 0x08018001 |                                  |

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

## PC?

Register 0x4 is the vcpu program counter.
Looks like it's doing .. something.

```
[   27.792694] vdi read 0x00000004:0x00007654
[   27.796832] vdi read 0x00000004:0x00003a46
[   27.800949] vdi read 0x00000004:0x00001360
[   27.805063] vdi read 0x00000004:0x00001364
[   27.809201] vdi read 0x00000004:0x0000135e
[   27.813317] vdi read 0x00000004:0x0001d2ba
[   27.817450] vdi read 0x00000004:0x00001360
[   27.821567] vdi read 0x00000004:0x00003a5e
[   27.825681] vdi read 0x00000004:0x00001358
[   27.829819] vdi read 0x00000004:0x0000135a
[   27.833935] vdi read 0x00000004:0x00001352
[   27.838076] vdi read 0x00000004:0x00007f3c
[   27.842194] vdi read 0x00000004:0x00001360
[   27.846308] vdi read 0x00000004:0x00003a3a
[   27.850446] vdi read 0x00000004:0x00003a4c
[   27.854562] vdi read 0x00000004:0x00001360
[   27.858695] vdi read 0x00000004:0x000089d8
[   27.862812] vdi read 0x00000004:0x0000135e
[   27.866949] vdi read 0x00000004:0x00001352
[   27.871067] vdi read 0x00000004:0x000089d8
[   27.875181] vdi read 0x00000004:0x00003a9c
[   27.879313] vdi read 0x00000004:0x00001366
[   27.883430] vdi read 0x00000004:0x00001354
[   27.887567] vdi read 0x00000004:0x000089d8
[   27.891685] vdi read 0x00000004:0x00001354
[   27.895799] vdi read 0x00000004:0x0000135c
[   27.899940] vdi read 0x00000004:0x00003a50
[   27.904057] vdi read 0x00000004:0x0000135c
[   27.908195] vdi read 0x00000004:0x00001358
[   27.912312] vdi read 0x00000004:0x00003a48
[   27.916426] vdi read 0x00000004:0x00003a5a
[   27.920559] vdi read 0x00000004:0x00001362
[   27.924676] vdi read 0x00000004:0x00007644
[   27.928813] vdi read 0x00000004:0x00003a4e
[   27.932929] vdi read 0x00000004:0x0000135c
[   27.937062] vdi read 0x00000004:0x00007f42
[   27.941178] vdi read 0x00000004:0x00001362
[   27.945293] vdi read 0x00000004:0x00001356
[   27.949430] vdi read 0x00000004:0x00001356
[   27.953546] vdi read 0x00000004:0x0001d2a8
[   27.957688] vdi read 0x00000004:0x00001362
[   27.961805] vdi read 0x00000004:0x00007f12
[   27.965918] vdi read 0x00000004:0x00003a46
[   27.970056] vdi read 0x00000004:0x00003a54
[   27.974173] vdi read 0x00000004:0x00001364
[   27.978307] vdi read 0x00000004:0x00007654
[   27.982423] vdi read 0x00000004:0x00001362
[   27.986561] vdi read 0x00000004:0x00001362
[   27.990678] vdi read 0x00000004:0x00003aa2
[   27.994792] vdi read 0x00000004:0x0000801c
[   27.998930] vdi read 0x00000004:0x00003a64
[   28.003046] vdi read 0x00000004:0x00001364
[   28.007181] vdi read 0x00000004:0x00001356
[   28.011298] vdi read 0x00000004:0x00001352
[   28.015412] vdi read 0x00000004:0x00003a40
[   28.019553] vdi read 0x00000004:0x00001362
[   28.023670] vdi read 0x00000004:0x000089d8
[   28.027808] vdi read 0x00000004:0x0000808e
[   28.031924] vdi read 0x00000004:0x00001354
[   28.036039] vdi read 0x00000004:0x00001358
[   28.040171] vdi read 0x00000004:0x000036e4
[   28.044288] vdi read 0x00000004:0x0000135c
[   28.048425] vdi read 0x00000004:0x00001356
[   28.052542] vdi read 0x00000004:0x00001368
[   28.056675] vdi read 0x00000004:0x00001356
[   28.060791] vdi read 0x00000004:0x0000135a
[   28.064905] vdi read 0x00000004:0x000089d8
[   28.069043] vdi read 0x00000004:0x0001d2a8
[   28.073161] vdi read 0x00000004:0x00001364
[   28.077302] vdi read 0x00000004:0x0000399c
[   28.081419] vdi read 0x00000004:0x00001356
[   28.085534] vdi read 0x00000004:0x00001358
[   28.089673] vdi read 0x00000004:0x00003992
[   28.093790] vdi read 0x00000004:0x0000135e
[   28.097922] vdi read 0x00000004:0x00001366
[   28.102039] vdi read 0x00000004:0x00003a66
[   28.106153] vdi read 0x00000004:0x0000135a
[   28.110290] vdi read 0x00000004:0x00001358
[   28.114407] vdi read 0x00000004:0x00001352
[   28.118540] vdi read 0x00000004:0x00007f10
[   28.122656] vdi read 0x00000004:0x00001366
[   28.126793] vdi read 0x00000004:0x00001352
[   28.130909] vdi read 0x00000004:0x00007644
[   28.135024] vdi read 0x00000004:0x0001d2c0
[   28.139166] vdi read 0x00000004:0x00001358
[   28.143282] vdi read 0x00000004:0x00003a3e
[   28.147421] vdi read 0x00000004:0x00001358
[   28.151537] vdi read 0x00000004:0x00001366
[   28.155652] vdi read 0x00000004:0x0000801c
[   28.159784] vdi read 0x00000004:0x00001358
[   28.163901] vdi read 0x00000004:0x00001362
[   28.168038] vdi read 0x00000004:0x00001366
[   28.172155] vdi read 0x00000004:0x0000801a
[   28.176269] vdi read 0x00000004:0x00001362
[   28.180402] vdi read 0x00000004:0x00001368
[   28.184519] vdi read 0x00000004:0x00001354
[   28.188658] vdi read 0x00000004:0x0000135e
[   28.192775] vdi read 0x00000004:0x00003a3e
[   28.196917] vdi read 0x00000004:0x0000135c
[   28.201034] vdi read 0x00000004:0x00003a46
[   28.205148] vdi read 0x00000004:0x0001d2a8
[   28.209287] vdi read 0x00000004:0x00001364
[   28.213404] vdi read 0x00000004:0x0001d2b4
[   28.217538] vdi read 0x00000004:0x00001360
[   28.221654] vdi read 0x00000004:0x00003988
[   28.225769] vdi read 0x00000004:0x00003a46
[   28.229907] vdi read 0x00000004:0x00007652
[   28.234024] vdi read 0x00000004:0x0000135e
[   28.238157] vdi read 0x00000004:0x00003a42
[   28.242273] vdi read 0x00000004:0x00001360
[   28.246387] vdi read 0x00000004:0x00001352
[   28.250525] vdi read 0x00000004:0x00001360
[   28.254641] vdi read 0x00000004:0x00003a46
[   28.258783] vdi read 0x00000004:0x0000135e
[   28.262900] vdi read 0x00000004:0x00003a3e
[   28.267038] vdi read 0x00000004:0x00003a3e
[   28.271154] vdi read 0x00000004:0x00001364
[   28.275269] vdi read 0x00000004:0x00001366
[   28.279408] vdi read 0x00000004:0x00008662
[   28.283526] vdi read 0x00000004:0x00001354
[   28.287664] vdi read 0x00000004:0x0000135a
[   28.291781] vdi read 0x00000004:0x0000808c
[   28.295895] vdi read 0x00000004:0x00001352
[   28.300028] vdi read 0x00000004:0x0000135a
[   28.304145] vdi read 0x00000004:0x00001360
[   28.308283] vdi read 0x00000004:0x00001364
[   28.312399] vdi read 0x00000004:0x00001366
[   28.316539] vdi read 0x00000004:0x00003a46
[   28.320656] vdi read 0x00000004:0x00001360
[   28.324770] vdi read 0x00000004:0x0000135a
[   28.328909] vdi read 0x00000004:0x00001366
[   28.333025] vdi read 0x00000004:0x0000135c
[   28.337157] vdi read 0x00000004:0x0000135a
[   28.341274] vdi read 0x00000004:0x00007644
[   28.345388] vdi read 0x00000004:0x00007f42
[   28.349526] vdi read 0x00000004:0x00001354
[   28.353642] vdi read 0x00000004:0x0000135a
[   28.357780] vdi read 0x00000004:0x0000135c
[   28.361896] vdi read 0x00000004:0x00003a3e
[   28.366011] vdi read 0x00000004:0x0000135a
[   28.370148] vdi read 0x00000004:0x00001354
[   28.374265] vdi read 0x00000004:0x00001360
[   28.378406] vdi read 0x00000004:0x0000135c
[   28.382523] vdi read 0x00000004:0x00001362
[   28.386662] vdi read 0x00000004:0x000036b0
[   28.390778] vdi read 0x00000004:0x00001360
[   28.394892] vdi read 0x00000004:0x0000135a
[   28.399025] vdi read 0x00000004:0x00007f3c
[   28.403142] vdi read 0x00000004:0x00001356
[   28.407279] vdi read 0x00000004:0x00001352
[   28.411395] vdi read 0x00000004:0x00001354
[   28.415510] vdi read 0x00000004:0x000036fe
[   28.419642] vdi read 0x00000004:0x00001364
[   28.423759] vdi read 0x00000004:0x00001362
[   28.427897] vdi read 0x00000004:0x000089d8
[   28.432013] vdi read 0x00000004:0x00001352
[   28.436128] vdi read 0x00000004:0x0000135e
[   28.440270] vdi read 0x00000004:0x00003a42
[   28.444387] vdi read 0x00000004:0x00001358
[   28.448525] vdi read 0x00000004:0x00001366
[   28.452642] vdi read 0x00000004:0x00003a46
[   28.456775] vdi read 0x00000004:0x00001360
[   28.460891] vdi read 0x00000004:0x00007644
[   28.465006] vdi read 0x00000004:0x0000867a
[   28.469144] vdi read 0x00000004:0x00001352
[   28.473261] vdi read 0x00000004:0x0000135a
[   28.477393] vdi read 0x00000004:0x00003a50
[   28.481509] vdi read 0x00000004:0x0000135a
[   28.485623] vdi read 0x00000004:0x00001366
[   28.489761] vdi read 0x00000004:0x00001362
[   28.493877] vdi read 0x00000004:0x00003a4a
[   28.498018] vdi read 0x00000004:0x0000135e
[   28.502135] vdi read 0x00000004:0x00003a54
[   28.506250] vdi read 0x00000004:0x0000801c
[   28.510389] vdi read 0x00000004:0x00001366
[   28.514505] vdi read 0x00000004:0x0000135e
[   28.518638] vdi read 0x00000004:0x0000135e
[   28.522755] vdi read 0x00000004:0x00001352
[   28.526892] vdi read 0x00000004:0x0000135c
[   28.531008] vdi read 0x00000004:0x00007644
[   28.535123] vdi read 0x00000004:0x00001362
[   28.539255] vdi read 0x00000004:0x00001354
[   28.543371] vdi read 0x00000004:0x00003a3e
[   28.547509] vdi read 0x00000004:0x00003a3e
[   28.551627] vdi read 0x00000004:0x00001360
[   28.555741] vdi read 0x00000004:0x00007f34
[   28.559882] vdi read 0x00000004:0x0000135a
[   28.563999] vdi read 0x00000004:0x00001364
[   28.568137] vdi read 0x00000004:0x00007f42
[   28.572254] vdi read 0x00000004:0x00001360
[   28.576369] vdi read 0x00000004:0x00001356
[   28.580502] vdi read 0x00000004:0x00007644
[   28.584618] vdi read 0x00000004:0x0000135a
[   28.588756] vdi read 0x00000004:0x00001356
[   28.592872] vdi read 0x00000004:0x0000399c
[   28.597005] vdi read 0x00000004:0x0000135a
[   28.601121] vdi read 0x00000004:0x00001354
[   28.605235] vdi read 0x00000004:0x0001d2be
[   28.609374] vdi read 0x00000004:0x00003a9c
[   28.613490] vdi read 0x00000004:0x0000135a
[   28.617632] vdi read 0x00000004:0x00003a42
[   28.621749] vdi read 0x00000004:0x00001364
[   28.625863] vdi read 0x00000004:0x00001362
[   28.630001] vdi read 0x00000004:0x00001352
[   28.634117] vdi read 0x00000004:0x00003a4e
[   28.638250] vdi read 0x00000004:0x00001352
[   28.642367] vdi read 0x00000004:0x00003a46
[   28.646504] vdi read 0x00000004:0x00007644
[   28.650621] vdi read 0x00000004:0x00001356
[   28.654736] vdi read 0x00000004:0x0000135e
[   28.658868] vdi read 0x00000004:0x00003a4e
[   28.662984] vdi read 0x00000004:0x00001362
[   28.667122] vdi read 0x00000004:0x00001366
[   28.671239] vdi read 0x00000004:0x00003a42
[   28.675354] vdi read 0x00000004:0x0000135c
[   28.679495] vdi read 0x00000004:0x0000135a
[   28.683612] vdi read 0x00000004:0x0001d346
[   28.687751] vdi read 0x00000004:0x0000135e
[   28.691867] vdi read 0x00000004:0x00001354
[   28.695981] vdi read 0x00000004:0x000036e4
[   28.700114] vdi read 0x00000004:0x00001362
[   28.704230] vdi read 0x00000004:0x00001364
[   28.708368] vdi read 0x00000004:0x0000135a
[   28.712485] vdi read 0x00000004:0x00001356
[   28.716618] vdi read 0x00000004:0x0000135a
[   28.720734] vdi read 0x00000004:0x00007f20
[   28.724849] vdi read 0x00000004:0x00001356
[   28.728987] vdi read 0x00000004:0x00001360
[   28.733104] vdi read 0x00000004:0x00007f42
[   28.737245] vdi read 0x00000004:0x00001354
[   28.741362] vdi read 0x00000004:0x000036a6
[   28.745476] vdi read 0x00000004:0x00003a4e
[   28.749614] vdi read 0x00000004:0x00003a4e
[   28.753731] vdi read 0x00000004:0x00001364
[   28.757863] vdi read 0x00000004:0x0000808c
[   28.761979] vdi read 0x00000004:0x00001362
[   28.766094] vdi read 0x00000004:0x00001362
[   28.770231] vdi read 0x00000004:0x00001354
[   28.774348] vdi read 0x00000004:0x0000764a
[   28.778480] vdi read 0x00000004:0x00001356
[   28.782598] vdi read 0x00000004:0x0000764c
[   28.786736] vdi read 0x00000004:0x00007644
[   28.790853] vdi read 0x00000004:0x0000135e
[   28.794966] vdi read 0x00000004:0x0000135e
[   28.799107] vdi read 0x00000004:0x00008688
[   28.803224] vdi read 0x00000004:0x00001362
[   28.807363] vdi read 0x00000004:0x00001352
[   28.811479] vdi read 0x00000004:0x00003a40
[   28.815593] vdi read 0x00000004:0x00003a6a
[   28.819726] vdi read 0x00000004:0x00001364
[   28.823842] vdi read 0x00000004:0x00003a42
[   28.827980] vdi read 0x00000004:0x00007644
[   28.832097] vdi read 0x00000004:0x00001364
[   28.836211] vdi read 0x00000004:0x00001354
[   28.840343] vdi read 0x00000004:0x00003a9c
[   28.844459] vdi read 0x00000004:0x00001358
[   28.848596] vdi read 0x00000004:0x00001364
[   28.852712] vdi read 0x00000004:0x00001362
[   28.856854] vdi read 0x00000004:0x00001362
[   28.860971] vdi read 0x00000004:0x0000135e
[   28.865085] vdi read 0x00000004:0x0000764a
[   28.869223] vdi read 0x00000004:0x00003a42
[   28.873340] vdi read 0x00000004:0x00001358
[   28.877473] vdi read 0x00000004:0x00003700
[   28.881590] vdi read 0x00000004:0x00001358
[   28.885705] vdi read 0x00000004:0x0000135e
[   28.889842] vdi read 0x00000004:0x00001354
[   28.893958] vdi read 0x00000004:0x00007648
[   28.898090] vdi read 0x00000004:0x00001356
[   28.902207] vdi read 0x00000004:0x000089d6
[   28.906322] vdi read 0x00000004:0x00003a3e
[   28.910460] vdi read 0x00000004:0x0001d2be
[   28.914577] vdi read 0x00000004:0x0000135c
[   28.918719] vdi read 0x00000004:0x00007f2e
[   28.922836] vdi read 0x00000004:0x00001362
[   28.926974] vdi read 0x00000004:0x00001356
[   28.931090] vdi read 0x00000004:0x00003a6a
[   28.935205] vdi read 0x00000004:0x00001362
[   28.939338] vdi read 0x00000004:0x00007f3c
[   28.943455] vdi read 0x00000004:0x00001352
[   28.947593] vdi read 0x00000004:0x00001362
[   28.951710] vdi read 0x00000004:0x0000399c
[   28.955824] vdi read 0x00000004:0x00007644
[   28.959956] vdi read 0x00000004:0x0000135c
[   28.964073] vdi read 0x00000004:0x00003a34
[   28.968211] vdi read 0x00000004:0x0000764c
[   28.972328] vdi read 0x00000004:0x00001358
[   28.976442] vdi read 0x00000004:0x00001364
[   28.980582] vdi read 0x00000004:0x0000764a
[   28.984699] vdi read 0x00000004:0x00001362
[   28.988837] vdi read 0x00000004:0x0000135a
[   28.992954] vdi read 0x00000004:0x00003a46
[   28.997087] vdi read 0x00000004:0x00001360
[   29.001204] vdi read 0x00000004:0x000036fe
[   29.005318] vdi read 0x00000004:0x00008678
[   29.009455] vdi read 0x00000004:0x00003a3e
[   29.013572] vdi read 0x00000004:0x00001358
[   29.017709] vdi read 0x00000004:0x00001352
[   29.021826] vdi read 0x00000004:0x00007648
[   29.025940] vdi read 0x00000004:0x00008662
[   29.030078] vdi read 0x00000004:0x00007648
[   29.034195] vdi read 0x00000004:0x00001356
[   29.038336] vdi read 0x00000004:0x00007652
[   29.042454] vdi read 0x00000004:0x00001364
[   29.046592] vdi read 0x00000004:0x00001352
[   29.050709] vdi read 0x00000004:0x00001356
[   29.054824] vdi read 0x00000004:0x00001352
[   29.058957] vdi read 0x00000004:0x00003a4a
[   29.063073] vdi read 0x00000004:0x00001354
[   29.067211] vdi read 0x00000004:0x0000135e
[   29.071329] vdi read 0x00000004:0x00003a3e
[   29.075444] vdi read 0x00000004:0x0000135c
[   29.079576] vdi read 0x00000004:0x0000135a
[   29.083694] vdi read 0x00000004:0x00001358
[   29.087832] vdi read 0x00000004:0x00001354
[   29.091950] vdi read 0x00000004:0x0000801c
[   29.096064] vdi read 0x00000004:0x00003a9e
[   29.100205] vdi read 0x00000004:0x0000135e
[   29.104323] vdi read 0x00000004:0x00003a3e
[   29.108462] vdi read 0x00000004:0x0000135c
[   29.112578] vdi read 0x00000004:0x00001364
[   29.116711] vdi read 0x00000004:0x0001d346
[   29.120828] vdi read 0x00000004:0x00001358
[   29.124943] vdi read 0x00000004:0x00003a4a
[   29.129081] vdi read 0x00000004:0x00008662
[   29.133198] vdi read 0x00000004:0x00001358
[   29.137331] vdi read 0x00000004:0x00007f42
[   29.141447] vdi read 0x00000004:0x00001356
[   29.145561] vdi read 0x00000004:0x00001352
[   29.149699] vdi read 0x00000004:0x00001364
[   29.153815] vdi read 0x00000004:0x00003a42
[   29.157956] vdi read 0x00000004:0x00001356
[   29.162073] vdi read 0x00000004:0x0001d2ca
[   29.166188] vdi read 0x00000004:0x00007644
[   29.170326] vdi read 0x00000004:0x00007f10
[   29.174443] vdi read 0x00000004:0x0000135a
[   29.178576] vdi read 0x00000004:0x00007648
[   29.182692] vdi read 0x00000004:0x00001358
[   29.186830] vdi read 0x00000004:0x00001362
[   29.190947] vdi read 0x00000004:0x00007648
[   29.195061] vdi read 0x00000004:0x00003966
[   29.199194] vdi read 0x00000004:0x00001358
[   29.203311] vdi read 0x00000004:0x00003a46
[   29.207448] vdi read 0x00000004:0x00007652
[   29.211565] vdi read 0x00000004:0x00001362
[   29.215680] vdi read 0x00000004:0x00003988
[   29.219822] vdi read 0x00000004:0x00001352
[   29.223940] vdi read 0x00000004:0x00003a3e
[   29.228078] vdi read 0x00000004:0x00008678
[   29.232195] vdi read 0x00000004:0x0000135c
[   29.236309] vdi read 0x00000004:0x00001352
[   29.240442] vdi read 0x00000004:0x00007f14
[   29.244558] vdi read 0x00000004:0x00001364
[   29.248696] vdi read 0x00000004:0x0000135e
[   29.252814] vdi read 0x00000004:0x0000135c
[   29.256947] vdi read 0x00000004:0x00001362
[   29.261063] vdi read 0x00000004:0x00008662
[   29.265178] vdi read 0x00000004:0x00001362
[   29.269316] vdi read 0x00000004:0x00001360
[   29.273432] vdi read 0x00000004:0x0000135e
[   29.277573] vdi read 0x00000004:0x00003a82
[   29.281690] vdi read 0x00000004:0x0000135e
[   29.285804] vdi read 0x00000004:0x0001d2a6
[   29.289942] vdi read 0x00000004:0x00007648
[   29.294059] vdi read 0x00000004:0x00001358
[   29.298192] vdi read 0x00000004:0x0000135a
[   29.302308] vdi read 0x00000004:0x0000801c
[   29.306423] vdi read 0x00000004:0x0000135e
[   29.310561] vdi read 0x00000004:0x00001364
[   29.314677] vdi read 0x00000004:0x00007644
[   29.318810] vdi read 0x00000004:0x00001364
[   29.322926] vdi read 0x00000004:0x0000135c
[   29.327064] vdi read 0x00000004:0x0000135c
[   29.331180] vdi read 0x00000004:0x00001354
[   29.335296] vdi read 0x00000004:0x00001354
[   29.339437] vdi read 0x00000004:0x00007648
[   29.343553] vdi read 0x00000004:0x00001366
[   29.347692] vdi read 0x00000004:0x00001360
[   29.351808] vdi read 0x00000004:0x00003a4e
[   29.355923] vdi read 0x00000004:0x00007f16
[   29.360055] vdi read 0x00000004:0x00001356
[   29.364172] vdi read 0x00000004:0x00003a3e
[   29.368310] vdi read 0x00000004:0x00003a40
[   29.372427] vdi read 0x00000004:0x00001354
[   29.376560] vdi read 0x00000004:0x00008682
[   29.380676] vdi read 0x00000004:0x00001360
[   29.384790] vdi read 0x00000004:0x00001358
[   29.388928] vdi read 0x00000004:0x00001354
[   29.393044] vdi read 0x00000004:0x00003a9c
[   29.397185] vdi read 0x00000004:0x00001358
[   29.401302] vdi read 0x00000004:0x00003a38
[   29.405416] vdi read 0x00000004:0x00008678
[   29.409554] vdi read 0x00000004:0x0001d2b4
[   29.413671] vdi read 0x00000004:0x00001356
[   29.417808] vdi read 0x00000004:0x00001364
[   29.421925] vdi read 0x00000004:0x00003a3a
[   29.426039] vdi read 0x00000004:0x0000135c
[   29.430177] vdi read 0x00000004:0x00001358
[   29.434293] vdi read 0x00000004:0x00001352
[   29.438426] vdi read 0x00000004:0x0000866c
[   29.442534] vdi read 0x00000004:0x00001360
[   29.446672] vdi read 0x00000004:0x00001352
[   29.450790] vdi read 0x00000004:0x00001354
[   29.454904] vdi read 0x00000004:0x00001354
[   29.459045] vdi read 0x00000004:0x00003972
[   29.463162] vdi read 0x00000004:0x00001360
[   29.467301] vdi read 0x00000004:0x00001366
[   29.471418] vdi read 0x00000004:0x00007652
[   29.475532] vdi read 0x00000004:0x0000764c
[   29.479665] vdi read 0x00000004:0x0000135c
[   29.483781] vdi read 0x00000004:0x00003a3e
[   29.487919] vdi read 0x00000004:0x00003a3c
[   29.492035] vdi read 0x00000004:0x00001364
[   29.496149] vdi read 0x00000004:0x00001354
[   29.500286] vdi read 0x00000004:0x00001360
[   29.504403] vdi read 0x00000004:0x00003a4a
[   29.508541] vdi read 0x00000004:0x00003a50
[   29.512657] vdi read 0x00000004:0x00001356
[   29.516798] vdi read 0x00000004:0x000089d8
[   29.520915] vdi read 0x00000004:0x00001354
[   29.525029] vdi read 0x00000004:0x00001360
[   29.529168] vdi read 0x00000004:0x00001354
[   29.533284] vdi read 0x00000004:0x00003a46
[   29.537417] vdi read 0x00000004:0x00001358
[   29.541534] vdi read 0x00000004:0x00007644
[   29.545649] vdi read 0x00000004:0x00003a6a
[   29.549786] vdi read 0x00000004:0x00008678
[   29.553902] vdi read 0x00000004:0x00001362
[   29.558035] vdi read 0x00000004:0x00003a4c
[   29.562152] vdi read 0x00000004:0x00001352
[   29.566266] vdi read 0x00000004:0x00001362
[   29.570403] vdi read 0x00000004:0x0000135c
[   29.574520] vdi read 0x00000004:0x00003a3e
[   29.578661] vdi read 0x00000004:0x00001364
[   29.582779] vdi read 0x00000004:0x00007644
[   29.586918] vdi read 0x00000004:0x0000135c
[   29.591035] vdi read 0x00000004:0x0000801c
[   29.595149] vdi read 0x00000004:0x00003a3e
[   29.599282] vdi read 0x00000004:0x00001358
[   29.603399] vdi read 0x00000004:0x00007648
[   29.607537] vdi read 0x00000004:0x00003a3e
[   29.611653] vdi read 0x00000004:0x00001354
[   29.615767] vdi read 0x00000004:0x00001360
[   29.619900] vdi read 0x00000004:0x00003a34
[   29.624016] vdi read 0x00000004:0x0000135c
[   29.628154] vdi read 0x00000004:0x0000135a
[   29.632270] vdi read 0x00000004:0x00003990
[   29.636384] vdi read 0x00000004:0x00007644
[   29.640526] vdi read 0x00000004:0x00001362
[   29.644643] vdi read 0x00000004:0x00003a3e
[   29.648781] vdi read 0x00000004:0x00007652
[   29.652898] vdi read 0x00000004:0x00001354
[   29.657031] vdi read 0x00000004:0x00003a3e
[   29.661147] vdi read 0x00000004:0x0000135c
[   29.665263] vdi read 0x00000004:0x00001352
[   29.669400] vdi read 0x00000004:0x00001354
[   29.673516] vdi read 0x00000004:0x00007654
[   29.677649] vdi read 0x00000004:0x00001364
[   29.681765] vdi read 0x00000004:0x00007644
[   29.685880] vdi read 0x00000004:0x00007648
[   29.690018] vdi read 0x00000004:0x0001d2aa
[   29.694134] vdi read 0x00000004:0x00001366
[   29.698276] vdi read 0x00000004:0x00008666
[   29.702393] vdi read 0x00000004:0x00001358
[   29.706530] vdi read 0x00000004:0x00001360
[   29.710647] vdi read 0x00000004:0x00003a3e
[   29.714761] vdi read 0x00000004:0x00001364
[   29.718894] vdi read 0x00000004:0x00001358
[   29.723010] vdi read 0x00000004:0x00003a3e
[   29.727149] vdi read 0x00000004:0x00001352
[   29.731265] vdi read 0x00000004:0x00001358
[   29.735379] vdi read 0x00000004:0x000036d6
[   29.739512] vdi read 0x00000004:0x00001364
[   29.743628] vdi read 0x00000004:0x00001354
[   29.747765] vdi read 0x00000004:0x00001356
[   29.751883] vdi read 0x00000004:0x0001d2a8
[   29.755997] vdi read 0x00000004:0x00001366
[   29.760138] vdi read 0x00000004:0x00001356
[   29.764255] vdi read 0x00000004:0x00001362
[   29.768393] vdi read 0x00000004:0x00001352
[   29.772510] vdi read 0x00000004:0x000036ac
[   29.776644] vdi read 0x00000004:0x00001356
[   29.780760] vdi read 0x00000004:0x00001360
[   29.784874] vdi read 0x00000004:0x00007652
[   29.789012] vdi read 0x00000004:0x00003aa2
[   29.793128] vdi read 0x00000004:0x0000135a
[   29.797262] vdi read 0x00000004:0x00007f1c
[   29.801378] vdi read 0x00000004:0x00001360
[   29.805493] vdi read 0x00000004:0x00001362
[   29.809631] vdi read 0x00000004:0x00001366
[   29.813747] vdi read 0x00000004:0x00003a4c
[   29.817888] vdi read 0x00000004:0x0000135c
[   29.822005] vdi read 0x00000004:0x00003a9c
[   29.826119] vdi read 0x00000004:0x00003a4e
[   29.830257] vdi read 0x00000004:0x0000764a
[   29.834374] vdi read 0x00000004:0x00001364
[   29.838508] vdi read 0x00000004:0x00003a4c
[   29.842624] vdi read 0x00000004:0x00001362
[   29.846761] vdi read 0x00000004:0x00001354
[   29.850877] vdi read 0x00000004:0x0000764a
[   29.854991] vdi read 0x00000004:0x00008678
[   29.859124] vdi read 0x00000004:0x00001354
[   29.863241] vdi read 0x00000004:0x00003a4e
[   29.867380] vdi read 0x00000004:0x00003a46
[   29.871497] vdi read 0x00000004:0x00001356
[   29.875612] vdi read 0x00000004:0x00003a40
[   29.879753] vdi read 0x00000004:0x00001366
[   29.883870] vdi read 0x00000004:0x00003a42
[   29.888008] vdi read 0x00000004:0x000036e4
[   29.892125] vdi read 0x00000004:0x0000135e
[   29.896239] vdi read 0x00000004:0x0000135c
[   29.900372] vdi read 0x00000004:0x00003a40
[   29.904488] vdi read 0x00000004:0x0000135e
[   29.908625] vdi read 0x00000004:0x00001354
[   29.912742] vdi read 0x00000004:0x0000801c
[   29.916875] vdi read 0x00000004:0x00001354
[   29.920992] vdi read 0x00000004:0x00001356
[   29.925106] vdi read 0x00000004:0x00003a4a
[   29.929244] vdi read 0x00000004:0x00003a42
[   29.933360] vdi read 0x00000004:0x00001354
[   29.937503] vdi read 0x00000004:0x0000764c
[   29.941620] vdi read 0x00000004:0x00001356
[   29.945735] vdi read 0x00000004:0x00007f42
[   29.949874] vdi read 0x00000004:0x00003a42
[   29.953990] vdi read 0x00000004:0x00001352
[   29.958123] vdi read 0x00000004:0x0000801a
[   29.962240] vdi read 0x00000004:0x00001364
[   29.966354] vdi read 0x00000004:0x00001354
[   29.970491] vdi read 0x00000004:0x0000135a
[   29.974608] vdi read 0x00000004:0x00003a34
[   29.978741] vdi read 0x00000004:0x00001356
[   29.982857] vdi read 0x00000004:0x00001352
[   29.986994] vdi read 0x00000004:0x00001362
[   29.991110] vdi read 0x00000004:0x00003a3e
[   29.995225] vdi read 0x00000004:0x00001364
[   29.999366] vdi read 0x00000004:0x0000135c
[   30.003483] vdi read 0x00000004:0x00001358
[   30.007621] vdi read 0x00000004:0x00001364
[   30.011738] vdi read 0x00000004:0x00001364
[   30.015852] vdi read 0x00000004:0x00003a46
[   30.019984] vdi read 0x00000004:0x0000135c
[   30.024100] vdi read 0x00000004:0x00001356
[   30.028238] vdi read 0x00000004:0x0000135a
[   30.032354] vdi read 0x00000004:0x00007f34
[   30.036469] vdi read 0x00000004:0x00001354
[   30.040605] vdi read 0x00000004:0x00003a50
[   30.044720] vdi read 0x00000004:0x00001366
[   30.048857] vdi read 0x00000004:0x0000135e
[   30.052975] vdi read 0x00000004:0x00007648
[   30.057116] vdi read 0x00000004:0x00001366
[   30.061235] vdi read 0x00000004:0x00007f14
[   30.065349] vdi read 0x00000004:0x00001354
[   30.069487] vdi read 0x00000004:0x0000135e
[   30.073604] vdi read 0x00000004:0x0001d2b4
[   30.077737] vdi read 0x00000004:0x0000135e
[   30.081853] vdi read 0x00000004:0x0000135c
[   30.085967] vdi read 0x00000004:0x000036b0
[   30.090104] vdi read 0x00000004:0x000089d8
[   30.094221] vdi read 0x00000004:0x00001352
[   30.098358] vdi read 0x00000004:0x00001358
[   30.102475] vdi read 0x00000004:0x00001366
[   30.106610] vdi read 0x00000004:0x00001366
[   30.110727] vdi read 0x00000004:0x000036fe
[   30.114841] vdi read 0x00000004:0x0000764c
[   30.118982] vdi read 0x00000004:0x00001362
[   30.123099] vdi read 0x00000004:0x00007644
[   30.127238] vdi read 0x00000004:0x0001d2be
[   30.131355] vdi read 0x00000004:0x0000135a
[   30.135470] vdi read 0x00000004:0x0000764a
[   30.139602] vdi read 0x00000004:0x00001362
[   30.143719] vdi read 0x00000004:0x0000135a
[   30.147857] vdi read 0x00000004:0x00001362
[   30.151974] vdi read 0x00000004:0x00001360
[   30.156088] vdi read 0x00000004:0x0000135e
[   30.160220] vdi read 0x00000004:0x0001d2a8
[   30.164337] vdi read 0x00000004:0x00001358
[   30.168474] vdi read 0x00000004:0x00001366
[   30.172591] vdi read 0x00000004:0x000089d0
[   30.176735] vdi read 0x00000004:0x00001366
[   30.180852] vdi read 0x00000004:0x00003a9e
[   30.184966] vdi read 0x00000004:0x00008020
[   30.189105] vdi read 0x00000004:0x00001364
[   30.193222] vdi read 0x00000004:0x00003704
[   30.197355] vdi read 0x00000004:0x00001360
[   30.201471] vdi read 0x00000004:0x00001354
[   30.205586] vdi read 0x00000004:0x00003a46
[   30.209723] vdi read 0x00000004:0x00003a40
[   30.213840] vdi read 0x00000004:0x00001362
[   30.217972] vdi read 0x00000004:0x00001368
[   30.222089] vdi read 0x00000004:0x00001366
[   30.226203] vdi read 0x00000004:0x00001362
[   30.230340] vdi read 0x00000004:0x00001352
[   30.234458] vdi read 0x00000004:0x00008678
[   30.238600] vdi read 0x00000004:0x0000135a
[   30.242716] vdi read 0x00000004:0x00003a42
[   30.246855] vdi read 0x00000004:0x00007648
[   30.250973] vdi read 0x00000004:0x00001360
[   30.255087] vdi read 0x00000004:0x0001d2c8
[   30.259220] vdi read 0x00000004:0x0000135e
[   30.263336] vdi read 0x00000004:0x00001366
[   30.267475] vdi read 0x00000004:0x00001364
[   30.271591] vdi read 0x00000004:0x0000801e
[   30.275705] vdi read 0x00000004:0x00001362
[   30.279838] vdi read 0x00000004:0x0000135c
[   30.283955] vdi read 0x00000004:0x00001360
[   30.288092] vdi read 0x00000004:0x00001356
[   30.292209] vdi read 0x00000004:0x00001360
[   30.296323] vdi read 0x00000004:0x00007648
[   30.300465] vdi read 0x00000004:0x00001360
[   30.304581] vdi read 0x00000004:0x00007f14
[   30.308719] vdi read 0x00000004:0x00003996
[   30.312835] vdi read 0x00000004:0x00001352
[   30.316968] vdi read 0x00000004:0x00001358
[   30.321084] vdi read 0x00000004:0x00003a62
[   30.325199] vdi read 0x00000004:0x00001364
[   30.329336] vdi read 0x00000004:0x0000135a
[   30.333453] vdi read 0x00000004:0x00003980
[   30.337586] vdi read 0x00000004:0x00001352
[   30.341703] vdi read 0x00000004:0x0000135c
[   30.345817] vdi read 0x00000004:0x00003a34
[   30.349954] vdi read 0x00000004:0x00007f2e
[   30.354071] vdi read 0x00000004:0x00001362
[   30.358212] vdi read 0x00000004:0x00001362
[   30.362329] vdi read 0x00000004:0x0000135a
[   30.366443] vdi read 0x00000004:0x00001362
[   30.370581] vdi read 0x00000004:0x00001360
[   30.374698] vdi read 0x00000004:0x00003a48
[   30.378831] vdi read 0x00000004:0x00001366
[   30.382947] vdi read 0x00000004:0x00001356
[   30.387084] vdi read 0x00000004:0x00001360
[   30.391201] vdi read 0x00000004:0x00001362
[   30.395315] vdi read 0x00000004:0x0000135c
[   30.399447] vdi read 0x00000004:0x0000135e
[   30.403564] vdi read 0x00000004:0x0000135e
[   30.407702] vdi read 0x00000004:0x0000134e
[   30.411818] vdi read 0x00000004:0x00001356
[   30.415932] vdi read 0x00000004:0x00007f10
[   30.420073] vdi read 0x00000004:0x00003a82
[   30.424190] vdi read 0x00000004:0x00001352
[   30.428328] vdi read 0x00000004:0x0000135e
[   30.432445] vdi read 0x00000004:0x00001356
[   30.436578] vdi read 0x00000004:0x00001362
[   30.440694] vdi read 0x00000004:0x0001d33e
[   30.444809] vdi read 0x00000004:0x00001366
[   30.448946] vdi read 0x00000004:0x0000135a
[   30.453063] vdi read 0x00000004:0x00007f14
[   30.457195] vdi read 0x00000004:0x00003966
[   30.461312] vdi read 0x00000004:0x0000135a
[   30.465426] vdi read 0x00000004:0x000036dc
[   30.469563] vdi read 0x00000004:0x00001356
[   30.473680] vdi read 0x00000004:0x0000808c
[   30.477822] vdi read 0x00000004:0x00001362
[   30.481938] vdi read 0x00000004:0x00001360
[   30.486054] vdi read 0x00000004:0x00001364
[   30.490191] vdi read 0x00000004:0x0000135c
[   30.494307] vdi read 0x00000004:0x00007f42
[   30.498440] vdi read 0x00000004:0x00001364
[   30.502556] vdi read 0x00000004:0x00001364
[   30.506694] vdi read 0x00000004:0x0000135e
[   30.510810] vdi read 0x00000004:0x00007f1a
[   30.514924] vdi read 0x00000004:0x00001358
[   30.519056] vdi read 0x00000004:0x00001352
[   30.523172] vdi read 0x00000004:0x00007648
[   30.527310] vdi read 0x00000004:0x00007654
[   30.531426] vdi read 0x00000004:0x00001362
[   30.535541] vdi read 0x00000004:0x00001360
[   30.539682] vdi read 0x00000004:0x00007652
[   30.543798] vdi read 0x00000004:0x00001354
[   30.547938] vdi read 0x00000004:0x00001356
[   30.552054] vdi read 0x00000004:0x00007644
[   30.556168] vdi read 0x00000004:0x00001354
[   30.560306] vdi read 0x00000004:0x00001364
[   30.564423] vdi read 0x00000004:0x00007644
[   30.568561] vdi read 0x00000004:0x00007644
[   30.572677] vdi read 0x00000004:0x00001356
[   30.576810] vdi read 0x00000004:0x00001356
[   30.580926] vdi read 0x00000004:0x00003a82
[   30.585040] vdi read 0x00000004:0x00001366
[   30.589178] vdi read 0x00000004:0x00001358
[   30.593294] vdi read 0x00000004:0x00001356
[   30.597436] vdi read 0x00000004:0x00001364
[   30.601553] vdi read 0x00000004:0x00007f34
[   30.605668] vdi read 0x00000004:0x00003a46
[   30.609806] vdi read 0x00000004:0x00003a3e
[   30.613922] vdi read 0x00000004:0x00001364
[   30.618055] vdi read 0x00000004:0x00003a4e
[   30.622171] vdi read 0x00000004:0x00001356
[   30.626285] vdi read 0x00000004:0x00001362
[   30.630423] vdi read 0x00000004:0x00001356
[   30.634539] vdi read 0x00000004:0x00007648
[   30.638672] vdi read 0x00000004:0x00001356
[   30.642788] vdi read 0x00000004:0x00001354
[   30.646926] vdi read 0x00000004:0x00001358
[   30.651042] vdi read 0x00000004:0x0001d2b0
[   30.655157] vdi read 0x00000004:0x00001362
[   30.659298] vdi read 0x00000004:0x000036b0
[   30.663415] vdi read 0x00000004:0x00001356
[   30.667553] vdi read 0x00000004:0x00001358
[   30.671669] vdi read 0x00000004:0x0001d346
[   30.675784] vdi read 0x00000004:0x00008688
[   30.679916] vdi read 0x00000004:0x0000135e
[   30.684033] vdi read 0x00000004:0x00003a4c
[   30.688171] vdi read 0x00000004:0x00003a3e
[   30.692287] vdi read 0x00000004:0x00001360
[   30.696402] vdi read 0x00000004:0x0000135c
[   30.700534] vdi read 0x00000004:0x00003a54
[   30.704651] vdi read 0x00000004:0x00001358
[   30.708788] vdi read 0x00000004:0x00001360
[   30.712905] vdi read 0x00000004:0x00007f42
[   30.717046] vdi read 0x00000004:0x0000135a
[   30.721163] vdi read 0x00000004:0x00001360
[   30.725277] vdi read 0x00000004:0x00003a3e
[   30.729415] vdi read 0x00000004:0x00008672
[   30.733532] vdi read 0x00000004:0x0000135e
[   30.737665] vdi read 0x00000004:0x00008678
[   30.741781] vdi read 0x00000004:0x00001366
[   30.745896] vdi read 0x00000004:0x00001366
[   30.750033] vdi read 0x00000004:0x00001360
[   30.754149] vdi read 0x00000004:0x00008682
[   30.758282] vdi read 0x00000004:0x00001354
[   30.762399] vdi read 0x00000004:0x0001d2be
[   30.766537] vdi read 0x00000004:0x0000764a
[   30.770654] vdi read 0x00000004:0x00001358
[   30.774768] vdi read 0x00000004:0x0000135a
[   30.778909] vdi read 0x00000004:0x00003a38
[   30.783026] vdi read 0x00000004:0x00001352
[   30.787164] vdi read 0x00000004:0x00001364
[   30.791281] vdi read 0x00000004:0x00003a38
[   30.795395] vdi read 0x00000004:0x00001364
[   30.799527] vdi read 0x00000004:0x00001356
[   30.803644] vdi read 0x00000004:0x00003a3e
[   30.807781] vdi read 0x00000004:0x00003a3e
[   30.811898] vdi read 0x00000004:0x00001366
[   30.816013] vdi read 0x00000004:0x0000135c
[   30.820145] vdi read 0x00000004:0x00003a62
[   30.824262] vdi read 0x00000004:0x0000135c
[   30.828399] vdi read 0x00000004:0x00001360
[   30.832516] vdi read 0x00000004:0x00003a3e
[   30.836657] vdi read 0x00000004:0x00001358
[   30.840774] vdi read 0x00000004:0x00007644
[   30.844888] vdi read 0x00000004:0x00003a46
[   30.849026] vdi read 0x00000004:0x00003a4e
[   30.853142] vdi read 0x00000004:0x0000135a
[   30.857275] vdi read 0x00000004:0x00003a3e
[   30.861391] vdi read 0x00000004:0x00001364
[   30.865505] vdi read 0x00000004:0x00001352
[   30.869642] vdi read 0x00000004:0x00001358
[   30.873758] vdi read 0x00000004:0x00003996
[   30.877891] vdi read 0x00000004:0x0000135e
[   30.882008] vdi read 0x00000004:0x00001352
[   30.886122] vdi read 0x00000004:0x0000801a
[   30.890258] vdi read 0x00000004:0x0000135a
[   30.894375] vdi read 0x00000004:0x0000135e
[   30.898516] vdi read 0x00000004:0x00001362
[   30.902633] vdi read 0x00000004:0x00008686
[   30.906770] vdi read 0x00000004:0x00007f10
[   30.910887] vdi read 0x00000004:0x00001366
[   30.915001] vdi read 0x00000004:0x00001366
[   30.919134] vdi read 0x00000004:0x00007f34
[   30.923250] vdi read 0x00000004:0x00001356
[   30.927388] vdi read 0x00000004:0x00001362
[   30.931505] vdi read 0x00000004:0x00007f3e
[   30.935619] vdi read 0x00000004:0x00001358
[   30.939752] vdi read 0x00000004:0x00001362
[   30.943869] vdi read 0x00000004:0x00001354
[   30.948007] vdi read 0x00000004:0x00001360
[   30.952123] vdi read 0x00000004:0x00001358
[   30.956237] vdi read 0x00000004:0x00007f18
[   30.960380] vdi read 0x00000004:0x00001362
[   30.964496] vdi read 0x00000004:0x00003a46
[   30.968635] vdi read 0x00000004:0x00007644
[   30.972751] vdi read 0x00000004:0x0000135a
[   30.976885] vdi read 0x00000004:0x00008682
[   30.981001] vdi read 0x00000004:0x00001356
[   30.985115] vdi read 0x00000004:0x00001358
[   30.989254] vdi read 0x00000004:0x0000135e
[   30.993370] vdi read 0x00000004:0x00003a3e
[   30.997503] vdi read 0x00000004:0x00001358
[   31.001619] vdi read 0x00000004:0x00003996
[   31.005733] vdi read 0x00000004:0x00003a48
[   31.009870] vdi read 0x00000004:0x00007644
[   31.013987] vdi read 0x00000004:0x00001358
[   31.018128] vdi read 0x00000004:0x00003a3e
[   31.022245] vdi read 0x00000004:0x00001356
[   31.026361] vdi read 0x00000004:0x00001364
[   31.030498] vdi read 0x00000004:0x00003972
[   31.034615] vdi read 0x00000004:0x0000135c
[   31.038748] vdi read 0x00000004:0x0000135c
[   31.042864] vdi read 0x00000004:0x00003a3e
[   31.047002] vdi read 0x00000004:0x00007f28
[   31.051119] vdi read 0x00000004:0x00001364
[   31.055233] vdi read 0x00000004:0x00001366
[   31.059365] vdi read 0x00000004:0x00003a4a
[   31.063482] vdi read 0x00000004:0x00001354
[   31.067620] vdi read 0x00000004:0x00001356
[   31.071736] vdi read 0x00000004:0x00008678
[   31.075851] vdi read 0x00000004:0x00001358
[   31.079992] vdi read 0x00000004:0x0000135e
[   31.084109] vdi read 0x00000004:0x00001352
[   31.088248] vdi read 0x00000004:0x00001352
[   31.092364] vdi read 0x00000004:0x00003704
[   31.096497] vdi read 0x00000004:0x0000135e
[   31.100605] vdi read 0x00000004:0x00001352
[   31.104719] vdi read 0x00000004:0x000036d4
[   31.108857] vdi read 0x00000004:0x0000801a
[   31.112974] vdi read 0x00000004:0x0000135c
[   31.117107] vdi read 0x00000004:0x00001360
[   31.121223] vdi read 0x00000004:0x00001352
[   31.125337] vdi read 0x00000004:0x0000135e
[   31.129475] vdi read 0x00000004:0x00001356
[   31.133592] vdi read 0x00000004:0x00007648
[   31.137733] vdi read 0x00000004:0x00001360
[   31.141850] vdi read 0x00000004:0x00003704
[   31.145965] vdi read 0x00000004:0x00007644
[   31.150102] vdi read 0x00000004:0x00003a4a
[   31.154219] vdi read 0x00000004:0x00001354
[   31.158352] vdi read 0x00000004:0x00003aa2
[   31.162469] vdi read 0x00000004:0x0000135a
[   31.166607] vdi read 0x00000004:0x00001360
[   31.170723] vdi read 0x00000004:0x00007644
[   31.174837] vdi read 0x00000004:0x00007648
[   31.178970] vdi read 0x00000004:0x00001354
[   31.183087] vdi read 0x00000004:0x00003a4e
[   31.187224] vdi read 0x00000004:0x0000764c
[   31.191341] vdi read 0x00000004:0x0000135e
[   31.195457] vdi read 0x00000004:0x000089d8
[   31.199598] vdi read 0x00000004:0x00001366
[   31.203715] vdi read 0x00000004:0x00007f10
[   31.207854] vdi read 0x00000004:0x00003a3e
[   31.211970] vdi read 0x00000004:0x00001364
[   31.216085] vdi read 0x00000004:0x00001362
[   31.220218] vdi read 0x00000004:0x00007652
[   31.224336] vdi read 0x00000004:0x0000135c
[   31.228473] vdi read 0x00000004:0x0000135a
[   31.232590] vdi read 0x00000004:0x0000764c
[   31.236725] vdi read 0x00000004:0x000036b0
[   31.240841] vdi read 0x00000004:0x0000135c
[   31.244955] vdi read 0x00000004:0x0000135a
[   31.249093] vdi read 0x00000004:0x00001362
[   31.253210] vdi read 0x00000004:0x00007648
[   31.257352] vdi read 0x00000004:0x00001366
[   31.261468] vdi read 0x00000004:0x00007652
[   31.265582] vdi read 0x00000004:0x00003a4e
[   31.269721] vdi read 0x00000004:0x00001354
[   31.273838] vdi read 0x00000004:0x00001352
[   31.277971] vdi read 0x00000004:0x00007648
[   31.282087] vdi read 0x00000004:0x00001358
[   31.286201] vdi read 0x00000004:0x00001352
[   31.290339] vdi read 0x00000004:0x00001362
[   31.294455] vdi read 0x00000004:0x00003a3e
[   31.298601] vdi read 0x00000004:0x00008672
[   31.302718] vdi read 0x00000004:0x00001352
[   31.306858] vdi read 0x00000004:0x00003a34
[   31.310975] vdi read 0x00000004:0x0000135a
[   31.315090] vdi read 0x00000004:0x00001356
[   31.319237] vdi read 0x00000004:0x000036a8
[   31.323354] vdi read 0x00000004:0x0000135a
[   31.327493] vdi read 0x00000004:0x00001360
[   31.331609] vdi read 0x00000004:0x00003a34
[   31.335723] vdi read 0x00000004:0x00003a3e
[   31.339856] vdi read 0x00000004:0x00001358
[   31.343972] vdi read 0x00000004:0x00007644
[   31.348111] vdi read 0x00000004:0x0000764a
[   31.352227] vdi read 0x00000004:0x00001356
[   31.356341] vdi read 0x00000004:0x00001356
[   31.360474] vdi read 0x00000004:0x00007648
[   31.364591] vdi read 0x00000004:0x0000135c
[   31.368728] vdi read 0x00000004:0x00001356
[   31.372844] vdi read 0x00000004:0x00003a34
[   31.376986] vdi read 0x00000004:0x00001360
[   31.381103] vdi read 0x00000004:0x0001d2a8
[   31.385217] vdi read 0x00000004:0x00003a4c
[   31.389355] vdi read 0x00000004:0x00007654
[   31.393471] vdi read 0x00000004:0x00001352
[   31.397604] vdi read 0x00000004:0x00003a46
[   31.401721] vdi read 0x00000004:0x0000135e
[   31.405835] vdi read 0x00000004:0x0000135a
[   31.409973] vdi read 0x00000004:0x00001358
[   31.414089] vdi read 0x00000004:0x00003a42
[   31.418222] vdi read 0x00000004:0x00001352
[   31.422340] vdi read 0x00000004:0x00008678
[   31.426454] vdi read 0x00000004:0x00001364
[   31.430591] vdi read 0x00000004:0x00001352
[   31.434709] vdi read 0x00000004:0x000036a8
[   31.438851] vdi read 0x00000004:0x00001360
[   31.442968] vdi read 0x00000004:0x000036aa
[   31.447106] vdi read 0x00000004:0x0001d2b4
[   31.451222] vdi read 0x00000004:0x00001360
[   31.455337] vdi read 0x00000004:0x0000135a
[   31.459469] vdi read 0x00000004:0x00007648
[   31.463586] vdi read 0x00000004:0x00001360
[   31.467724] vdi read 0x00000004:0x00001360
[   31.471841] vdi read 0x00000004:0x00003a46
[   31.475955] vdi read 0x00000004:0x00007648
[   31.480088] vdi read 0x00000004:0x00001354
[   31.484204] vdi read 0x00000004:0x00003a4c
[   31.488342] vdi read 0x00000004:0x00003a3e
[   31.492458] vdi read 0x00000004:0x00001358
[   31.496599] vdi read 0x00000004:0x00001352
[   31.500716] vdi read 0x00000004:0x00001366
[   31.504830] vdi read 0x00000004:0x0000135c
[   31.508969] vdi read 0x00000004:0x00001354
[   31.513086] vdi read 0x00000004:0x00007648
[   31.517218] vdi read 0x00000004:0x00001366
[   31.521335] vdi read 0x00000004:0x00007654
[   31.525450] vdi read 0x00000004:0x0000808c
[   31.529587] vdi read 0x00000004:0x00008678
[   31.533703] vdi read 0x00000004:0x00001356
[   31.537836] vdi read 0x00000004:0x00007648
[   31.541952] vdi read 0x00000004:0x00001354
[   31.546066] vdi read 0x00000004:0x00001360
[   31.550203] vdi read 0x00000004:0x00001366
[   31.554320] vdi read 0x00000004:0x00003a4e
[   31.558462] vdi read 0x00000004:0x00001362
[   31.562579] vdi read 0x00000004:0x00003a54
[   31.566717] vdi read 0x00000004:0x00003a3e
[   31.570834] vdi read 0x00000004:0x0000135c
[   31.574948] vdi read 0x00000004:0x00001358
[   31.579085] vdi read 0x00000004:0x0000135a
[   31.583202] vdi read 0x00000004:0x00003a3e
[   31.587340] vdi read 0x00000004:0x00003aa2
[   31.591456] vdi read 0x00000004:0x00001352
[   31.595571] vdi read 0x00000004:0x0001d2a8
[   31.599704] vdi read 0x00000004:0x00001360
[   31.603821] vdi read 0x00000004:0x0001d2b4
[   31.607960] vdi read 0x00000004:0x00003a38
[   31.612077] vdi read 0x00000004:0x00001360
[   31.616191] vdi read 0x00000004:0x0000135c
[   31.620332] vdi read 0x00000004:0x00003a3e
[   31.624449] vdi read 0x00000004:0x0000135c
[   31.628588] vdi read 0x00000004:0x00001352
[   31.632705] vdi read 0x00000004:0x00001362
[   31.636838] vdi read 0x00000004:0x0000135c
[   31.640954] vdi read 0x00000004:0x00003a46
[   31.645069] vdi read 0x00000004:0x0000135e
[   31.649206] vdi read 0x00000004:0x00001354
[   31.653323] vdi read 0x00000004:0x0000135c
[   31.657455] vdi read 0x00000004:0x00003a3e
[   31.661572] vdi read 0x00000004:0x00001366
[   31.665686] vdi read 0x00000004:0x0000135e
[   31.669824] vdi read 0x00000004:0x00001368
[   31.673940] vdi read 0x00000004:0x0000764a
[   31.678081] vdi read 0x00000004:0x0000135c
[   31.682198] vdi read 0x00000004:0x00003a50
[   31.686312] vdi read 0x00000004:0x00001362
[   31.690450] vdi read 0x00000004:0x00001362
[   31.694567] vdi read 0x00000004:0x0000396e
[   31.698699] vdi read 0x00000004:0x0000808c
[   31.702816] vdi read 0x00000004:0x00001362
[   31.706953] vdi read 0x00000004:0x0000135c
[   31.711070] vdi read 0x00000004:0x00003a42
[   31.715184] vdi read 0x00000004:0x00001364
[   31.719317] vdi read 0x00000004:0x00001362
[   31.723433] vdi read 0x00000004:0x00007648
[   31.727570] vdi read 0x00000004:0x00008682
[   31.731687] vdi read 0x00000004:0x00001362
[   31.735801] vdi read 0x00000004:0x00001356
[   31.739943] vdi read 0x00000004:0x0000801e
[   31.744060] vdi read 0x00000004:0x0000135c
[   31.748198] vdi read 0x00000004:0x00001364
[   31.752315] vdi read 0x00000004:0x00001362
[   31.756429] vdi read 0x00000004:0x00001352
[   31.760561] vdi read 0x00000004:0x00001366
[   31.764678] vdi read 0x00000004:0x00001366
[   31.768815] vdi read 0x00000004:0x00008020
[   31.772932] vdi read 0x00000004:0x00001364
[   31.777064] vdi read 0x00000004:0x00007652
[   31.781181] vdi read 0x00000004:0x0000135c
[   31.785296] vdi read 0x00000004:0x0000135c
[   31.789434] vdi read 0x00000004:0x00001364
[   31.793550] vdi read 0x00000004:0x00001362
[   31.797691] vdi read 0x00000004:0x00001366
[   31.801808] vdi read 0x00000004:0x00007f42
[   31.805923] vdi read 0x00000004:0x0000135e
[   31.810061] vdi read 0x00000004:0x0000135e
[   31.814177] vdi read 0x00000004:0x00007f12
[   31.818310] vdi read 0x00000004:0x0000135a
[   31.822428] vdi read 0x00000004:0x0000808c
[   31.826565] vdi read 0x00000004:0x000036a8
[   31.830681] vdi read 0x00000004:0x00001356
[   31.834796] vdi read 0x00000004:0x00001366
[   31.838929] vdi read 0x00000004:0x00003704
[   31.843045] vdi read 0x00000004:0x00001356
[   31.847182] vdi read 0x00000004:0x00001366
[   31.851299] vdi read 0x00000004:0x000089da
[   31.855413] vdi read 0x00000004:0x00007644
[   31.859554] vdi read 0x00000004:0x00001352
[   31.863671] vdi read 0x00000004:0x0000399c
[   31.867811] vdi read 0x00000004:0x00003a3e
[   31.871927] vdi read 0x00000004:0x00001358
[   31.876041] vdi read 0x00000004:0x00001354
[   31.880174] vdi read 0x00000004:0x00003a3e
[   31.884290] vdi read 0x00000004:0x00001366
[   31.888428] vdi read 0x00000004:0x00001360
[   31.892544] vdi read 0x00000004:0x000036e4
[   31.896676] vdi read 0x00000004:0x00001358
[   31.900793] vdi read 0x00000004:0x00001360
[   31.904907] vdi read 0x00000004:0x00007652
[   31.909044] vdi read 0x00000004:0x0000801a
[   31.913161] vdi read 0x00000004:0x00001352
[   31.917302] vdi read 0x00000004:0x0000135c
[   31.921419] vdi read 0x00000004:0x00001352
[   31.925533] vdi read 0x00000004:0x00001364
[   31.929671] vdi read 0x00000004:0x00001362
[   31.933788] vdi read 0x00000004:0x00003a48
[   31.937921] vdi read 0x00000004:0x0000135e
[   31.942037] vdi read 0x00000004:0x000036a8
[   31.946151] vdi read 0x00000004:0x00003a4a
[   31.950288] vdi read 0x00000004:0x0000764a
[   31.954405] vdi read 0x00000004:0x00001360
[   31.958537] vdi read 0x00000004:0x00001362
[   31.962654] vdi read 0x00000004:0x0000134e
[   31.966792] vdi read 0x00000004:0x0000135e
[   31.970910] vdi read 0x00000004:0x00007648
[   31.975024] vdi read 0x00000004:0x00003a50
[   31.979165] vdi read 0x00000004:0x0000135e
[   31.983282] vdi read 0x00000004:0x00007644
[   31.987421] vdi read 0x00000004:0x0001d2a6
[   31.991538] vdi read 0x00000004:0x00001364
[   31.995653] vdi read 0x00000004:0x0000808c
[   31.999785] vdi read 0x00000004:0x00001366
[   32.003901] vdi read 0x00000004:0x0000135a
[   32.008039] vdi read 0x00000004:0x00001360
[   32.012155] vdi read 0x00000004:0x00007644
[   32.016270] vdi read 0x00000004:0x00001356
[   32.020402] vdi read 0x00000004:0x00001360
[   32.024519] vdi read 0x00000004:0x00008662
[   32.028657] vdi read 0x00000004:0x00001354
[   32.032774] vdi read 0x00000004:0x00001366
[   32.036915] vdi read 0x00000004:0x00007654
[   32.041032] vdi read 0x00000004:0x00001360
[   32.045146] vdi read 0x00000004:0x0001d346
[   32.049285] vdi read 0x00000004:0x00003a46
[   32.053402] vdi read 0x00000004:0x0000135e
[   32.057534] vdi read 0x00000004:0x0001d2ae
[   32.061650] vdi read 0x00000004:0x0000135e
[   32.065765] vdi read 0x00000004:0x00001352
[   32.069902] vdi read 0x00000004:0x00001358
[   32.074019] vdi read 0x00000004:0x0001d2a8
[   32.078152] vdi read 0x00000004:0x00001360
[   32.082268] vdi read 0x00000004:0x0000135c
[   32.086383] vdi read 0x00000004:0x00003a48
[   32.090522] vdi read 0x00000004:0x00007f14
[   32.094639] vdi read 0x00000004:0x00001356
[   32.098780] vdi read 0x00000004:0x00007f3a
[   32.102898] vdi read 0x00000004:0x00001352
[   32.107036] vdi read 0x00000004:0x0000135c
[   32.111153] vdi read 0x00000004:0x00001358
[   32.115267] vdi read 0x00000004:0x00001356
[   32.119404] vdi read 0x00000004:0x00001352
[   32.123520] vdi read 0x00000004:0x00003988
[   32.127658] vdi read 0x00000004:0x0001d2b4
[   32.131775] vdi read 0x00000004:0x00001358
[   32.135890] vdi read 0x00000004:0x00001362
[   32.140022] vdi read 0x00000004:0x0001d2c6
[   32.144139] vdi read 0x00000004:0x00001366
[   32.148277] vdi read 0x00000004:0x00001358
[   32.152394] vdi read 0x00000004:0x00003a4e
[   32.156534] vdi read 0x00000004:0x00001360
[   32.160652] vdi read 0x00000004:0x000036fe
[   32.164766] vdi read 0x00000004:0x00003a42
[   32.168904] vdi read 0x00000004:0x00003a40
[   32.173020] vdi read 0x00000004:0x00001360
[   32.177154] vdi read 0x00000004:0x00003a46
[   32.181271] vdi read 0x00000004:0x00001352
[   32.185386] vdi read 0x00000004:0x00001360
[   32.189523] vdi read 0x00000004:0x0000135a
[   32.193641] vdi read 0x00000004:0x00001364
[   32.197778] vdi read 0x00000004:0x00001356
[   32.201895] vdi read 0x00000004:0x00003972
[   32.206010] vdi read 0x00000004:0x00003a3e
[   32.210148] vdi read 0x00000004:0x00007f1c
[   32.214265] vdi read 0x00000004:0x0000135a
[   32.218406] vdi read 0x00000004:0x00008666
[   32.222523] vdi read 0x00000004:0x00001366
[   32.226661] vdi read 0x00000004:0x00001358
[   32.230778] vdi read 0x00000004:0x00008662
[   32.234892] vdi read 0x00000004:0x00001362
[   32.239025] vdi read 0x00000004:0x00001356
[   32.243143] vdi read 0x00000004:0x00001352
[   32.247281] vdi read 0x00000004:0x00001366
[   32.251399] vdi read 0x00000004:0x00003a3e
[   32.255513] vdi read 0x00000004:0x0000134e
[   32.259646] vdi read 0x00000004:0x0000135c
[   32.263762] vdi read 0x00000004:0x00003a3e
[   32.267900] vdi read 0x00000004:0x00003a40
[   32.272017] vdi read 0x00000004:0x00001360
[   32.276131] vdi read 0x00000004:0x00001362
[   32.280273] vdi read 0x00000004:0x00003a74
[   32.284389] vdi read 0x00000004:0x00001354
[   32.288528] vdi read 0x00000004:0x00003972
[   32.292645] vdi read 0x00000004:0x00001362
[   32.296778] vdi read 0x00000004:0x00001364
[   32.300894] vdi read 0x00000004:0x00003a6a
[   32.305008] vdi read 0x00000004:0x00001358
[   32.309146] vdi read 0x00000004:0x0000135c
[   32.313262] vdi read 0x00000004:0x0000396e
[   32.317395] vdi read 0x00000004:0x0000801c
[   32.321512] vdi read 0x00000004:0x0000135c
[   32.325626] vdi read 0x00000004:0x000036d4
[   32.329763] vdi read 0x00000004:0x0000135c
[   32.333880] vdi read 0x00000004:0x00001356
[   32.338021] vdi read 0x00000004:0x00001364
[   32.342138] vdi read 0x00000004:0x00001362
[   32.346253] vdi read 0x00000004:0x0000135c
[   32.350391] vdi read 0x00000004:0x00001352
[   32.354508] vdi read 0x00000004:0x00003a42
[   32.358640] vdi read 0x00000004:0x00001358
[   32.362757] vdi read 0x00000004:0x000089d8
[   32.366894] vdi read 0x00000004:0x00001352
[   32.371011] vdi read 0x00000004:0x00001364
[   32.375125] vdi read 0x00000004:0x00001352
[   32.379257] vdi read 0x00000004:0x0000135c
[   32.383373] vdi read 0x00000004:0x00007f42
[   32.387511] vdi read 0x00000004:0x00001352
[   32.391628] vdi read 0x00000004:0x00001352
[   32.395742] vdi read 0x00000004:0x0001d2a8
[   32.399883] vdi read 0x00000004:0x00001354
[   32.404000] vdi read 0x00000004:0x000036b0
[   32.408139] vdi read 0x00000004:0x00007644
[   32.412256] vdi read 0x00000004:0x00001366
[   32.416371] vdi read 0x00000004:0x00001356
[   32.420503] vdi read 0x00000004:0x0000764c
[   32.424620] vdi read 0x00000004:0x00001358
[   32.428758] vdi read 0x00000004:0x0000135c
[   32.432874] vdi read 0x00000004:0x00008686
[   32.437006] vdi read 0x00000004:0x00001360
[   32.441122] vdi read 0x00000004:0x00001354
[   32.445236] vdi read 0x00000004:0x00003a46
[   32.449375] vdi read 0x00000004:0x00007644
[   32.453491] vdi read 0x00000004:0x00001352
[   32.457632] vdi read 0x00000004:0x0001d2a6
[   32.461749] vdi read 0x00000004:0x00001366
[   32.465863] vdi read 0x00000004:0x0000135a
[   32.470001] vdi read 0x00000004:0x00001364
[   32.474118] vdi read 0x00000004:0x0000764a
[   32.478251] vdi read 0x00000004:0x00001360
[   32.482368] vdi read 0x00000004:0x0000764a
[   32.486506] vdi read 0x00000004:0x00003a46
[   32.490622] vdi read 0x00000004:0x00001364
[   32.494736] vdi read 0x00000004:0x00001362
[   32.498869] vdi read 0x00000004:0x00003a42
[   32.502986] vdi read 0x00000004:0x00001364
[   32.507124] vdi read 0x00000004:0x0000135a
[   32.511241] vdi read 0x00000004:0x00007644
[   32.515355] vdi read 0x00000004:0x00001356
[   32.519496] vdi read 0x00000004:0x0000135a
[   32.523613] vdi read 0x00000004:0x0000801c
[   32.527752] vdi read 0x00000004:0x00001364
[   32.531868] vdi read 0x00000004:0x0000135e
[   32.535982] vdi read 0x00000004:0x00003a48
[   32.540115] vdi read 0x00000004:0x00001364
[   32.544231] vdi read 0x00000004:0x00001354
[   32.548369] vdi read 0x00000004:0x00001352
[   32.552486] vdi read 0x00000004:0x0000135c
[   32.556618] vdi read 0x00000004:0x0000135a
[   32.560734] vdi read 0x00000004:0x00003a4c
[   32.564848] vdi read 0x00000004:0x0001d2b4
[   32.568986] vdi read 0x00000004:0x00003a60
[   32.573102] vdi read 0x00000004:0x00001352
[   32.577243] vdi read 0x00000004:0x00003a46
[   32.581361] vdi read 0x00000004:0x00001354
[   32.585475] vdi read 0x00000004:0x00001362
[   32.589613] vdi read 0x00000004:0x000089d8
[   32.593729] vdi read 0x00000004:0x00001352
[   32.597868] vdi read 0x00000004:0x0000135e
[   32.601985] vdi read 0x00000004:0x00007f28
[   32.606099] vdi read 0x00000004:0x00007644
[   32.610236] vdi read 0x00000004:0x00003a4a
[   32.614353] vdi read 0x00000004:0x00001354
[   32.618486] vdi read 0x00000004:0x00007648
[   32.622603] vdi read 0x00000004:0x00001366
[   32.626740] vdi read 0x00000004:0x00001360
[   32.630857] vdi read 0x00000004:0x000036a8
[   32.634971] vdi read 0x00000004:0x00008664
[   32.639112] vdi read 0x00000004:0x00001360
[   32.643229] vdi read 0x00000004:0x00008662
[   32.647368] vdi read 0x00000004:0x00007648
[   32.651484] vdi read 0x00000004:0x00001362
[   32.655598] vdi read 0x00000004:0x00001354
[   32.659731] vdi read 0x00000004:0x00003a3e
[   32.663847] vdi read 0x00000004:0x0000135c
[   32.667985] vdi read 0x00000004:0x0000135e
[   32.672102] vdi read 0x00000004:0x00008662
[   32.676216] vdi read 0x00000004:0x00008688
[   32.680348] vdi read 0x00000004:0x00001358
[   32.684464] vdi read 0x00000004:0x0001d33e
[   32.688602] vdi read 0x00000004:0x00007648
[   32.692719] vdi read 0x00000004:0x00001364
[   32.696860] vdi read 0x00000004:0x0000808c
[   32.700978] vdi read 0x00000004:0x00001354
[   32.705092] vdi read 0x00000004:0x00001354
[   32.709230] vdi read 0x00000004:0x00001366
[   32.713347] vdi read 0x00000004:0x00007644
[   32.717480] vdi read 0x00000004:0x00001358
[   32.721597] vdi read 0x00000004:0x00008678
[   32.725711] vdi read 0x00000004:0x00001356
[   32.729848] vdi read 0x00000004:0x00001352
[   32.733964] vdi read 0x00000004:0x00001360
[   32.738097] vdi read 0x00000004:0x00008662
[   32.742214] vdi read 0x00000004:0x00001366
[   32.746328] vdi read 0x00000004:0x00001360
[   32.750465] vdi read 0x00000004:0x00001362
[   32.754581] vdi read 0x00000004:0x00003a4c
[   32.758722] vdi read 0x00000004:0x00001366
[   32.762840] vdi read 0x00000004:0x00007644
[   32.766978] vdi read 0x00000004:0x00007644
[   32.771095] vdi read 0x00000004:0x00001366
[   32.775209] vdi read 0x00000004:0x00001360
[   32.779342] vdi read 0x00000004:0x0001d346
[   32.783458] vdi read 0x00000004:0x00001354
[   32.787596] vdi read 0x00000004:0x00001360
[   32.791713] vdi read 0x00000004:0x00008666
[   32.795827] vdi read 0x00000004:0x00001360
[   32.799959] vdi read 0x00000004:0x00001352
[   32.804075] vdi read 0x00000004:0x00008682
[   32.808213] vdi read 0x00000004:0x00007648
[   32.812329] vdi read 0x00000004:0x00001364
[   32.816443] vdi read 0x00000004:0x00001354
[   32.820585] vdi read 0x00000004:0x00007f12
[   32.824702] vdi read 0x00000004:0x00001360
[   32.828842] vdi read 0x00000004:0x0000764c
[   32.832959] vdi read 0x00000004:0x0000135e
[   32.837092] vdi read 0x00000004:0x0000801c
[   32.841209] vdi read 0x00000004:0x0000135c
[   32.845324] vdi read 0x00000004:0x0000135e
[   32.849462] vdi read 0x00000004:0x00001366
[   32.853579] vdi read 0x00000004:0x0000135a
[   32.857713] vdi read 0x00000004:0x00001356
[   32.861829] vdi read 0x00000004:0x00007644
[   32.865943] vdi read 0x00000004:0x0000135a
[   32.870080] vdi read 0x00000004:0x0000135c
[   32.874197] vdi read 0x00000004:0x00001362
[   32.878339] vdi read 0x00000004:0x00001358
[   32.882456] vdi read 0x00000004:0x00003980
[   32.886594] vdi read 0x00000004:0x0001d2a6
[   32.890710] vdi read 0x00000004:0x00001356
[   32.894825] vdi read 0x00000004:0x00001364
[   32.898958] vdi read 0x00000004:0x00007648
[   32.903074] vdi read 0x00000004:0x00001366
[   32.907212] vdi read 0x00000004:0x00001360
[   32.911328] vdi read 0x00000004:0x0001d2be
[   32.915443] vdi read 0x00000004:0x00003a54
[   32.919575] vdi read 0x00000004:0x00001360
[   32.923692] vdi read 0x00000004:0x00007f3a
[   32.927830] vdi read 0x00000004:0x00003a3e
[   32.931947] vdi read 0x00000004:0x00001358
[   32.936061] vdi read 0x00000004:0x00001364
[   32.940203] vdi read 0x00000004:0x00003a42
[   32.944320] vdi read 0x00000004:0x00001352
[   32.948458] vdi read 0x00000004:0x0000135a
[   32.952574] vdi read 0x00000004:0x00003aa2
[   32.956707] vdi read 0x00000004:0x0000135e
[   32.960823] vdi read 0x00000004:0x00003a3e
[   32.964937] vdi read 0x00000004:0x00007654
[   32.969075] vdi read 0x00000004:0x00003a42
[   32.973191] vdi read 0x00000004:0x00001354
[   32.977324] vdi read 0x00000004:0x00003a9c
[   32.981441] vdi read 0x00000004:0x00001356
[   32.985555] vdi read 0x00000004:0x00001364
[   32.989692] vdi read 0x00000004:0x00001360
[   32.993808] vdi read 0x00000004:0x00008686
[   32.997954] vdi read 0x00000004:0x00007652
[   33.002071] vdi read 0x00000004:0x0000135a
[   33.006186] vdi read 0x00000004:0x00001356
[   33.010324] vdi read 0x00000004:0x0000135a
[   33.014440] vdi read 0x00000004:0x00003a6a
[   33.018574] vdi read 0x00000004:0x0000135e
[   33.022692] vdi read 0x00000004:0x00001364
[   33.026829] vdi read 0x00000004:0x0000135a
[   33.030945] vdi read 0x00000004:0x0000135c
[   33.035060] vdi read 0x00000004:0x00003a46
[   33.039193] vdi read 0x00000004:0x00001362
[   33.043309] vdi read 0x00000004:0x0000135c
[   33.047447] vdi read 0x00000004:0x00001360
[   33.051563] vdi read 0x00000004:0x00003a6a
[   33.055677] vdi read 0x00000004:0x00001364
[   33.059819] vdi read 0x00000004:0x00007f3c
[   33.063936] vdi read 0x00000004:0x0000135a
[   33.068075] vdi read 0x00000004:0x00001362
[   33.072192] vdi read 0x00000004:0x00003aa2
[   33.076306] vdi read 0x00000004:0x00001356
[   33.080444] vdi read 0x00000004:0x00001360
[   33.084561] vdi read 0x00000004:0x00003990
[   33.088699] vdi read 0x00000004:0x000036b0
[   33.092816] vdi read 0x00000004:0x00001356
[   33.096948] vdi read 0x00000004:0x00001354
[   33.101064] vdi read 0x00000004:0x00007644
[   33.105179] vdi read 0x00000004:0x00001362
[   33.109316] vdi read 0x00000004:0x00001366
[   33.113433] vdi read 0x00000004:0x00001352
[   33.117575] vdi read 0x00000004:0x0000135c
[   33.121692] vdi read 0x00000004:0x00001354
[   33.125806] vdi read 0x00000004:0x0000764c
[   33.129945] vdi read 0x00000004:0x00003a38
[   33.134061] vdi read 0x00000004:0x0000135c
[   33.138194] vdi read 0x00000004:0x00003a42
[   33.142310] vdi read 0x00000004:0x0000135c
[   33.146425] vdi read 0x00000004:0x0000135a
[   33.150562] vdi read 0x00000004:0x00001356
[   33.154679] vdi read 0x00000004:0x00003a46
[   33.158812] vdi read 0x00000004:0x00001366
[   33.162928] vdi read 0x00000004:0x00007f42
[   33.167065] vdi read 0x00000004:0x000036a6
[   33.171182] vdi read 0x00000004:0x00001352
[   33.175296] vdi read 0x00000004:0x00001356
[   33.179437] vdi read 0x00000004:0x00003a46
[   33.183554] vdi read 0x00000004:0x0000135c
[   33.187693] vdi read 0x00000004:0x00001358
[   33.191809] vdi read 0x00000004:0x00003a46
[   33.195923] vdi read 0x00000004:0x00007644
[   33.200055] vdi read 0x00000004:0x0000135a
[   33.204171] vdi read 0x00000004:0x000089d8
[   33.208309] vdi read 0x00000004:0x000036a6
[   33.212425] vdi read 0x00000004:0x00001354
[   33.216557] vdi read 0x00000004:0x00001366
[   33.220674] vdi read 0x00000004:0x00007644
[   33.224788] vdi read 0x00000004:0x0000135a
[   33.228926] vdi read 0x00000004:0x0000135e
[   33.233043] vdi read 0x00000004:0x00007f12
[   33.237185] vdi read 0x00000004:0x0000135e
[   33.241302] vdi read 0x00000004:0x0001d346
[   33.245417] vdi read 0x00000004:0x00003a3e
[   33.249556] vdi read 0x00000004:0x00001362
[   33.253673] vdi read 0x00000004:0x00001366
[   33.257806] vdi read 0x00000004:0x00001364
[   33.261922] vdi read 0x00000004:0x00001360
[   33.266037] vdi read 0x00000004:0x0000808c
[   33.270175] vdi read 0x00000004:0x00003a46
[   33.274292] vdi read 0x00000004:0x00001366
[   33.278426] vdi read 0x00000004:0x00003a3e
[   33.282542] vdi read 0x00000004:0x00001360
[   33.286680] vdi read 0x00000004:0x0000135a
[   33.290796] vdi read 0x00000004:0x00007f12
[   33.294911] vdi read 0x00000004:0x00007648
[   33.299052] vdi read 0x00000004:0x00001362
[   33.303169] vdi read 0x00000004:0x00003a50
[   33.307307] vdi read 0x00000004:0x00007648
[   33.311424] vdi read 0x00000004:0x00001352
[   33.315538] vdi read 0x00000004:0x00001356
[   33.319671] vdi read 0x00000004:0x00008682
[   33.323788] vdi read 0x00000004:0x0000135e
[   33.327925] vdi read 0x00000004:0x00001354
[   33.332042] vdi read 0x00000004:0x00007654
[   33.336156] vdi read 0x00000004:0x0000135a
[   33.340289] vdi read 0x00000004:0x00001356
[   33.344406] vdi read 0x00000004:0x00001360
[   33.348543] vdi read 0x00000004:0x00003a74
[   33.352660] vdi read 0x00000004:0x00001358
[   33.356802] vdi read 0x00000004:0x00003a6e
[   33.360919] vdi read 0x00000004:0x00001358
[   33.365033] vdi read 0x00000004:0x00001366
[   33.369171] vdi read 0x00000004:0x00007f28
[   33.373287] vdi read 0x00000004:0x00001354
[   33.377420] vdi read 0x00000004:0x0000135e
[   33.381537] vdi read 0x00000004:0x00003a6a
[   33.385651] vdi read 0x00000004:0x00001360
[   33.389787] vdi read 0x00000004:0x0000135a
[   33.393904] vdi read 0x00000004:0x00001362
[   33.398036] vdi read 0x00000004:0x00008678
[   33.402153] vdi read 0x00000004:0x0000135e
[   33.406266] vdi read 0x00000004:0x0000135e
[   33.410404] vdi read 0x00000004:0x00001366
[   33.414520] vdi read 0x00000004:0x00003a3e
[   33.418661] vdi read 0x00000004:0x0000135e
[   33.422778] vdi read 0x00000004:0x0001d2c6
[   33.426917] vdi read 0x00000004:0x00008662
[   33.431034] vdi read 0x00000004:0x00001364
[   33.435149] vdi read 0x00000004:0x0000399a
[   33.439282] vdi read 0x00000004:0x0000135c
[   33.443398] vdi read 0x00000004:0x00001364
[   33.447536] vdi read 0x00000004:0x00001364
[   33.451652] vdi read 0x00000004:0x00007f18
[   33.455766] vdi read 0x00000004:0x00001366
[   33.459898] vdi read 0x00000004:0x0000135e
[   33.464015] vdi read 0x00000004:0x00003a54
[   33.468152] vdi read 0x00000004:0x00003a50
[   33.472270] vdi read 0x00000004:0x00001362
[   33.476384] vdi read 0x00000004:0x000089d8
[   33.480525] vdi read 0x00000004:0x00003a6a
[   33.484642] vdi read 0x00000004:0x00001362
[   33.488780] vdi read 0x00000004:0x00003972
[   33.492897] vdi read 0x00000004:0x0000135e
[   33.497029] vdi read 0x00000004:0x00001360
[   33.501145] vdi read 0x00000004:0x00003a4c
[   33.505260] vdi read 0x00000004:0x00001352
[   33.509397] vdi read 0x00000004:0x0000135c
[   33.513515] vdi read 0x00000004:0x00003988
[   33.517647] vdi read 0x00000004:0x00003a6a
[   33.521763] vdi read 0x00000004:0x00001358
[   33.525878] vdi read 0x00000004:0x000089d8
[   33.530015] vdi read 0x00000004:0x0000135c
[   33.534132] vdi read 0x00000004:0x00001354
[   33.538273] vdi read 0x00000004:0x00001352
[   33.542390] vdi read 0x00000004:0x0001d2b4
[   33.546528] vdi read 0x00000004:0x00001356
[   33.550645] vdi read 0x00000004:0x0000135e
[   33.554759] vdi read 0x00000004:0x0001d346
[   33.558892] vdi read 0x00000004:0x00001364
[   33.563008] vdi read 0x00000004:0x0000135c
[   33.567146] vdi read 0x00000004:0x00001366
[   33.571262] vdi read 0x00000004:0x0000801a
[   33.575376] vdi read 0x00000004:0x0000135a
[   33.579509] vdi read 0x00000004:0x00001358
[   33.583625] vdi read 0x00000004:0x00007f10
[   33.587764] vdi read 0x00000004:0x00001364
[   33.591881] vdi read 0x00000004:0x0000135e
[   33.595995] vdi read 0x00000004:0x00003a40
[   33.600136] vdi read 0x00000004:0x00001356
[   33.604253] vdi read 0x00000004:0x00007648
[   33.608391] vdi read 0x00000004:0x00008686
[   33.612508] vdi read 0x00000004:0x00001356
[   33.616643] vdi read 0x00000004:0x0001d346
[   33.620760] vdi read 0x00000004:0x00001356
[   33.624875] vdi read 0x00000004:0x0000801a
[   33.629013] vdi read 0x00000004:0x00003a46
[   33.633129] vdi read 0x00000004:0x00001364
[   33.637262] vdi read 0x00000004:0x0000135a
[   33.641378] vdi read 0x00000004:0x00001356
[   33.645494] vdi read 0x00000004:0x00001366
[   33.649631] vdi read 0x00000004:0x00001360
[   33.653748] vdi read 0x00000004:0x00003a54
[   33.657889] vdi read 0x00000004:0x0000135e
[   33.662006] vdi read 0x00000004:0x00007644
[   33.666121] vdi read 0x00000004:0x00001350
[   33.670259] vdi read 0x00000004:0x0000135a
[   33.674376] vdi read 0x00000004:0x0000135c
[   33.678509] vdi read 0x00000004:0x0001d33e
[   33.682625] vdi read 0x00000004:0x00001360
[   33.686763] vdi read 0x00000004:0x00001354
[   33.690879] vdi read 0x00000004:0x00007648
[   33.694993] vdi read 0x00000004:0x00001360
[   33.699126] vdi read 0x00000004:0x0000135a
[   33.703242] vdi read 0x00000004:0x00007648
[   33.707380] vdi read 0x00000004:0x00003a50
[   33.711497] vdi read 0x00000004:0x00001364
[   33.715611] vdi read 0x00000004:0x00001362
[   33.719752] vdi read 0x00000004:0x0001d2a6
[   33.723870] vdi read 0x00000004:0x0000135e
[   33.728008] vdi read 0x00000004:0x000089d0
[   33.732125] vdi read 0x00000004:0x00001364
[   33.736239] vdi read 0x00000004:0x0000135c
[   33.740371] vdi read 0x00000004:0x00003972
[   33.744487] vdi read 0x00000004:0x00001354
[   33.748625] vdi read 0x00000004:0x00003a6a
[   33.752741] vdi read 0x00000004:0x00001356
[   33.756874] vdi read 0x00000004:0x00008662
[   33.760990] vdi read 0x00000004:0x00001362
[   33.765105] vdi read 0x00000004:0x0000135a
[   33.769242] vdi read 0x00000004:0x00001354
[   33.773358] vdi read 0x00000004:0x00007644
[   33.777500] vdi read 0x00000004:0x0000135c
[   33.781617] vdi read 0x00000004:0x00007648
[   33.785731] vdi read 0x00000004:0x0000135a
[   33.789869] vdi read 0x00000004:0x0000135e
[   33.793985] vdi read 0x00000004:0x0000135c
[   33.798117] vdi read 0x00000004:0x00007644
[   33.802235] vdi read 0x00000004:0x0000135e
[   33.806349] vdi read 0x00000004:0x00001366
[   33.810486] vdi read 0x00000004:0x00001358
[   33.814603] vdi read 0x00000004:0x00007f3a
[   33.818735] vdi read 0x00000004:0x00001362
[   33.822851] vdi read 0x00000004:0x00003a4e
[   33.826989] vdi read 0x00000004:0x00003a46
[   33.831105] vdi read 0x00000004:0x00001362
[   33.835219] vdi read 0x00000004:0x00001360
[   33.839361] vdi read 0x00000004:0x00003a38
[   33.843478] vdi read 0x00000004:0x00001352
[   33.847616] vdi read 0x00000004:0x00001358
[   33.851733] vdi read 0x00000004:0x00003a3e
[   33.855847] vdi read 0x00000004:0x0000135e
[   33.859980] vdi read 0x00000004:0x00001352
[   33.864096] vdi read 0x00000004:0x00003aa2
[   33.868233] vdi read 0x00000004:0x00007644
[   33.872350] vdi read 0x00000004:0x00001364
[   33.876465] vdi read 0x00000004:0x00001364
[   33.880601] vdi read 0x00000004:0x00001356
[   33.884716] vdi read 0x00000004:0x000089d8
[   33.888853] vdi read 0x00000004:0x000036d4
[   33.892970] vdi read 0x00000004:0x00001354
[   33.897111] vdi read 0x00000004:0x0000135c
[   33.901228] vdi read 0x00000004:0x0000135c
[   33.905343] vdi read 0x00000004:0x00001364
[   33.909480] vdi read 0x00000004:0x00001358
[   33.913597] vdi read 0x00000004:0x0000801c
[   33.917730] vdi read 0x00000004:0x00001352
[   33.921846] vdi read 0x00000004:0x0000135c
[   33.925960] vdi read 0x00000004:0x00003a48
[   33.930098] vdi read 0x00000004:0x00003aa2
[   33.934215] vdi read 0x00000004:0x0000135e
[   33.938347] vdi read 0x00000004:0x000089d0
[   33.942463] vdi read 0x00000004:0x00001360
[   33.946601] vdi read 0x00000004:0x00001352
[   33.950718] vdi read 0x00000004:0x0000135a
[   33.954832] vdi read 0x00000004:0x00007f34
[   33.958973] vdi read 0x00000004:0x0000135a
[   33.963090] vdi read 0x00000004:0x00003974
[   33.967229] vdi read 0x00000004:0x00003a4c
[   33.971346] vdi read 0x00000004:0x00001352
[   33.975460] vdi read 0x00000004:0x00001354
[   33.979592] vdi read 0x00000004:0x00007648
[   33.983709] vdi read 0x00000004:0x00001364
[   33.987847] vdi read 0x00000004:0x00001366
[   33.991964] vdi read 0x00000004:0x00003a46
[   33.996078] vdi read 0x00000004:0x00007f18
[   34.000210] vdi read 0x00000004:0x00001358
[   34.004327] vdi read 0x00000004:0x00003a3e
[   34.008465] vdi read 0x00000004:0x00003a40
[   34.012582] vdi read 0x00000004:0x00001356
[   34.016723] vdi read 0x00000004:0x00003a48
[   34.020840] vdi read 0x00000004:0x0000135e
[   34.024954] vdi read 0x00000004:0x00001360
[   34.029093] vdi read 0x00000004:0x00001352
[   34.033209] vdi read 0x00000004:0x00001364
[   34.037342] vdi read 0x00000004:0x0000135e
[   34.041458] vdi read 0x00000004:0x00003a54
[   34.045573] vdi read 0x00000004:0x00001352
[   34.049710] vdi read 0x00000004:0x00001354
[   34.053827] vdi read 0x00000004:0x00001356
[   34.057959] vdi read 0x00000004:0x00003a46
[   34.062076] vdi read 0x00000004:0x0000135e
[   34.066190] vdi read 0x00000004:0x00001358
[   34.070327] vdi read 0x00000004:0x0000135a
[   34.074444] vdi read 0x00000004:0x00003a46
[   34.078585] vdi read 0x00000004:0x00001362
[   34.082702] vdi read 0x00000004:0x00003a4a
[   34.086841] vdi read 0x00000004:0x00001360
[   34.090958] vdi read 0x00000004:0x00001354
[   34.095072] vdi read 0x00000004:0x00003a3e
[   34.099205] vdi read 0x00000004:0x00001366
[   34.103322] vdi read 0x00000004:0x00007f34
[   34.107460] vdi read 0x00000004:0x000036fe
[   34.111577] vdi read 0x00000004:0x0000135e
[   34.115691] vdi read 0x00000004:0x0000135e
```
Vendor firmware with video playing:

```
/ # devmem 0x1f344804
0x0001D096
/ # devmem 0x1f344804
0x00003A2E
/ # devmem 0x1f344804
0x00001358
/ # devmem 0x1f344804
0x00001362
/ # devmem 0x1f344804
0x00008618
/ # devmem 0x1f344804
0x00001364
/ # devmem 0x1f344804
0x00001356
/ # devmem 0x1f344804
0x00001360
/ # devmem 0x1f344804
0x00001354
/ # devmem 0x1f344804
0x00007EC6
/ # devmem 0x1f344804
0x0000135C
/ # devmem 0x1f344804
0x00001354
/ # devmem 0x1f344804
0x00001366
/ # devmem 0x1f344804
0x00001362
/ # devmem 0x1f344804
0x0000135C
/ # devmem 0x1f344804
0x00007EC6
/ # devmem 0x1f344804
0x00001362
/ # devmem 0x1f344804
0x00007608
/ # devmem 0x1f344804
0x00001366
/ # devmem 0x1f344804
0x00001356
/ # devmem 0x1f344804
0x0000135A
/ # devmem 0x1f344804
0x000075FE
/ # devmem 0x1f344804
0x00001362
/ # devmem 0x1f344804
0x00003A2E
/ # devmem 0x1f344804
0x00001366
/ # devmem 0x1f344804
0x00001354
/ # devmem 0x1f344804
0x00003970
/ # devmem 0x1f344804
0x00001356
/ # devmem 0x1f344804
0x00003A2E
/ # devmem 0x1f344804
0x0000135E
/ # devmem 0x1f344804
0x00001364
/ # devmem 0x1f344804
0x000075FE
/ # devmem 0x1f344804
0x00001360
/ # devmem 0x1f344804
0x00001360
/ # devmem 0x1f344804
0x0000135C
/ # devmem 0x1f344804
0x0000863E
/ # devmem 0x1f344804
0x00007FD0
/ # devmem 0x1f344804
0x0000135E
/ # devmem 0x1f344804
0x0000135E
/ # devmem 0x1f344804
0x000075FA
/ # devmem 0x1f344804
0x00001366
/ # devmem 0x1f344804
0x00001356
/ # devmem 0x1f344804
0x00003A32
/ # 
/ # devmem 0x1f344804
0x0000135A
/ # devmem 0x1f344804
0x0000135E
/ # devmem 0x1f344804
0x00001360
/ # devmem 0x1f344804
0x00001358
/ # devmem 0x1f344804
0x0000135A
/ # devmem 0x1f344804
0x00003A36
/ # devmem 0x1f344804
0x00001352
/ # devmem 0x1f344804
0x0000861C
/ # devmem 0x1f344804
0x000075FE
/ # devmem 0x1f344804
0x00003A92
/ # devmem 0x1f344804
0x000075FA
/ # devmem 0x1f344804
0x000075FA
/ # devmem 0x1f344804
0x00001352
/ # devmem 0x1f344804
0x00001356
/ # 
```

sdk firmware

```
[   17.233723] vdi read 0x000000f4:0x00000000
[   17.237859] vdi write 0x000000f0:0x00000001
[   17.242060] vdi read 0x00000004:0x00001366
[   17.246186] vdi read 0x000000f0:0x00000001
[   17.250299] vdi read 0x000000f4:0x00000000
[   17.254410] vdi write 0x000000f0:0x00000001
[   17.258627] vdi read 0x00000004:0x00001362
[   17.262740] vdi read 0x000000f0:0x00000001
[   17.266865] vdi read 0x000000f4:0x00000000
[   17.270978] vdi write 0x000000f0:0x00000001
[   17.275176] vdi read 0x00000004:0x0000135c
[   17.279305] vdi read 0x000000f0:0x00000001
[   17.283418] vdi read 0x000000f4:0x00000000
[   17.287548] vdi write 0x000000f0:0x00000001
[   17.291748] vdi read 0x00000004:0x0000764c
[   17.295859] vdi read 0x000000f0:0x00000001
[   17.299995] vdi read 0x000000f4:0x00000000
[   17.304109] vdi write 0x000000f0:0x00000001
[   17.308322] vdi read 0x00000004:0x00008662
[   17.312435] vdi read 0x000000f0:0x00000001
[   17.316564] vdi read 0x000000f4:0x00000000
[   17.320677] vdi write 0x000000f0:0x00000001
[   17.324875] vdi read 0x00000004:0x00001352
[   17.329000] vdi read 0x000000f0:0x00000001
[   17.333113] vdi read 0x000000f4:0x00000000
[   17.337242] vdi write 0x000000f0:0x00000001
[   17.341441] vdi read 0x00000004:0x00001360
[   17.345552] vdi read 0x000000f0:0x00000001
[   17.349677] vdi read 0x000000f4:0x00000000
[   17.353789] vdi read 0x00000108:0x00000000
[   17.357921] vdi read 0x0000010c:0x00040000
[   17.362034] here 446
[   17.364235] vdec 1f344800.video-codec: : failure: 0x40000
[   17.369757] vdi write 0x00000104:0x00000000
[   17.373957] vdi write 0x00000070:0x00000001
[   17.378174] vdi write 0x00000100:0x00004000
[   17.382374] vdi write 0x00000038:0x00000001
[   17.386588] vdi read 0x00000070:0x00000001
[   17.390700] vdi read 0x00000070:0x00000000
[   17.394812] vdi read 0x00000108:0x00000001
[   17.398951] vdi read 0x0000011c:0x57415645
[   17.403064] vdi read 0x00000120:0x00005110
[   17.407190] vdi read 0x00000118:0x0b60ba3d
[   17.411303] vdi read 0x00000140:0x00000000
[   17.415414] vdi read 0x00000124:0x80cf0980
[   17.419551] vdi read 0x00000128:0x08018001
[   17.423664] vdi read 0x0000012c:0x00000103
[   17.427790] vdi read 0x00000134:0x00027a8a
[   17.431903] here 44: 0
[   17.434273] here 46
[   17.436407] vdi read 0x00000004:0x00001352
[   17.440520] vdi write 0x00000104:0x00000000
[   17.444719] vdi write 0x00000070:0x00000001
[   17.448932] vdi write 0x00000100:0x00004000
[   17.453132] vdi write 0x00000038:0x00000001
[   17.457350] vdi read 0x00000070:0x00000001
[   17.461463] vdi read 0x00000070:0x00000000
[   17.465574] vdi read 0x00000108:0x00000001
[   17.469699] vdi read 0x00000118:0x0b60ba3d
[   17.473815] vdec 1f344800.video-codec: enum product_id : 00000001
[   17.479963] vdec 1f344800.video-codec: fw_version : 00000000(r190888509)
[   17.487545] mstar_pm51: probe of 1f002000.mcu failed with error -2
```

cnm linux firmware firmware
https://gitlab.collabora.com/chipsnmedia/linux-firmware/-/tree/cnm/cnm

```
[   17.339745] vdi read 0x000000f0:0x00000001
[   17.343857] vdi read 0x000000f4:0x00000000
[   17.347981] vdi read 0x00000108:0x00000001
[   17.352094] vdi write 0x00000104:0x00000000
[   17.356312] vdi write 0x00000070:0x00000001
[   17.360512] vdi write 0x00000100:0x00004000
[   17.364710] vdi write 0x00000038:0x00000001
[   17.368922] vdi read 0x00000070:0x00000001
[   17.373035] vdi read 0x00000070:0x00000000
[   17.377159] vdi read 0x00000108:0x00000001
[   17.381271] vdi read 0x0000011c:0x57415645
[   17.385383] vdi read 0x00000120:0x00005110
[   17.389507] vdi read 0x00000118:0x00038582
[   17.393619] vdi read 0x00000140:0x00000000
[   17.397749] vdi read 0x00000124:0x80cf0980
[   17.401862] vdi read 0x00000128:0x08018001
[   17.405974] vdi read 0x0000012c:0x00000103
[   17.410103] vdi read 0x00000134:0x00027a8a
[   17.414216] here 44: 0
[   17.416605] here 46
[   17.418723] vdi read 0x00000004:0x00009a9c
[   17.422834] vdi write 0x00000104:0x00000000
[   17.427046] vdi write 0x00000070:0x00000001
[   17.431247] vdi write 0x00000100:0x00004000
[   17.435445] vdi write 0x00000038:0x00000001
[   17.439656] vdi read 0x00000070:0x00000001
[   17.443769] vdi read 0x00000070:0x00000000
[   17.447894] vdi read 0x00000108:0x00000001
[   17.452006] vdi read 0x00000118:0x00038582
[   17.456123] vdec 1f344800.video-codec: enum product_id : 00000001
[   17.462254] vdec 1f344800.video-codec: fw_version : 00000000(r230786)
[   17.469552] mstar_pm51: probe of 1f002000.mcu failed with error -2
```

Firmware from the working board:

```
[   16.171359] read  <-- 0x00000118:0x04625134
[   16.175554] read  <-- 0x00000118:0x04625134
[   16.179758] vdec 1f344800.video-codec: fw version: 0x04625134
[   16.185526] read  <-- 0x00000124:0x80cf0980
[   16.189734] vdec 1f344800.video-codec: fw config0: 0x80cf0980
[   16.195497] read  <-- 0x00000128:0x08018001
[   16.199701] vdec 1f344800.video-codec: fw config1: 0x08018001
[   16.205466] read  <-- 0x0000012c:0x00000103
[   16.209669] vdec 1f344800.video-codec: fw conf feature: 0x00000103
[   16.215871] read  <-- 0x00000130:0x0133f0de
[   16.220077] vdec 1f344800.video-codec: fw conf date: 0x0133f0de
[   16.226014] read  <-- 0x00000134:0x00027a8a
[   16.230216] vdec 1f344800.video-codec: fw conf revision: 0x00027a8a
[   16.236506] read  <-- 0x00000138:0x00000102
[   16.240708] vdec 1f344800.video-codec: fw conf type: 0x00000102
[   16.246646] read  <-- 0x0000013c:0x00000000
[   16.250849] vdec 1f344800.video-codec: fw product id: 0x00000000
[   16.256873] read  <-- 0x00000140:0x00000000
[   16.261079] vdec 1f344800.video-codec: fw customer id: 0x00000000
[   16.267201] vdec 1f344800.video-codec: enum product_id : 00000001
[   16.273313] vdec 1f344800.video-codec: fw_version : 00000000(r73552180)
[   16.280407] mstar_pm51: probe of 1f002000.mcu failed with error -2
```

Values are all the same as the binary module.
