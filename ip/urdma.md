# URDMA

UART DMA controller for Fast UART


## Broken ring buffer logic?

For tx at least:

- The read pointer resets to zero
- The write pointer needs to be manually reset to zero if it's been written with a different value previously
- The logic seems to be broken in that the write point points to the currently filled byte and not the next to fill byte
   - i.e. Usually if the read point is at 0 and the write pointer is at 1 it means there is a byte at 0, and 1 will be filled next
   - But in URDMA the write point seems to pointer at the last filled byte.
   - So you get the weird sitation that both pointers being zero means the buffer is empty or there is a byte to tx at 0
   - buffering one byte and setting write point to 1 causes two bytes to be transmitted.
