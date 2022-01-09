# GE

- Seems to be at 0x1f281200 on i2m
- i2m version seems to be the same or similar to the mst786 one.

| offset | name                  | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6       | 5 | 4 | 3 | 2 | 1   | 0      | notes        |
|--------|-----------------------|----|----|----|----|----|----|---|---|---|---------|---|---|---|---|-----|--------|--------------|
| 0x0    |                       |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     | enable |              |
| 0x7c   | src/dst format        |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     |        |              |
| 0x80   | srcl                  |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     |        |              |
| 0x84   | srch                  |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     |        |              |
| 0x98   | dstl                  |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     |        |              |
| 0x9c   | dsth                  |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     |        |              |
| 0xc0   | src pitch             |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     |        |              |
| 0xcc   | dst pitch             |    |    |    |    |    |    |   |   |   |         |   |   |   |   |     |        |              |
| 0x164  |                       |    |    |    |    |    |    |   |   |   |         |   |   |   |   | rot | rot    | GE_SetRotate |
| 0x180  | cmd                   |    |    |    |    |    |    |   |   |   | bit blt |   |   |   |   |     |        |              |
| 0x1b8  | bit blt source width  |    |    |    |    | x  | x  | x | x | x | x       | x | x | x | x | x   | x      |              |
| 0x1bc  | bit blt source height |    |    |    |    | x  | x  | x | x | x | x       | x | x | x | x | x   | x      |              |
