# centos7 systemctl jar

## config
- cd /usr/lib/systemd/system
- vi ezjc-eureka-server.service
`
[Unit] 
Description=ezjc eureka server 
After=syslog.target network.target

[Service] 
Type=simple 

ExecStart=/usr/bin/java -jar /usr/local/ezjc-cloud/ezjc-eureka-server-1.0.jar 
ExecStop=/bin/kill -15 $MAINPID 

User=root 
Group=root 
 
[Install] 
WantedBy=multi-user.target
`

## use
- systemctl start ezjc-eureka-server
- systemctl stop ezjc-eureka-server
- systemctl enable ezjc-eureka-server
- systemctl disable ezjc-eureka-server

- systemctl daemon-reload
- systemctl start sell.service
