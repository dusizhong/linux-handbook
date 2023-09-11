# linux nginx yum

## install
- netstat -tunlp |grep 80
- sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
- sudo yum install -y nginx
- sudo systemctl start nginx.service
- sudo systemctl enable nginx.service
- firewall-cmd --list-all
- firewall-cmd --zone=public --add-port=80/tcp --permanent
- firewall-cmd --reload
- curl localhost

## selinum 解决无法配置80外的其他端口问题
- vi /etc/selinux/config
`
SELINUX = disabled
`
- reboot

## config
- vi /etc/nginx/nginx.conf
`
http {
	client_max_body_size 1024m;
}
`
- /etc/nginx/conf.d/default.conf
- cp default.conf yoursite.conf
- vi yoursite.conf
- chmod -R 755 /usr/local/yoursite
