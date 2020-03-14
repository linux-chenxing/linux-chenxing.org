# infinity 6

This seems to be an updated version of the infinity3 IP camera SoCs.
The vendor kernel for these seems to be 4.9.84.

## Specs

- 16KB Boot ROM

## SSC325

- Chip id: 0xef

### Pinout

| #  | name      | #  | name      |
|----|-----------|----|-----------|
| 1  |           | 45 | fuart_cts |
| 2  |           | 46 | fuart_rts |
| 3  |           | 47 |           |
| 4  |           | 48 |           |
| 5  |           | 49 |           |
| 6  |           | 50 |           |
| 7  |           | 51 |           |
| 8  |           | 52 |           |
| 9  |           | 53 |           |
| 10 |           | 54 |           |
| 11 |           | 55 |           |
| 12 |           | 56 |           |
| 13 |           | 57 |           |
| 14 |           | 58 |           |
| 15 |           | 59 |           |
| 16 |           | 60 |           |
| 17 |           | 61 |           |
| 18 |           | 62 |           |
| 19 |           | 63 |           |
| 20 |           | 64 |           |
| 21 |           | 65 |           |
| 22 |           | 66 |           |
| 23 |           | 67 |           |
| 24 |           | 68 |           |
| 25 |           | 69 |           |
| 26 |           | 70 |           |
| 27 |           | 71 |           | 
| 28 |           | 72 |           |
| 29 |           | 73 |           |
| 30 |           | 74 |           |
| 31 |           | 75 |           |
| 32 |           | 76 |           |
| 33 |           | 77 |           |
| 34 |           | 78 |           |
| 35 | xtali     | 79 |           |
| 36 | xtalo     | 80 |           |
| 37 |           | 81 |           |
| 38 |           | 82 |           |
| 39 |           | 83 |           |
| 40 |           | 84 | usb_dm    |
| 41 |           | 85 | usb_dp    |
| 42 |           | 86 |           |
| 43 | fuart_rx  | 87 |           |
| 44 | fuart_tx  | 88 |           |
|    |           | ep |  gnd      |


### BootROM tag

```MVX1##I6g4d97980CMN_ROM######XVM```

## SSC326D

![SSC326D block diagram](ssc326d_blockdiagram.png)
