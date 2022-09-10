# MSB123xC

MSB123xC is a family of the DVB-T/T2/C demodulator chips, which take raw IF from the tuner,
demodulates it and then outputs the demodulated stream through the MPEG-TS interface.

This page mostly talks about **MSB1236C**, althrough it might apply to other chips as well.

## Pinout

- Package: LQFP48

|  #  |  Name             |  #  |  Name             |
|-----|-------------------|-----|-------------------|
|   1 | I2CS_SCL          |  25 | VDD               |
|   2 | SS                |  26 | VSS               |
|   3 | XTAL_OUT          |  27 | VDD33             |
|   4 | XTAL_IN           |  28 | MSPI_CLK/SSPI_CSZ |
|   5 | AVDD_1            |  29 | RESETZ            |
|   6 | RF_AGC/GPIO       |  30 | VSS               |
|   7 | IF_AGC            |  31 | MSPI_DI/SSPI_DO   |
|   8 | QP                |  32 | MSPI_DO/SSPI_DI   |
|   9 | QM                |  33 | MSPI_CSZ/SSPI_CLK |
|  10 | VSS               |  34 | TS_CLK            |
|  11 | IP                |  35 | TS_D7             |
|  12 | IM                |  36 | TS_D6             |
|  13 | AVDD_2            |  37 | TS_D5             |
|  14 | VSS               |  38 | TS_D4             |
|  15 | NC                |  39 | TS_D3             |
|  16 | AVDD_3            |  40 | TS_D2             |
|  17 | VDD               |  41 | TS_D1             |
|  18 | VSS               |  42 | TS_D0             |
|  19 | GPIO0             |  43 | TS_VLD            |
|  20 | I2CM_SCL          |  44 | TS_SYNC           |
|  21 | I2CM_SDA          |  45 | VDD33             |
|  22 | VSS               |  46 | VSS               |
|  23 | VDD33             |  47 | VDD               |
|  24 | TS_ERR            |  48 | I2CS_SDA          |

### Strapping pins

| TS_ERR |  ???             |
|--------|------------------|
|  0     | normal           |
|  1     | SERDB disappears |
