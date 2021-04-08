# movedma

| offset | name                       | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3                     | 2                     | 1                    | 0               | notes |
|--------|----------------------------|----|----|----|----|----|----|---|---|---|---|---|---|-----------------------|-----------------------|----------------------|-----------------|-------|
| 0x0    |                            |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      | en              |       |
| 0x4    |                            |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      | move0_offset_en |       |
| 0x8    |                            |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      | move0_en_status |       |
| 0xc    | move0_src_start_addr_l     |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x10   | move0_src_start_addr_h     |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x14   | move0_dest_start_addr_l    |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x18   | move0_dest_start_addr_h    |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x1c   | move0_total_byte_cnt_l     |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x20   | move0_total_byte_cnt_h     |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x24   | move0_offset_src_width_l   |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x28   | move0_offset_src_width_h   |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x2c   | move0_offset_src_offset_l  |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x30   | move0_offset_src_offset_h  |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x34   | move0_offset_dest_width_l  |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x38   | move0_offset_dest_width_h  |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x3c   | move0_offset_dest_offset_l |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x40   | move0_offset_dest_offset_h |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x44   | dma_move0_left_byte_l      |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x48   | dma_move0_left_byte_h      |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x90   | dma_mov_sw_rst             |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x94   | dma02mi_priority_mask      |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x98   | dma_irq_mask               |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x9c   | dma_irq_force              |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xa0   | dma_irq_clr                |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xa4   | dma_irq_select             |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xa8   | dma_irq_final_status       |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xac   | dma_irq_raw_status         |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xb0   | dma_probe_sel              |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xb4   | dma_probe_l                |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xb8   | dma_probe_h                |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xbc   | dma_bist_fail_rd           |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0xc0   |                            |    |    |    |    |    |    |   |   |   |   |   |   | dma_move0_dst_miu_sel | dma_move0_src_miu_sel | dma_move0_miu_sel_en |                 |       |
| 0x100  | dma_cmdq_irq_mask          |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x104  | dma_cmdq_irq_force         |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x108  | dma_cmdq_irq_clr           |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x10c  | dma_cmdq_irq_select        |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x110  | dma_cmdq_irq_final_status  |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
| 0x114  | dma_cmdq_irq_raw_status    |    |    |    |    |    |    |   |   |   |   |   |   |                       |                       |                      |                 |       |
