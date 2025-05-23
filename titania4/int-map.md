# Titania4 Interrupt map

## Non-PM intc

### IRQ

| line |        name        |
|------|--------------------|
| 0    | UART0              |
| 1    |                    |
| 2    |                    |
| 3    | MVD                |
| 4    | PS                 |
| 5    | NFIE               |
| 6    | USB                |
| 7    | UHC                |
| 8    | EC_BRIDGE          |
| 9    |                    |
| 10   | DISP               |
| 11   | DHC                |
| 12   |                    |
| 13   |                    |
| 14   | COMB               |
| 15   |                    |
| 16   | TSP2HK             |
| 17   | VE                 |
| 18   | CIMAX2MCU          |
| 19   | DC                 |
| 20   | GOP                |
| 21   | PCM                |
| 22   | IIC0               |
| 23   | **RTC?**           |
| 24   | **KEYPAD?**        |
| 25   | **PM?**            |
| 26   | DDC2BI             |
| 27   | SCM                |
| 28   | VBI                |
| 29   | **RTC1?**          |
| 30   | AFEC               |
| 31   | ADCDVI2RIU         |
| 32   | HVD                |
| 33   | USB1               |
| 34   | UHC1               |
| 35   | MIU                |
| 36   |                    |
| 37   |                    |
| 38   | AEON2HI            |
| 39   | UART1              |
| 40   | UART2              |
| 41   |                    |
| 42   |                    |
| 43   |                    |
| 44   |                    |
| 45   | JPD                |
| 46   |                    |
| 47   |                    |
| 48   | BDMA0              |
| 49   | BDMA1              |
| 50   | UART2MCU           |
| 51   | URDMA2MCU          |
| 52   | DVI_HDMI_HDCP      |
| 53   | G3D2MCU            |
| 54   |                    |
| 55   |                    |
| 56   | HDCP               |
| 57   | WADR_ERR_INT       |
| 58   |                    |
| 59   |                    |
| 60   |                    |
| 61   |                    |
| 62   |                    |
| 63   |                    |

### FIQ

| line |          name          |
|------|------------------------|
| 0    | EXTIMER0               |
| 1    | EXTIMER1               |
| 2    | WDT                    |
| 3    |                        |
| 4    |                        |
| 5    |                        |
| 6    |                        |
| 7    |                        |
| 8    |                        |
| 9    |                        |
| 10   |                        |
| 11   | HDMI_NON_PCM           |
| 12   | SPDIF_IN_NON_PCM       |
| 13   | EMAC                   |
| 14   | SE_DSP2UP              |
| 15   | TSP2AEON               |
| 16   | VIVALDI_STR            |
| 17   | VIVALDI_PTS            |
| 18   | DSP_MIU_PROT           |
| 19   | XIU_TIMEOUT            |
| 20   | DMDMCU2HK_INT          |
| 21   | VSYNC_VE4VBI           |
| 22   | FIELD_VE4VBI           |
| 23   | VDMCU2HK               |
| 24   | VE_DONE_TT             |
| 25   | INT_CCFL               |
| 26   | INT                    |
| 27   | IR                     |
| 28   | AFEC_VSYNC             |
| 29   | DEC_DSP2UP             |
| 30   | MIPS_WDT               |
| 31   | DSP2MIPS               |
| 32   | IR_INT_RC              |
| 33   | AU_DMA_BUF_INT         |
| 34   |                        |
| 35   |                        |
| 36   | 8051_TO_MIPS_VPE0      |
| 37   | 8051_TO_MIPS_VPE1      |
| 38   | 8051_TO_AEON           |
| 39   |                        |
| 40   | AEON_TO_MIPS_VPE0      |
| 41   | AEON_TO_MIPS_VPE1      |
| 42   | AEON_TO_8051           |
| 43   |                        |
| 44   | MIPS_VPE1_TO_MIPS_VPE0 |
| 45   | MIPS_VPE1_TO_AEON      |
| 46   | MIPS_VPE1_TO_8051      |
| 47   |                        |
| 48   | MIPS_VPE0_TO_MIPS_VPE1 |
| 49   | MIPS_VPE0_TO_AEON      |
| 50   | MIPS_VPE0_TO_8051      |
| 51   |                        |
| 52   |                        |
| 53   |                        |
| 54   |                        |
| 55   |                        |
| 56   |                        |
| 57   |                        |
| 58   |                        |
| 59   |                        |
| 60   |                        |
| 61   |                        |
| 62   |                        |
| 63   |                        |
