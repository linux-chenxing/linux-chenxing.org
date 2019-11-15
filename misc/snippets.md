# Snippets

## Dump out PM GPIO registers

```
GPIO_BASE=1F001E00; \
for GPIO in `seq 0 127`; do \
    offset=`echo "obase=16;$GPIO*4" | bc`; \
    address=`echo "obase=16;ibase=16;$GPIO_BASE+$offset" | bc`; \
    echo "$address ($offset)"; \
    devmem 0x$address 16; \
done
```
