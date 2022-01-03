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
|            | x           |         |           |         | x       | x       |        |        |          | Gets stuck                                                            |

## ADMA

ADMA is pretty simple:
 - Create a list of descriptors
 - set the ADMA enable bit
 - set the DMA addr to the location of the first descriptor
 - set the DMA len to 0x10
 - set the DMA job count to 1
 - trigger and wait

### ADMA descriptor format

| offset | name       | 31      | 30      | 29      | 28      | 27      | 26      | 25      | 24      | 23      | 22      | 21      | 20      | 19      | 18      | 17      | 16      | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2       | 1       | 0   | notes                         |
|--------|------------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|----|----|----|----|----|----|---|---|---|---|---|---|---|---------|---------|-----|-------------------------------|
| 0x0    | ctrl/flags | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt | job cnt |    |    |    |    |    |    |   |   |   |   |   |   |   | miu sel | miu sel | end | end - list descriptor in list |
| 0x4    | dma addr   |         |         |         |         |         |         |         |         |         |         |         |         |         |         |         |         |    |    |    |    |    |    |   |   |   |   |   |   |   |         |         |     |                               |
| 0x8    | dma len    |         |         |         |         |         |         |         |         |         |         |         |         |         |         |         |         |    |    |    |    |    |    |   |   |   |   |   |   |   |         |         |     |                               |
| 0xc    | padding    |         |         |         |         |         |         |         |         |         |         |         |         |         |         |         |         |    |    |    |    |    |    |   |   |   |   |   |   |   |         |         |     |                               |
