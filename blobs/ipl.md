# IPL blobs

## First stage IPL loaded by the bootrom

- First 4 bytes are an ARM instruction to jump somewhere else in the IPL binary like a reset vector.
   This also seems to be generally used to switch from ARM to Thumb execution.
- Second 4 bytes are "IPL_"
- Third 4 bytes are the size of the IPL

## Second stage IPL loaded by the first stage IPL

The header format is the same as the first stage IPL but the second 4 bytes are "IPLC"
