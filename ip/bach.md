# Bach

## Bank address for infinity3/mercury5

[detailed here](https://github.com/fifteenhex/SDK_pulbic/blob/c1436fa7446457e8d6547874d27ee4e34be150cf/Mercury5/proj/sc/driver/hal/mercury/audio/inc/hal_bach.h#L41)

0x1f2a0400
0x1f2a0600
0x1f2a0800
0x1f206800

## bank 0

| offset | name                            | 15          | 14            | 13             | 12 | 11 | 10 | 9 | 8 | 7    | 6    | 5            | 4    | 3    | 2    | 1    | 0    |
|--------|---------------------------------|-------------|---------------|----------------|----|----|----|---|---|------|------|--------------|------|------|------|------|------|
| 0x00c  | mux0 sel                        |             |               |                |    |    |    |   |   |      |      | mmc1 src sel |      |      |      |      |      |
| 0x1d4  | dma test ctrl 5 (sine wave gen) | sine gen en | sine gen left | sine gen right |    |    |    |   |   | gain | gain | gain         | gain | freq | freq | freq | freq |
|        |                                 |             |               |                |    |    |    |   |   |      |      |              |      |      |      |      |      |

## bank 1 - DMA registers

| offset | name   | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|--------|--------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|---|
|        |        |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |
|        |        |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |
|        |        |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |

## bank 2

| offset | name         | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7          | 6       | 5       | 4      | 3     | 2     | 1        | 0    |
|--------|--------------|----|----|----|----|----|----|---|---|------------|---------|---------|--------|-------|-------|----------|------|
| 0x0    | analog ctrl0 |    |    |    |    |    |    |   |   |            |         |         |        |       |       |          |      |
| 0x4    | analog ctrl1 |    |    |    |    |    |    |   |   |            |         |         |        |       |       |          |      |
| 0x8    | analog ctrl2 |    |    |    |    |    |    |   |   |            |         |         |        |       |       |          |      |
| 0xc    | analog ctrl3 |    |    |    |    |    |    |   |   | mic stg1_l | ldo dac | ldo adc | l0 dac | inmux | inmux | bias dac | adc0 |
