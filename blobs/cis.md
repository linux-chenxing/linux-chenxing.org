# CIS

https://github.com/wireless-tag-com/openwrt-ssd20x/blob/87d0cbd51907d3f053230381d9277e29ab0194bb/18.06/package/sigmastar/uboot-sstar/src/drivers/mstar/spinand/inc/common/drvSPINAND.h#L67

|      | 0x0      | 0x1      | 0x2      | 0x3      | 0x4      | 0x5      | 0x6      | 0x7      | 0x8      | 0x9      | 0xa       | 0xb       | 0xc      | 0xd      | 0xe      | 0xf      | Notes                                 |
|------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|-----------|-----------|----------|----------|----------|----------|---------------------------------------|
| 0x0  | 0x4d (M) | 0x53 (S) | 0x54 (T) | 0x41 (A) | 0x52 (R) | 0x53 (S) | 0x45 (E) | 0x4D (M) | 0x49 (I) | 0x55 (U) |  0x53 (S) |  0x46 (F) | 0x44 (D) | 0x43 (C) | 0x49 (I) | 0x53 (S) | Fixed magic header - MSTARSEMIUSFDCIS |
| 0x10 |          |          |          |          |          |          |          |          |          |          |           |           |          |          |          |          |                                       |
| 0x20 |          |          |          |          |          |          |          |          |          |          |           |           |          |          |          |          |                                       |
| 0x30 |          |          |          |          |          |          |          |          |          |          |           |           |          |          |          |          |                                       |
