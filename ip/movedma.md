# movedma

| offset | name                       | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0               | notes |
|--------|----------------------------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|-----------------|-------|
| 0x0    |                            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   | en              |       |
| 0x4    |                            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   | move0_offset_en |       |
| 0x8    |                            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   | move0_en_status |       |
| 0xc    | move0_src_start_addr_l     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x10   | move0_src_start_addr_h     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x14   | move0_dest_start_addr_l    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x18   | move0_dest_start_addr_h    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x1c   | move0_total_byte_cnt_l     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x20   | move0_total_byte_cnt_h     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x24   | move0_offset_src_width_l   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x28   | move0_offset_src_width_h   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x2c   | move0_offset_src_offset_l  |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x30   | move0_offset_src_offset_h  |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x34   | move0_offset_dest_width_l  |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x38   | move0_offset_dest_width_h  |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x3c   | move0_offset_dest_offset_l |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x40   | move0_offset_dest_offset_h |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x44   | dma_move0_left_byte_l      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
| 0x48   | dma_move0_left_byte_h      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
|        |                            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
|        |                            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |                 |       |
