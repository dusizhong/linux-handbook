# linux fdisk

## check info
- fdisk -l
- lsblk
- df -h

### move /home space to /

1. remove old home
- df -h
- umount /home
- lvremove /dev/centos/home
- vgdisplay

2. create new home
- lvcreate -L 50G -n home centos
- lvdisplay
- vgdisplay
- vgchange -ay centos
- mkfs -t xfs /dev/centos/home
- mount /dev/centos/home /home
- df -h

2. extend /
- vgdisplay
- lvextend -L +891.12G /dev/centos/root
- lvdisplay
- vgchange -ay centos
- xfs_growfs /dev/centos/root
- df -h
