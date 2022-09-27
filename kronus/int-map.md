# Kronus Interrupt map

## PM intc

### part1

| line |        name        |    notes                                  |
|------|--------------------|-------------------------------------------|
| 0    | TIMER0             |                                           |
| 1    | TIMER1             |                                           |
| 2    |                    |                                           |
| 3    |                    |                                           |
| 4    |                    |                                           |
| 5    |                    |                                           |
| 6    |                    |                                           |
| 7    |                    |                                           |
| 8    |                    |                                           |
| 9    |                    |                                           |
| 10   |                    |                                           |
| 11   |                    |                                           |
| 12   |                    |                                           |
| 13   |                    |                                           |
| 14   |                    |                                           |
| 15   |                    |                                           |

### part2

| line |        name        |    notes                                  |
|------|--------------------|-------------------------------------------|
| 0    | ???                |                                           |
| 1    | part1 irq          |                                           |
| 2    |                    |                                           |
| 3    |                    |                                           |
| 4    |                    |                                           |
| 5    |                    |                                           |
| 6    |                    |                                           |
| 7    |                    |                                           |
| 8    |                    |                                           |
| 9    |                    |                                           |
| 10   |                    |                                           |
| 11   |                    |                                           |
| 12   |                    |                                           |
| 13   |                    |                                           |
| 14   |                    |                                           |
| 15   |                    |                                           |


## Non-PM intc

### IRQ

| line |        name        |    notes                                  |
|------|--------------------|-------------------------------------------|
| 0    | UART0              |                                           |
| 1    | IIC1               |                                           |
| 2    |                    |                                           |
| 3    | MVD                |                                           |
| 4    | PS                 |                                           |
| 5    | NFIE               |                                           |
| 6    | USB                |                                           |
| 7    | UHC                |                                           |
| 8    | EC_BRIDGE          |                                           |
| 9    | EMAC               |                                           |
| 10   | DISP               |                                           |
| 11   | DHC                |                                           |
| 12   | OTG                |                                           |
| 13   | USB2               |                                           |
| 14   |                    |                                           |
| 15   | UHC2               |                                           |
| 16   | TSP2HK             |                                           |
| 17   | VE                 |                                           |
| 18   | CIMAX2MCU          |                                           |
| 19   | DC                 |                                           |
| 20   | GOP                |                                           |
| 21   | PCM                |                                           |
| 22   | IIC0               |                                           |
| 23   | RTC                |                                           |
| 24   | KEYPAD             | probably SAR irq                          |
| 25   | PM                 |                                           |
| 26   | DDC2BI             |                                           |
| 27   | UP_EMM_ECM         |                                           |
| 28   | UART_CA            |                                           |
| 29   | RTC1               |                                           |
| 30   |                    |                                           |
| 31   | ADCDVI2RIU         |                                           |
| 32   | HVD                |                                           |
| 33   | USB1               |                                           |
| 34   | UHC1               |                                           |
| 35   | MIU                |                                           |
| 36   |                    |                                           |
| 37   |                    |                                           |
| 38   | AEON2HI            |                                           |
| 39   | UART1              |                                           |
| 40   | UART2              |                                           |
| 41   |                    |                                           |
| 42   | MPIF               |                                           |
| 43   |                    |                                           |
| 44   |                    |                                           |
| 45   | JPD                |                                           |
| 46   | CA_MVD_CHKSUM_FAIL |                                           |
| 47   | CA_TSP_CHKSUM_FAIL |                                           |
| 48   | BDMA0              |                                           |
| 49   | BDMA1              |                                           |
| 50   | UART2MCU           | FUART interrupt                           |
| 51   | URDMA2MCU          | URDMA interrupt                           |
| 52   | DVI_HDMI_HDCP      |                                           |
| 53   | CEC                |                                           |
| 54   | HDMITX_LEVEL       |                                           |
| 55   |                    |                                           |
| 56   | HDCP               |                                           |
| 57   | DMAWADR_ERR        |                                           |
| 58   | CA_I3              |                                           |
| 59   | CA_SVP_CMD         |                                           |
| 60   | RASP1              |                                           |
| 61   | RASP0              |                                           |
| 62   |                    |                                           |
| 63   | FRM_PM             | "FRoM PM"? Comes from PM intc's part2     |

### FIQ

| line |          name          |    notes                                  |
|------|------------------------|-------------------------------------------|
| 0    | EXTIMER0               |                                           |
| 1    | EXTIMER1               |                                           |
| 2    | WDT                    |                                           |
| 3    |                        |                                           |
| 4    |                        |                                           |
| 5    |                        |                                           |
| 6    |                        |                                           |
| 7    |                        |                                           |
| 8    |                        |                                           |
| 9    | UART_CA                |                                           |
| 10   |                        |                                           |
| 11   | HDMI_NON_PCM           |                                           |
| 12   | SPDIF_IN_NON_PCM       |                                           |
| 13   | EMAC                   |                                           |
| 14   | SE_DSP2UP              |                                           |
| 15   | TSP2AEON               |                                           |
| 16   | VIVALDI_STR            |                                           |
| 17   | VIVALDI_PTS            |                                           |
| 18   | DSP_MIU_PROT           |                                           |
| 19   | XIU_TIMEOUT            |                                           |
| 20   | DMDMCU2HK_INT          |                                           |
| 21   | VSYNC_VE4VBI           | VE vsync interrupt                        |
| 22   | FIELD_VE4VBI           | VE field interrupt                        |
| 23   | VDMCU2HK               |                                           |
| 24   | VE_DONE_TT             | VE teletext done interrupt                |
| 25   | INT_CCFL               |                                           |
| 26   | INT                    |                                           |
| 27   | IR                     |                                           |
| 28   |                        |                                           |
| 29   | DEC_DSP2UP             |                                           |
| 30   | MIPS_WDT               |                                           |
| 31   | DSP2MIPS               |                                           |
| 32   | IR_INT_RC              |                                           |
| 33   | AU_DMA_BUF_INT         |                                           |
| 34   | VE_SW_WR2BUF           |                                           |
| 35   | UP_EMM_ECM             |                                           |
| 36   | 8051_TO_MIPS_VPE0      | INTR_CPUINT host0 int0                    |
| 37   | 8051_TO_MIPS_VPE1      | INTR_CPUINT host0 int1                    |
| 38   | 8051_TO_AEON           | INTR_CPUINT host0 int2                    |
| 39   |                        |                                           |
| 40   | AEON_TO_MIPS_VPE0      | INTR_CPUINT host1 int0                    |
| 41   | AEON_TO_MIPS_VPE1      | INTR_CPUINT host1 int1                    |
| 42   | AEON_TO_8051           | INTR_CPUINT host1 int2                    |
| 43   |                        |                                           |
| 44   | MIPS_VPE1_TO_MIPS_VPE0 | INTR_CPUINT host2 int0                    |
| 45   | MIPS_VPE1_TO_AEON      | INTR_CPUINT host2 int1                    |
| 46   | MIPS_VPE1_TO_8051      | INTR_CPUINT host2 int2                    |
| 47   |                        |                                           |
| 48   | MIPS_VPE0_TO_MIPS_VPE1 | INTR_CPUINT host3 int0                    |
| 49   | MIPS_VPE0_TO_AEON      | INTR_CPUINT host3 int1                    |
| 50   | MIPS_VPE0_TO_8051      | INTR_CPUINT host3 int2                    |
| 51   |                        |                                           |
| 52   |                        |                                           |
| 53   |                        |                                           |
| 54   | HDMITX_EDGE            |                                           |
| 55   |                        |                                           |
| 56   | PVR2MI0                |                                           |
| 57   | PVR2MI1                |                                           |
| 58   |                        |                                           |
| 59   |                        |                                           |
| 60   |                        |                                           |
| 61   |                        |                                           |
| 62   |                        |                                           |
| 63   | FRM_PM                 | "FRoM PM"? .... part1?                    |
