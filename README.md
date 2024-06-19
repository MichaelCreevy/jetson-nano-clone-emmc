# jetson nano clone emmc

Connect the USB flash drive to the Jetson Nano, check the device number of the USB flash drive, such as sda, open the Jetson Nano terminal and enter.

	ls /dev/sd*

Format the USB flash drive.

	sudo mkfs.ext4 /dev/sda


Modify the startup path.
create 3 files {extlinuxsda.conf, extlinuxsdb.conf, extlinuxsdc.conf}

	sudo nano /boot/extlinux/extlinux.conf

	APPEND ${cbootargs} quietroot=/dev/sda1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 	console=tty0 fbcon=map:0 net.ifnames=0

	APPEND ${cbootargs} quietroot=/dev/sdb1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 	console=tty0 fbcon=map:0 net.ifnames=0

	APPEND ${cbootargs} quietroot=/dev/mmcblk0p1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 	console=tty0 fbcon=map:0 net.ifnames=0

Find the statement APPEND ${cbootargs} quiet root=/dev/mmcblk0p1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 console=tty0, modify mmcblk0p1 to sda.

Mount the USB flash drive.

	sudo mount /dev/sda /mnt

Copy the system to the USB flash drive (the process has no information to print, please wait patiently).

	sudo cp -ax / /mnt

After the copy is completed, uninstall the USB flash drive (do not unplug the USB flash drive).

	sudo umount /mnt/

Restart the system.

	sudo reboot now

