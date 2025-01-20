# project-yocto
yocto project is an open source project it's not a linux distribution it's creats one for your .

nmount the SD card:
sudo umount /dev/sdb1
sudo umount /dev/sdb2


 Write the .wic image to the SD card: 
 we'll use the dd command to write the image to the SD card (/dev/sdb in your case). 

sudo dd if=core-image-minimal-raspberrypi3-20250112224637.rootfs.wic of=/dev/sdb bs=4M status=progress


Insert the SD card into your Raspberry Pi: Now, the SD card is ready to boot the Raspberry Pi. Insert it into your Raspberry Pi and power it on!

