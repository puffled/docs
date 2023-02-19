the process is pretty much the same as any other gentoo installation (see [handbook](https://wiki.gentoo.org/wiki/Handbook:AMD64)), however you skip ***everything*** to do with preparing some live environment (this is android/android recovery), and you skip everything to do with partitioning.

### annoyances

 -  the root directory `/` is either an initramfs, or the system partition, so you will treat `/data` as your working directory (like `/mnt/gentoo` referenced in the handbook).
 - `/data` will likely be mounted with `nosuid`, so remount it, `mount -o suid,remount /data`.
 - selinux will likely be enabled, so disable it, `setenforce 0` (some devices have selinux force enabled, and this will not work, please use a better rom, or figure out how to get a kernel with runtime configurable/permanently disabled selinux).
 - there is also `CONFIG_ANDROID_PARANOID_NETWORKING` to screw with you, it is an in-kernel feature to restrict system call access to certain group ids. for internet usage, you will want to add `inet:x:3003:portage,<your username>` to `/etc/groups`.

### android boot image

obtain your device's boot image, from a partition (generally `/dev/block/by-name/boot`), or from an ota update package.

a boot image should look like the following

```bash
> file boot.img
boot.img: Android bootimg, kernel (0x10008000), ramdisk (0x11000000), page size: 2048, cmdline (buildvariant=userdebug)
```

to unpack and repack a boot image, use [osm0sis/mkbootimg](https://github.com/osm0sis/mkbootimg). extract the boot image:

```bash
/path/to/mkbootimg/unpackbootimg -i boot.img -o boot
```

configure your device-specific kernel, compile it (if it even compiles), then repack the boot image. repacking is somewhat
convoluted, so i recommend writing a script to generate boot images, as it is quite the large invocation:

```bash
#!/bin/bash

set -e

cp -v /usr/src/linux/arch/arm64/boot/Image boot/boot.img-kernel

/path/to/mkbootimg/mkbootimg \
        --base "$(cat boot/boot.img-base)" \
        --board "$(cat boot/boot.img-board)" \
        --cmdline "$(cat boot/boot.img-cmdline)" \
        --hashtype "$(cat boot/boot.img-hashtype)" \
        --header_version "$(cat boot/boot.img-header_version)" \
        --kernel 'boot/boot.img-kernel' \
        --kernel_offset "$(cat boot/boot.img-kernel_offset)" \
        --os_patch_level "$(cat boot/boot.img-os_patch_level)" \
        --os_version "$(cat boot/boot.img-os_version)" \
        --pagesize "$(cat boot/boot.img-pagesize)" \
        --ramdisk_offset "$(cat boot/boot.img-ramdisk_offset)" \
        --ramdisk 'boot/boot.img-ramdisk' \
        --second_offset "$(cat boot/boot.img-second_offset)" \
        --tags_offset "$(cat boot/boot.img-tags_offset)" \
        --output 'new-boot.img'
```
