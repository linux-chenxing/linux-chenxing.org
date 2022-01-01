# SDIO

| offset | name   | 15 | 14 | 13 | 12 | 11 | 10 | 9          | 8           | 7       | 6         | 5       | 4       | 3       | 2      | 1      | 0        | comment |
|--------|--------|----|----|----|----|----|----|------------|-------------|---------|-----------|---------|---------|---------|--------|--------|----------|---------|
| 0x30   | SD_CTL |    |    |    |    |    |    | ERR_DET_ON | BUSY_DET_ON | CHK_CMD | JOB_START | ADMA_EN | JOB_DIR | DTRX_EN | CMD_EN | RSP_EN | RSPR2_EN |         |
|        |        |    |    |    |    |    |    |            |             |         |           |         |         |         |        |        |          |         |
|        |        |    |    |    |    |    |    |            |             |         |           |         |         |         |        |        |          |         |

## SD_CTL bits

| ERR_DET_ON | BUSY_DET_ON | CHK_CMD | JOB_START | ADMA_EN | JOB_DIR | DTRX_EN | CMD_EN | RSP_EN | RSPR2_EN | Result                                                                |
|------------|-------------|---------|-----------|---------|---------|---------|--------|--------|----------|-----------------------------------------------------------------------|
| x          |             |         |           |         |         | x       |        |        |          | Multiple error interrupts after starting transfer with no error flags |
|            |             |         |           |         |         |         |        |        |          |                                                                       |
