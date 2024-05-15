# linux fdisk

## adjust space
- df -h
- fuser -m /home (yum install psmisc)
- kill 9 3174
- umount /home
- lvremove /dev/mapper/centos-home (yum -y install lvm2)
- lvcreate -L 500G -n home centos
- mkfs -t xfs /dev/mapper/centos-home
- mount /dev/mapper/centos-home /home
- lvextend -l +100%FREE /dev/mapper/centos-root
- xfs_growfs /dev/mapper/centos-root
