# linux yum vsftp

## preparation
- rpm -aq vsftpd
- systemctl stop vsftpd
- rpm -e vsftpd
- wget http://mirror.centos.org/centos/7/updates/x86_64/Packages/vsftpd-3.0.2-29.el7_9.x86_64.rpm
- rpm -ivh vsftpd-3.0.2-29.el7_9.x86_64.rpm

## install
- systemctl start vsftpd
- systemctl enable vsftpd
- firewall-cmd --zone=public --add-port=30021-30030/tcp --permanent
- firewall-cmd --add-service=ftp --permanent
- firewall-cmd --reload

## add virtual ftp user
- yum -y install libdb-utils (if needed)
- vi /etc/vsftpd/vusers.txt
`
houwenyao
hwy@0301
zhangxiaojie
zxj@0301
`
- db_load -T -t hash -f /etc/vsftpd/vusers.txt /etc/vsftpd/vusers.db
- file /etc/vsftpd/vusers.*
- chmod 600 /etc/vsftpd/*
- useradd -d /usr/local/ebid-min -s /sbin/nologin -r ftpuser
- mkdir -p /usr/local/ebid-min
- cat > /etc/pam.d/ftp_vuser_auth <<EOF
auth required pam_userdb.so db=/etc/vsftpd/vusers
account required pam_userdb.so db=/etc/vsftpd/vusers
EOF

- cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.bak
- vi /etc/vsftpd/vsftpd.conf
`
anonymous_enable=NO
pasv_enable=YES
pasv_min_port=30023
pasv_max_port=30030
allow_writeable_chroot=YES
pam_service_name=ftp_vuser_auth
guest_enable=YES
guest_username=ftpuser
user_config_dir=/etc/vsftpd/vsftpd_user_conf
anon_umask=022
`

- mkdir /etc/vsftpd/vsftpd_user_conf
- cat > /etc/vsftpd/vsftpd_user_conf/houwenyao <<EOF
write_enable=YES
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_other_write_enable=YES
local_root=/usr/local/ebid-min/
EOF

## trouble 550 553 Permision deny
1. chown -R ftpuser:ftpuser /usr/local/ebid-min
2. chmod -R 755 /usr/local/ebid-min
3. make sure nginx.conf use root;
4.
- vi /etc/selinux/config
setenforce disable
- setenforce 0


## modify port (not use)
- vi /etc/vsftpd/vsftpd.conf
listen_port=30021
- vi /etc/services
ftp             30021/tcp
ftp             30021/udp
- systemctl reload vsftpd 
- netstat -apn|grep vsftpd

## test on centos
- yum install ftp -y
- wget http://mirror.centos.org/centos/7/os/x86_64/Packages/ftp-0.17-67.el7.x86_64.rpm (if needed)
- rpm -ivh ftp-0.17-67.el7.x86_64.rpm (if needed)
- ftp://124.239.222.121:30021

## test on win
- ftp
- open 192.168.2.100 30021 (open 8.142.211.10 30021)
- quote PORT