# Adding a new chip to this wiki

- If you have the chip at hand please get the chip id. In u-boot run ```md.w 0x1f003c00``` (usually you can smash enter or ctrl-c at power on to get access to u-boot).
- Try to get the firmware binary
- Try to dump the boot rom: Start logging in minicom, enter `md.b 0x0 0x10000`, clean up the dump and then feed it to https://github.com/gmbnomis/uboot-mdb-dump
