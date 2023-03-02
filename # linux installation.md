# linux installation

## install centos7
1. prepartion
- make Ukey by ultraISO & modify label is CENTOS7
- handle 'dracut-initqueue' when boot install failed:
- input dracut:/# blkid show ukey info: /dev/sdb4: LABEL="CENTOS7" UUID="B4FE-5315" TYPE="vfat"
- press 'e' in install menu & modify sepcify ukey info:
- linuxefi /images/pxeboot/vmlinuz inst.stage2=hd:/dev/sdb4 quiet
- Ctrl+x

2. start install...
- set language: English
- set datetime: Asia/Shanghai

3. installation destination
- select hd-disk and configure partitioning
- delete unknow partition in list
- select Standard Partition
- add boot 500mb
- add boot/efi 200mb
- add swap 128G
- add / avaiable space
- accept done

4. network settings
- General: check: Automatically connect to this network when it is available
- IPv4 Settings: add ip mask gateway dns
- check: Require IPv4 addressing for this connection to complete

5. set root
- root Yanfa@0228

6. install complete & reboot

7. fix datetime
- yum -y install ntp ntpdate
- ntpdate cn.pool.ntp.org
- hwclock --systohc

8. have done!