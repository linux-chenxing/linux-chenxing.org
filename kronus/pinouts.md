# Kronus pinouts

## MSD7816

- Package: eLQFP128
- Exposed pad is GND
- Superscript is the function's mux value

|  #  |         name          |              alt functions              |
|-----|-----------------------|-----------------------------------------|
|   1 | IDAC_OUT_X            |                                         |
|   2 | IDAC_OUT_B            |                                         |
|   3 | IDAC_OUT_G            |                                         |
|   4 | IDAC_OUT_R            |                                         |
|   5 | AVDD33_DAC            |                                         |
|   6 | VDDC                  |                                         |
|   7 | VDDIO_CMD1            |                                         |
|   8 | D3_ODT/D2_CKE         |                                         |
|   9 | D3_RASZ/D2_WEZ        |                                         |
|  10 | VDDIO_DATA            |                                         |
|  11 | D3_DQ4/D2_DQ4         |                                         |
|  12 | D3_DQ6/D2_DQ3         |                                         |
|  13 | D3_DQ2/D2_DQ1         |                                         |
|  14 | D3_DQ0/D2_DQ6         |                                         |
|  15 | D3_DQM1/D2_DQ11       |                                         |
|  16 | VDDIO_DATA            |                                         |
|  17 | D3_DQ13/D2_DQ12       |                                         |
|  18 | D3_DQ11/D2_DQ9        |                                         |
|  19 | D3_DQ15/D2_DQ14       |                                         |
|  20 | D3_DQ9/D2_DQM1        |                                         |
|  21 | DVDD_DDR              |                                         |
|  22 | D3_DQS0/D2_DQS0       |                                         |
|  23 | D3_DQSB0/D2_DWSB0     |                                         |
|  24 | D3_DQS1/D2_DQS1       |                                         |
|  25 | D3_DQSB1/D2_DQSB1     |                                         |
|  26 | AVDD_PLL              |                                         |
|  27 | D3_DQ12/D2_DQM0       |                                         |
|  28 | D3_DQ8/D2_DQ15        |                                         |
|  29 | D3_DQ14/D2_DQ8        |                                         |
|  30 | D3_DQ10/D2_DQ10       |                                         |
|  31 | D3_DQM0/D2_DQ13       |                                         |
|  32 | VDDIO_DATA            |                                         |
|  33 | D3_DQ3/D2_DQ7         |                                         |
|  34 | D3_DQ1/D2_DQ0         |                                         |
|  35 | D3_DQ5/D2_DQ2         |                                         |
|  36 | D3_DQ7/D2_DQ5         |                                         |
|  37 | VDDIO_DATA            |                                         |
|  38 | D3_MCLK/D2_MCLK       |                                         |
|  39 | D3_MCLKZ/D2_MCLKZ     |                                         |
|  40 | VDDIO_MCLK            |                                         |
|  41 | D3_CKE/D2_ODT         |                                         |
|  42 | D3_A10/D2_RASZ        |                                         |
|  43 | D3_BA1/D2_CASZ        |                                         |
|  44 | D3_A12/D2_A0          |                                         |
|  45 | D3_A4/D2_A2           |                                         |
|  46 | VDDIO_CMD0            |                                         |
|  47 | D3_A6/D2_A4           |                                         |
|  48 | D3_A8/D2_A6           |                                         |
|  49 | D3_A1/D2_A8           |                                         |
|  50 | D3_A11/D2_A11         |                                         |
|  51 | VDDC                  |                                         |
|  52 | D3_BA2/D2_NC          |                                         |
|  53 | D3_A0/D2_A12          |                                         |
|  54 | D3_A2/D2_A9           |                                         |
|  55 | D3_A9/D2_A7           |                                         |
|  56 | D3_RESET/D2_A5        |                                         |
|  57 | D3_A7/D2_A3           |                                         |
|  58 | D3_A5/D2_A10          |                                         |
|  59 | VDDIO_CMD1            |                                         |
|  60 | D3_A3/D2_A1           |                                         |
|  61 | D3_BA0/D2_BA2         |                                         |
|  62 | D3_WEZ/D2_BA0         |                                         |
|  63 | D3_CASZ/D2_BA1        |                                         |
|  64 | VDDC                  |                                         |
|  65 | VDDP_3                |                                         |
|  66 | TS1_CLK<sup>1</sup>   | I2S_IN_BCK<sup>1/3</sup>, TMS_MCU<sup>1</sup>                        |
|  67 | TS1_D7<sup>1</sup>    | I2S_IN_WS<sup>1/3</sup>, TDO_MCU<sup>1</sup>, UART2_TX<sup>1</sup>   |
|  68 | TS1_D6<sup>1</sup>    | I2S_IN_D0<sup>1/3</sup>, I2CM1_SDA<sup>4</sup>, UART2_RX<sup>1</sup> |
|  69 | TS1_D5<sup>1</sup>    | I2CM1_SCL<sup>4</sup>                   |
|  70 | TS1_D4<sup>1</sup>    | I2S_OUT_MUTE<sup>1/3</sup>              |
|  71 | TS1_D3<sup>1</sup>    | I2S_OUT_BCK<sup>1/3</sup>               |
|  72 | TS1_D2<sup>1</sup>    | I2S_OUT_D0<sup>1/3</sup>, SPI_CLK<sup>1/3/5/7 (MPIF)</sup> |
|  73 | TS1_D1<sup>1</sup>    | I2S_OUT_WS<sup>1/3</sup>, SPI_IRQ<sup>?</sup>              |
|  74 | TS1_D0<sup>1</sup>    | I2S_OUT_D1<sup>1/3</sup>, SPI_CSZ<sup>1/3/5/7 (MPIF)</sup> |
|  75 | TS1_VLD<sup>1</sup>   | I2S_OUT_D2<sup>1/3</sup>, SPI_MOSI<sup>1/3/5/7 (MPIF)</sup>, TDI_MCU<sup>1</sup>           |
|  76 | TS1_SYNC<sup>1</sup>  | I2S_OUT_MCK<sup>1/3</sup>, SPI_MISO<sup>1/3/5/7 (MPIF)</sup>, TCK_MCU<sup>1</sup>, EJ_DINT |
|  77 | VDDP_3                |                                         |
|  78 | VDDC                  |                                         |
|  79 | S_GPIO3               | UART1_RX<sup>3</sup>, EJ_RSTZ           |
|  80 | S_GPIO4               | UART1_TX<sup>3</sup>, EJ_TCK            |
|  81 | I2CM0_SDA<sup>1</sup> | UART1_RX<sup>2</sup>                    |
|  82 | I2CM0_SCL<sup>1</sup> | UART1_TX<sup>2</sup>                    |
|  83 | AVDD_MPLL             |                                         |
|  84 | XTAL_IN               |                                         |
|  85 | XTAL_OUT              |                                         |
|  86 | GPIO                  | EJ_TMS                                  |
|  87 | GPIO                  | EJ_TDO                                  |
|  88 | SAR0                  |                                         |
|  89 | SAR1                  |                                         |
|  90 | SAR2                  |                                         |
|  91 | SAR3                  |                                         |
|  92 | AVDD_NODIE            |                                         |
|  93 | DVDD_NODIE            |                                         |
|  94 | [UART_RX](../ip/commonpins.md#pm_uart_rx) |                     |
|  95 | [UART_TX](../ip/commonpins.md#pm_uart_tx) |                     |
|  96 | GPIO_PM9              |                                         |
|  97 | SPI_CLK               |                                         |
|  98 | SPI_DI                |                                         |
|  99 | SPI_DO                |                                         |
| 100 | SPI_CSZ               |                                         |
| 101 | GPIO_PM0              |                                         |
| 102 | GPIO_PM4              |                                         |
| 103 | IRIN                  |                                         |
| 104 | CEC                   |                                         |
| 105 | [RESET](../ip/commonpins.md#pm_reset) |                         |
| 106 | VDDC                  |                                         |
| 107 | TESTPIN               |                                         |
| 108 | SPDIF_OUT<sup>4</sup> | UART1_TX<sup>1</sup>, EJ_TDI            |
| 109 | HDMI_HPD              | UART1_RX<sup>1</sup>, EJ_TRST           |
| 110 | AVDD3P3_USB_VDDP_1    |                                         |
| 111 | USB_DM                |                                         |
| 112 | USB_DP                |                                         |
| 113 | HDMI_SDA              |                                         |
| 114 | HDMI_SCL              |                                         |
| 115 | AVDD33_HDMI           |                                         |
| 116 | HDMI_TXCN             |                                         |
| 117 | HDMI_TXCP             |                                         |
| 118 | HDMI_TX0N             |                                         |
| 119 | HDMI_TX0P             |                                         |
| 120 | AVDD1P2_HDMI          |                                         |
| 121 | HDMI_TX1N             |                                         |
| 122 | HDMI_TX1P             |                                         |
| 123 | HDMI_TX2N             |                                         |
| 124 | HDMI_TX2P             |                                         |
| 125 | LINE_OUTL             |                                         |
| 126 | LINE_OUTR             |                                         |
| 127 | AVDD3V3_AU            |                                         |
| 128 | AU_VRM                |                                         |

## MSD7818

- Package: eLQFP128
- Exposed pad is GND
- Superscript is the function's mux value

|  #  |         name          |              alt functions              |
|-----|-----------------------|-----------------------------------------|
|   1 | IDAC_OUT_X            |                                         |
|   2 | IDAC_OUT_B            |                                         |
|   3 | IDAC_OUT_G            |                                         |
|   4 | IDAC_OUT_R            |                                         |
|   5 | AVDD33_DAC            |                                         |
|   6 | VDDC                  |                                         |
|   7 | VDDIO_CMD1            |                                         |
|   8 | D3_ODT/D2_CKE         |                                         |
|   9 | D3_RASZ/D2_WEZ        |                                         |
|  10 | VDDIO_DATA            |                                         |
|  11 | D3_DQ4/D2_DQ4         |                                         |
|  12 | D3_DQ6/D2_DQ3         |                                         |
|  13 | D3_DQ2/D2_DQ1         |                                         |
|  14 | D3_DQ0/D2_DQ6         |                                         |
|  15 | D3_DQM1/D2_DQ11       |                                         |
|  16 | VDDIO_DATA            |                                         |
|  17 | D3_DQ13/D2_DQ12       |                                         |
|  18 | D3_DQ11/D2_DQ9        |                                         |
|  19 | D3_DQ15/D2_DQ14       |                                         |
|  20 | D3_DQ9/D2_DQM1        |                                         |
|  21 | DVDD_DDR              |                                         |
|  22 | D3_DQS0/D2_DQS0       |                                         |
|  23 | D3_DQSB0/D2_DWSB0     |                                         |
|  24 | D3_DQS1/D2_DQS1       |                                         |
|  25 | D3_DQSB1/D2_DQSB1     |                                         |
|  26 | AVDD_PLL              |                                         |
|  27 | D3_DQ12/D2_DQM0       |                                         |
|  28 | D3_DQ8/D2_DQ15        |                                         |
|  29 | D3_DQ14/D2_DQ8        |                                         |
|  30 | D3_DQ10/D2_DQ10       |                                         |
|  31 | D3_DQM0/D2_DQ13       |                                         |
|  32 | VDDIO_DATA            |                                         |
|  33 | D3_DQ3/D2_DQ7         |                                         |
|  34 | D3_DQ1/D2_DQ0         |                                         |
|  35 | D3_DQ5/D2_DQ2         |                                         |
|  36 | D3_DQ7/D2_DQ5         |                                         |
|  37 | VDDIO_DATA            |                                         |
|  38 | D3_MCLK/D2_MCLK       |                                         |
|  39 | D3_MCLKZ/D2_MCLKZ     |                                         |
|  40 | VDDIO_MCLK            |                                         |
|  41 | D3_CKE/D2_ODT         |                                         |
|  42 | D3_A10/D2_RASZ        |                                         |
|  43 | D3_BA1/D2_CASZ        |                                         |
|  44 | D3_A12/D2_A0          |                                         |
|  45 | D3_A4/D2_A2           |                                         |
|  46 | VDDIO_CMD0            |                                         |
|  47 | D3_A6/D2_A4           |                                         |
|  48 | D3_A8/D2_A6           |                                         |
|  49 | D3_A1/D2_A8           |                                         |
|  50 | D3_A11/D2_A11         |                                         |
|  51 | VDDC                  |                                         |
|  52 | D3_BA2/D2_NC          |                                         |
|  53 | D3_A0/D2_A12          |                                         |
|  54 | D3_A2/D2_A9           |                                         |
|  55 | D3_A9/D2_A7           |                                         |
|  56 | D3_RESET/D2_A5        |                                         |
|  57 | D3_A7/D2_A3           |                                         |
|  58 | D3_A5/D2_A10          |                                         |
|  59 | VDDIO_CMD1            |                                         |
|  60 | D3_A3/D2_A1           |                                         |
|  61 | D3_BA0/D2_BA2         |                                         |
|  62 | D3_WEZ/D2_BA0         |                                         |
|  63 | D3_CASZ/D2_BA1        |                                         |
|  64 | VDDC                  |                                         |
|  65 | VDDP_3                |                                         |
|  66 | TS1_CLK<sup>1</sup>   | EJ_DINT, I2S_IN_BCK<sup>1/3</sup>, TMS_MCU<sup>1</sup>                        |
|  67 | GPIO                  | EJ_RSTZ, I2S_IN_WS<sup>1/3</sup>, UART2_TX<sup>1</sup>, TDO_MCU<sup>1</sup>   |
|  68 | GPIO                  | EJ_TCK, I2S_IN_D0<sup>1/3</sup>, UART2_RX<sup>1</sup>, I2CM1_SDA<sup>4</sup>  |
|  69 | GPIO                  | EJ_TMS, I2CM1_SCL<sup>4</sup>           |
|  70 | TS1_D0<sup>1</sup>    | EJ_TDO                                  |
|  71 | TS1_VLD<sup>1</sup>   | EJ_TDI, TDI_MCU<sup>1</sup>             |
|  72 | TS1_SYNC<sup>1</sup>  | EJ_TRSTN, TCK_MCU<sup>1</sup>           |
|  73 | VDDP_3                |                                         |
|  74 | VDDC                  |                                         |
|  75 | I2CM0_SDA<sup>1</sup> | UART1_RX<sup>2</sup>                    |
|  76 | I2CM0_SCL<sup>1</sup> | UART1_TX<sup>2</sup>                    |
|  77 | AVDD33_ADC            |                                         |
|  78 | IM_I                  |                                         |
|  79 | IP_I                  |                                         |
|  80 | IM_Q                  |                                         |
|  81 | IP_Q                  |                                         |
|  82 | AVDD_MPLL             |                                         |
|  83 | XTAL_IN               |                                         |
|  84 | XTAL_OUT              |                                         |
|  85 | AVSS_MPLL             |                                         |
|  86 | IF_AGC                |                                         |
|  87 | RF_AGC                |                                         |
|  88 | SAR0                  |                                         |
|  89 | SAR1                  |                                         |
|  90 | SAR2                  |                                         |
|  91 | SAR3                  |                                         |
|  92 | AVDD_NODIE            |                                         |
|  93 | DVDD_NODIE            |                                         |
|  94 | [UART_RX](../ip/commonpins.md#pm_uart_rx) |                     |
|  95 | [UART_TX](../ip/commonpins.md#pm_uart_tx) |                     |
|  96 | GPIO_PM9              |                                         |
|  97 | SPI_CLK               |                                         |
|  98 | SPI_DI                |                                         |
|  99 | SPI_DO                |                                         |
| 100 | SPI_CSZ               |                                         |
| 101 | GPIO_PM0              |                                         |
| 102 | GPIO_PM4              |                                         |
| 103 | IRIN                  |                                         |
| 104 | CEC                   |                                         |
| 105 | [RESET](../ip/commonpins.md#pm_reset) |                         |
| 106 | VDDC                  |                                         |
| 107 | TESTPIN               |                                         |
| 108 | SPDIF_OUT<sup>4</sup> | UART1_TX<sup>1</sup>                    |
| 109 | HDMI_HPD              | UART1_RX<sup>1</sup>                    |
| 110 | AVDD3P3_USB           |                                         |
| 111 | USB_DM                |                                         |
| 112 | USB_DP                |                                         |
| 113 | HDMI_SDA              |                                         |
| 114 | HDMI_SCL              |                                         |
| 115 | AVDD33_HDMI           |                                         |
| 116 | HDMI_TXCN             |                                         |
| 117 | HDMI_TXCP             |                                         |
| 118 | HDMI_TX0N             |                                         |
| 119 | HDMI_TX0P             |                                         |
| 120 | AVDD1P2_HDMI          |                                         |
| 121 | HDMI_TX1N             |                                         |
| 122 | HDMI_TX1P             |                                         |
| 123 | HDMI_TX2N             |                                         |
| 124 | HDMI_TX2P             |                                         |
| 125 | LINE_OUT0L            |                                         |
| 126 | LINE_OUT0R            |                                         |
| 127 | AVDD3V3_AUSDM         |                                         |
| 128 | AU_VRM                |                                         |

## Bootstrap pins

| SPI_CSZ | SPI_DI |            mode             |
|---------|--------|-----------------------------|
|    1    |    0   | Normal boot (without EJTAG) |
|    1    |    1   | Normal boot (with EJTAG)    |
|    0    |    0   | SBUS1                       |
|    0    |    1   | DBUS1                       |
