# linux nginx yum

## 安装
- netstat -tunlp |grep 80
- sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
- sudo yum install -y nginx
- sudo systemctl start nginx.service
- sudo systemctl enable nginx.service
- firewall-cmd --list-all
- firewall-cmd --zone=public --add-port=80/tcp --permanent
- firewall-cmd --reload
- curl localhost

## 配置总的上传文件大小
- vi /etc/nginx/nginx.conf
`
http {
	client_max_body_size 1024m;
}
`

## 配置新增站点
- /etc/nginx/conf.d/default.conf
- cp default.conf yoursite.conf
- vi yoursite.conf
- chmod -R 755 /usr/local/yoursite

## 配置websocket转发
`
location /ws {
	proxy_pass http://127.0.0.1:9501;
	proxy_set_header Host $host;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_http_version 1.1;
	proxy_set_header Upgrade $http_upgrade;
	proxy_set_header Connection "Upgrade";
}
`

## 解决新增上传文件目录403问题
`
基本权限：r,w,x(读,写,执行)
drwxr-xr-x. d表示目录，第一组（rwx）所有者的权限读写执行 ，第二组（r-x）读，和执行，第三组（r-x）读，和执行
三种所属位置分别用u,g,o来表示三种位置（所有者，所属组，其他人）
`
### 设置所有者及权限
- chown nginx:nginx temp/
- chmod 755 temp/

### 子目录自动继承父目录的所属组的身份（-R只改变已有的文件）
- chmod g+s temp/

### 让使用者具有文件属主身份和部分权限
- chmod u+s temp/
### 限制当前用户操作别人的文档
- chmod o+t temp/
### 单个设置某一个用户的权限(rwx)
- setfacl -m u:tom:rwx temp/

## 解决无法配置80外的其他端口问题
- vi /etc/selinux/config
`
SELINUX = disabled
`
- reboot