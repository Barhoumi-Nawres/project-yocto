# project-yocto
yocto project is an open source project it's not a linux distribution it's creats one for your .
we need to create two partition on SD card one for boot and the other for root 
using the flowing commands :
```bash
sudo fdisk /dev/sdb
sudo mkfs.vfat /dev/sdb1
sudo mkfs.ext4 /dev/sdb2
```
the result :
```bash

nawres@nawres:~/project/poky/build/tmp/deploy/images/raspberrypi3-64$ lsblk /dev/sdb
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sdb      8:16   1 14.8G  0 disk 
├─sdb1   8:17   1  256M  0 part 
└─sdb2   8:18   1 14.6G  0 part 
nawres@nawres:~/project/poky/build/tmp/deploy/images/raspberrypi3-64$ 
```
nmount the SD card:

```bash
sudo umount /dev/sdb1
sudo umount /dev/sdb2
```

 Write the .wic image to the SD card: 
  we'll use the dd command to write the image to the SD card (/dev/sdb in your case). 
 ```bash
sudo dd if=core-image-minimal-raspberrypi3-20250112224637.rootfs.wic of=/dev/sdb bs=4M status=progress
```
or 
```bash
bzip2 -dc core-image-minimal-raspberrypi3-64.rootfs-20250120212228.wic.bz2 | sudo dd of=/dev/sdX bs=1M iflag=fullblock oflag=direct conv=fsync

```

Check the Root Filesystem:

```bash
sudo mount /dev/sdb2 /mnt
ls /mnt
sudo umount /mnt
```
the result:
```bash
es:~/project/poky/build/tmp/deploy/images/raspberrypi3-64$ ls /mnt
bin  boot  dev  etc  home  lib  lost+found  media  mnt  proc  root  run  sbin  srv  sys  tmp  usr  var
```
for sdb1:

```bash
p/deploy/images/raspberrypi3-64$ sudo mount /dev/sdb1 /mnt
nawres@nawres:~/project/poky/build/tmp/deploy/images/raspberrypi3-64$ ls /mnt
bcm2710-rpi-3-b.dtb       bcm2837-rpi-3-b.dtb  config.txt    fixup4db.dat  fixup.dat     kernel8.img                   start4cd.elf  start4x.elf   start.elf
bcm2710-rpi-3-b-plus.dtb  bootcode.bin         fixup4cd.dat  fixup4x.dat   fixup_db.dat  overlays                      start4db.elf  start_cd.elf  start_x.elf
bcm2710-rpi-cm3.dtb       cmdline.txt          fixup4.dat    fixup_cd.dat  fixup_x.dat   rpi-bootfiles-20240319.stamp  start4.elf    start_db.elf
```


Insert the SD card into your Raspberry Pi: Now, the SD card is ready to boot the Raspberry Pi. Insert it into your Raspberry Pi and power it on!

