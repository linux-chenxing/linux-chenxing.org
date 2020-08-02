### RNG

RNG block registermap:

| Offset | Name   | Comment |
|--------|--------| ---     |
| 0x00   | CTRL   | bit7 - enable/initialize? |
| 0x08   | VALUE  | The output value. Ready when STATUS[0] is 1 |
| 0x0C   | STATUS | bit0 - ready |

### SHA

SHA block registermap:

| Offset | Name  | Comment |
| ---    | ---   | ---     |
| 0x20   | CTRL  |         |
| bit 1  | CTRL_FIRE_ONCE | write 1 to fire once, |
| bit 6  | CTRL_CLR  | 
| bit 9  | CTRL_MODE | 0 = SHA-1 <BR> 1 = SHA-256 |
| bit 13 | CTRL_INIT_HASH | enable/disable initial hash value |
| bit 14 | CTRL_MANUAL | |
| 0x28   | BUF_ADDR_L | |
| 0x2C   | BUF_ADDR_H | |
| 0x30   | BUF_LEN_L  | |
| 0x34   | BUF_LEN_H  | |
| 0x38   | BUF_ADDR_L | |
| 0x3C   | STATUS | bit 0 = ready, bit 1 - busy ?|
| 0x40-0x5f | VALUE | When reading - the output value, when writing - initial hash value (big endian) |
| 0xB8   | WORD_CNT_L | count in 4-byte words, lower 16 bits |
| 0xBC   | WORD_CNT_H | higher 16 bits |

### RSA

### AESDMA

On infinity3 the base address is 0x1f224400
