# PM Regmap

Probably only for infinity/mercury5

| offset | name           | 15 | 14 | 13 | 12 | 11                 | 10 | 9 | 8 | 7 | 6 | 5 | 4             | 3               | 2                 | 1   | 0 | Notes                           |
|--------|----------------|----|----|----|----|--------------------|----|---|---|---|---|---|---------------|-----------------|-------------------|-----|---|---------------------------------|
| 0x20   | wake up source |    |    |    |    |                    |    |   |   |   |   |   | rtc           |                 | wol               | sar |   |                                 |
| 0x24   |                |    |    |    |    | disable pm_uart rx |    |   |   |   |   |   |               |                 |                   |     |   |                                 |
| 0x48   | pm_lock        |    |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   | write 0xbabe to unlock pm_gpio4 |
| 0x70   |                |    |    |    |    |                    |    |   |   |   |   |   | ir in is gpio | isoen2gpio4?    | link wkint2gpio4? |     |   |                                 |
| 0xb8   |                |    |    |    |    |                    |    |   |   |   |   |   |               |                 |                   |     |   | write 0x79 to trigger a reset   |
| 0xbc   |                |    |    |    |    |                    |    |   |   |   |   |   |               | temp sensor en? |                   |     |   |                                 |
