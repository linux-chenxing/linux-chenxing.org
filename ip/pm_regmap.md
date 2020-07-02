# PM Regmap

Probably only for infinity/mercury5

## PM Ctrl registers - 0x1f001c00

| offset | name             | 15         | 14 | 13 | 12 | 11                 | 10 | 9 | 8 | 7 | 6 | 5 | 4             | 3               | 2                 | 1   | 0 | default | Notes                              |
|--------|------------------|------------|----|----|----|--------------------|----|---|---|---|---|---|---------------|-----------------|-------------------|-----|---|---------|------------------------------------|
| 0x20   | wake up source   |            |    |    |    |                    |    |   |   |   |   |   | rtc           |                 | wol               | sar |   |         |                                    |
| 0x24   |                  | power down |    |    |    | disable pm_uart rx |    |   |   |   |   |   |               |                 |                   |     |   |         |                                    |
| 0x48   | pm_lock          |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   |         | write 0xbabe to unlock pm_gpio4    |
| 0x70   |                  |            |    |    |    |                    |    |   |   |   |   |   | ir in is gpio | isoen2gpio4?    | link wkint2gpio4? |     |   |         |                                    |
| 0xb8   |                  |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   |         | write 0x79 to trigger a reset      |
| 0xbc   |                  |            |    |    |    |                    |    |   |   |   |   |   |               | temp sensor en? |                   |     |   |         |                                    |
| 0xc0   |                  |            |    |    |    |                    |    |   |   |   |   |   | ipl sets      |                 |                   | x   | x | 0x003   |                                    |
| 0xcc   |                  |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   |         | power down code writes 0x9fe8 here |
| 0xc8   |                  |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   |         | power down code writes 0x9fe8 here |
| 0xdc   |                  |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   |         | some pm code writes 0xa5 here      |
| 0xec   | resume address l |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   |         |                                    |
| 0xf0   | resume address h |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   |         |                                    |
| 0xf4   |                  |            |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   | 0x003f  | ipl sets to zero                   |

## mystery block - 0x1f007800?

The vendor pm suspend code does something here but the bootrom and ipl don't touch it.

| offset | name | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | Notes                                          |
|--------|------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|---|------------------------------------------------|
| 0x40   |      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | 0x0010 when booted, can write 0x00F9           |
| 0x44   |      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | 0x0001 when booted, can write 0xFFFF           |
| 0x48   |      |    |    |    |    |    |    |   |   |   | x | x |   |   |   |   |   | 0x0000 when booted, writing locks up processor |
