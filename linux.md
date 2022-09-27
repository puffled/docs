### i have so many `/dev/ttyN`!!! isnt this bloat

they're literally virtual files (`/dev` is either `devtmpfs`, or `tmpfs`). if you ***REALLY*** want to remove them, modify `MAX_NR_CONSOLES`. i have no idea what setting it to less than `2` or higher than `63` will do, i cannot be bothered to try, you shouldn't try either.

`include/uapi/linux/vt.h`

```c
#define MIN_NR_CONSOLES 1  /* must be at least 1 */
#define MAX_NR_CONSOLES 63 /* serial lines start at 64 */
```

### notable groups `/dev` managers chown things to

for those who wish to go down the `/dev` manager-less route

- `/dev/dri` (`video` group, used by "modern" and *sane* graphics drivers)
- `/dev/nvidi*` (`video` group, used by nvidia, nvidia-modprobe uses this)
- `/dev/fb*` (`video` group, may or may not be used by xorg, graphics driver dependant)
- `/dev/input` (`input` group, used by xorg again, specifically, libinput, etc))
- `/dev/tty*` (`tty` group, used by xorg)


todo: efistub
