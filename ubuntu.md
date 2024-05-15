# ubuntu server 22.04

## command
- ls /usr/bin 查看所有命令
- man ls 查看命令帮助
- ls --help 查看命令帮助

## apt
- sudo apt update
- sudo apt upgrade
- suod apt install


## usage
- 文件大小前50排序 du -h * 2>/dev/null | sort -rh | head -50
- 查看进程 ps -aux|grep xxx
- 查看时间 date
- 查看网卡 ifconfig
- 查看端口 netstat -tlnp | grep xx
- 查看系统 cat/etc/redhat-release
- 查看磁盘 df -hl
- 查看目录 du -sh xx


## 服务无法curl访问带域名网站处理（调用互联网API接口(腾讯、阿里)等出现“未知名称或服务”）
-  vi /etc/resolv.conf
`
nameserver 8.8.8.8
`

## wifi settings
- sudo apt install net-tools wpasupplicant
- ls /sys/class/net/
- ifconfig -a
- sudo vi /etc/netplan/00-intaller-config-wifi.yaml
`
network:
  version:2
wifis:
  wlo1:
    dhcp4: true
    access-points:
      yanfa_5G
        password: ezjc8888
`
- netplay try
- sudo netplan apply  
- sudo systemctl restart systemd-networkd


