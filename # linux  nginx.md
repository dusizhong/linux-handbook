# uos nginx

## check
- whereis nginx

## tar zip
- tar -zxvf nginx-1.20.2 -C /usr/local/nginx

## install
- cd /usr/local/nginx
- ./configure
- make
- make install

## config
- vi /usr/local/nginx/conf/nginx.conf
- mkdir /usr/local/nginx/logs

## start & stop
- cd /usr/local/nginx/sbin
- ./nginx
- ./nginx -s reload
- ./nginx -s stop

## firewall
- firewall-cmd --list-all
- sudo firewall-cmd --add-port=80/tcp --permanent
- firewall-cmd --reload

## boot enabled
- vi /usr/lib/systemd/system/nginx.service

`
[Unit]
Description=The nginx HTTP Server
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s stop
PrivateTmp=true

[Install]
WantedBy=multi-user.target
`
- systemctl start nginx.service
- systemctl status nginx.service
- systemctl enable nginx.service
- systemctl daemon-reload 

## boot enable way2 ?
- echo /usr/local/nginx/sbin >> /etc/rc.d/rc.local
- chmod +x /etc/rc.d/rc.local