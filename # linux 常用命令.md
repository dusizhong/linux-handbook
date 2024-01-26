# linux usage

## usage
- 文件大小前50排序 du -h * 2>/dev/null | sort -rh | head -50
- 查看进程 ps -aux|grep xxx
- 查看时间 date
- 查看网卡 ifconfig
- 查看端口 netstat -natp | grep xx
- 查看系统 cat/etc/redhat-release
- 查看磁盘 df -hl
- 查看目录 du -sh xx


## 服务无法curl访问带域名网站处理（调用互联网API接口(腾讯、阿里)等出现“未知名称或服务”）
-  vi /etc/resolv.conf
`
nameserver 8.8.8.8
`


