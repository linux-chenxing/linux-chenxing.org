# ISP/Debug tool

# ISP protocol

Some details on the protocol are [here](http://boeglin.org/blog/index.php?entry=Flashing-a-BenQ-Z-series-for-free%40dom%40). The same windows tool is used for all MStar chips it seems so this is probably valid across the board.

## mercury 5

Doing an i2cdetect scan on the uart pins of the mercury gives these two i2c addresses.

```
$ i2cdetect -y 0
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- -- 49 -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- 59 -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- -- 
```
