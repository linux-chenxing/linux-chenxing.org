# PSPI

- Found on pioneer3

|      | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7   | 6   | 5            | 4            | 3          | 2          | 1          | 0          |             | value after writing 0xffff |
|------|----|----|----|----|----|----|---|---|-----|-----|--------------|--------------|------------|------------|------------|------------|-------------|----------------------------|
| 0x0  |    |    |    |    |    |    |   |   |     |     | sw rst?      | sw rst?      |            |            |            |            |             |                            |
| 0x4  |    |    |    |    |    |    |   |   | div | div | div          | div          | div        | div        | div        | div        |             | 0xff                       |
| 0x8  |    |    |    |    |    |    |   |   |     |     | read enable? | read enable? |            |            |            |            |             | 0x1fff                     |
| 0xc  |    |    |    |    |    |    |   |   |     |     |              | bit count    | bit count  | bit count  | bit count  | bit count  |             | 0x3f1f                     |
| 0x10 |    |    |    |    |    |    |   |   |     |     |              |              |            |            |            |            | delay cycle | 0xffff                     |
| 0x18 |    |    |    |    |    |    |   |   |     |     |              |              |            |            |            |            | wait cycle  | 0xffff                     |
| 0x20 |    |    |    |    |    |    |   |   |     |     |              |              |            |            |            | trigger    |             | 0x0                        |
| 0x30 |    |    |    |    |    |    |   |   |     |     |              |              |            |            |            |            | fifo?       |                            |
| 0x80 |    |    |    |    |    |    |   |   |     |     |              |              | data lanes | data lanes | data lanes | data lanes |             |                            |
| 0x84 |    |    |    |    |    |    |   |   |     |     |              | cs           | cs         |            | chip id    | chip id    | te mode?    |                            |
| 0x88 |    |    |    |    |    |    |   |   |     |     |              |              |            |            |            |            | te mode?    |                            |
