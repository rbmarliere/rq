[Introduction](https://marliere.net/~ricardo/2023/10/08/better-workflow.html)

```
$ rq -h

usage: rq [-h] [-I IMG_DIR] [-k KERNEL] [--no-kernel] [-d DISK] [--no-disk]
          [-i INITRD] [-b BIOS] [-p PORT] [-f [F ...]] [-F [F ...]] [-c]
          [-a APPEND] [-g] [--wait-gdb] [--no-snapshot] [--debug]

Run qemu with sane defaults

options:
  -h, --help            show this help message and exit
  -I IMG_DIR, --img-dir IMG_DIR
                        directory containing images (e.g. initramfs, disk,
                        bios), can be set through RQ_IMGDIR environment variable
                        (default: /home/rbmarliere/images)
  -k KERNEL, --kernel KERNEL
                        kernel bootable image to use with -kernel (default:
                        linux/arch/x86/boot/bzImage)
  --no-kernel           do not use -kernel (default: False)
  -d DISK, --disk DISK  disk image to use with -drive (default:
                        /home/rbmarliere/images/disk.img)
  --no-disk             do not use -drive (default: False)
  -i INITRD, --initrd INITRD
                        initrd image to use with -initrd (default: None)
  -b BIOS, --bios BIOS  bios image to use with -bios (default:
                        /home/rbmarliere/images/seabios.bin)
  -p PORT, --port PORT  host's port to forward into guest's ssh port using -net
                        (default: 10022)
  -f [F ...]            file(s) to copy into the disk (default: None)
  -F [F ...]            file(s) to copy into the cpio initrd (default: None)
  -c, --crash           append crashkernel= to cmdline (default: False)
  -a APPEND, --append APPEND
                        append kernel parameters (default: None)
  -g, --gdb             use -s (default: False)
  --wait-gdb            use -S if -s is used (default: False)
  --no-snapshot         do not use -snapshot (default: False)
  --debug               print qemu command instead of running it (default:
                        False)
  -A ARCH, --arch ARCH  architecture to use (default: x86_64)

$ rq --debug

qemu-system-x86_64 \
    -m 8G \
    -smp 2,sockets=2,cores=1 \
    -net nic,model=e1000 \
    -net user,host=10.0.2.25,hostfwd=tcp::10022-:22 \
    -enable-kvm \
    -nographic \
    -bios /home/rbmarliere/images/seabios.bin \
    -snapshot \
    -kernel linux/arch/x86/boot/bzImage \
    -drive format=raw,file=/home/rbmarliere/images/disk.img
```
