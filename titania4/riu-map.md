# Titania4 RIU map

**Note: it's an assumption right now**

## PM
| riu addr |  phy addr  |             name              |
|----------|------------|-------------------------------|
| 0x000100 | 0x1f000200 | PM_RIU_DBG                    |
| 0x000200 | 0x1f000400 | MENULOAD                      |
| 0x000400 | 0x1f000800 | DDC                           |
| 0x000800 | 0x1f001000 | ISP                           |
| 0x0008E0 | 0x1f0011c0 | QSPI                          |
| 0x000E00 | 0x1f001c00 | PM_SLEEP                      |
| 0x001000 | 0x1f002000 | MCU                           |
| 0x001200 | 0x1f002400 | PM_RTC                        |
| 0x001300 | 0x1f002600 | PM_RTC2                       |
| 0x001400 | 0x1f002800 | PM_SAR                        |
| 0x001500 | 0x1f002a00 | PM_AV_LNK                     |
| 0x001E00 | 0x1f003c00 | PM_TOP                        |
| 0x002000 | 0x1f004000 | EFUSE                         |
| 0x002B00 | 0x1f005600 | IRQ                           |
| 0x002B80 | 0x1f005700 | CACHE                         |
| 0x002BC0 | 0x1f005780 | XDMIU                         |
| 0x003000 | 0x1f006000 | WDT                           |
| 0x003020 | 0x1f006040 | TIMER0                        |
| 0x003040 | 0x1f006080 | TIMER1                        |
| 0x003C00 | 0x1f007800 | REG_PIU_MISC_0                |
| 0x003D00 | 0x1f007a00 | IR (rc5/etc)                  |
| 0x003D80 | 0x1f007b00 | IR (nec/etc)                  |

## Non-PM
| riu addr |  phy addr  |             name              |
|----------|------------|-------------------------------|
| 0x100100 | 0x1f200200 | RIU_DBG                       |
| 0x100300 | 0x1f200600 | VD_MHEG5                      |
| 0x100500 | 0x1f200a00 | POR_STATUS                    |
| 0x100540 | 0x1f200a80 | INTR_CPUINT                   |
| 0x100580 | 0x1f200b00 | NORPF                         |
| 0x100600 | 0x1f200c00 | MIU2                          |
| 0x100700 | 0x1f200e00 | USB0                          |
| 0x100780 | 0x1f200f00 | USB1                          |
| 0x100900 | 0x1f201200 | BDMA                          |
| 0x100980 | 0x1f201300 | UART0                         |
| 0x100A00 | 0x1f201400 | RVD                           |
| 0x100B00 | 0x1f201600 | CLKGEN0                       |
| 0x100C00 | 0x1f201800 | DSCRMB                        |
| 0x100D00 | 0x1f201a00 | UHC1                          |
| 0x100F00 | 0x1f201e00 | MHEG5                         |
| 0x101100 | 0x1f202200 | MVD                           |
| 0x101200 | 0x1f202400 | MIU                           |
| 0x101300 | 0x1f202600 | VD_MCU                        |
| 0x101400 | 0x1f202800 | MVOP                          |
| 0x101500 | 0x1f202a00 | TSP0                          |
| 0x101600 | 0x1f202c00 | TSP1                          |
| 0x101700 | 0x1f202e00 | JPD                           |
| 0x101800 | 0x1f203000 | SEMAPH                        |
| 0x101840 | 0x1f203080 | MAU0                          |
| 0x101860 | 0x1f2030c0 | MAU1                          |
| 0x101880 | 0x1f203100 | MIPS_WDT                      |
| 0x1018C0 | 0x1f203180 | ECBRIDGE                      |
| 0x101900 | 0x1f203200 | INTR_CTRL                     |
| 0x101B00 | 0x1f203600 | HVD                           |
| 0x101E00 | 0x1f203c00 | CHIP                          |
| 0x101F00 | 0x1f203e00 | GOP                           |
| 0x102400 | 0x1f204800 | UHC                           |
| 0x102500 | 0x1f204a00 | ADC_ATOP                      |
| 0x102600 | 0x1f204c00 | ADC_DTOP                      |
| 0x102700 | 0x1f204e00 | HDMI                          |
| 0x102800 | 0x1f205000 | GE0                           |
| 0x102900 | 0x1f205200 | STRLD                         |
| 0x102E00 | 0x1f205c00 | SC0 (IP_MUX)                  |
| 0x102F00 | 0x1f205e00 | SC1 (XC)                      |
| 0x103000 | 0x1f206000 | SC2 (HDGEN)                   |
| 0x103100 | 0x1f206200 | SC3 (LPLL)                    |
| 0x103200 | 0x1f206400 | SC4 (MOD)                     |
| 0x103300 | 0x1f206600 | CLKGEN1                       |
| 0x103380 | 0x1f206700 | MAILBOX                       |
| 0x103440 | 0x1f206880 | PCM                           |
| 0x103460 | 0x1f2068c0 | VDMCU51_IF                    |
| 0x1034A0 | 0x1f206940 | PM                            |
| 0x1034C0 | 0x1f206980 | URDMA                         |
| 0x103500 | 0x1f206a00 | AFEC                          |
| 0x103600 | 0x1f206c00 | COMB                          |
| 0x103700 | 0x1f206e00 | VBI                           |
| 0x103800 | 0x1f207000 | SCM                           |
| 0x103A00 | 0x1f207400 | UTMI1                         |
| 0x103A80 | 0x1f207500 | UTMI                          |
| 0x103B00 | 0x1f207600 | VE0                           |
| 0x103C00 | 0x1f207800 | REG_PIU_NONPM                 |
| 0x103E00 | 0x1f207c00 | VE1                           |
| 0x103F00 | 0x1f207e00 | VE2                           |
| 0x110600 | 0x1f220c00 | UART1                         |
| 0x110640 | 0x1f220c80 | UART2                         |
| 0x110680 | 0x1f220d00 | FUART                         |
| 0x110700 | 0x1f220e00 | GE1                           |
| 0x110C00 | 0x1f221800 | ANA_MISC                      |
| 0x110D00 | 0x1f221a00 | MIU_ATOP                      |
| 0x110D80 | 0x1f221b00 | MIU1_ATOP                     |
| 0x112A00 | 0x1f225400 | VIVALDI0                      |
| 0x112B00 | 0x1f225600 | VIVALDI1                      |
| 0x112C00 | 0x1f225800 | VIVALDI2                      |
| 0x112D00 | 0x1f225a00 | VIVALDI3                      |
| 0x112E00 | 0x1f225c00 | VIVALDI4                      |
| 0x112F00 | 0x1f225e00 | VIVALDI5                      |
