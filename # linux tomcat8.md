# linux nginx yum

## install
- netstat -tunlp |grep 8080
- groupadd tomcat
- useradd -M -s /bin/nologin -g tomcat -d /opt/tomcat tomcat
- sudo yum install wget
- cd ~
- wget https://www-eu.apache.org/dist/tomcat/tomcat-8/v8.5.99/bin/apache-tomcat-8.5.99.tar.gz --no-check-certificate
- mkdir /opt/tomcat
- tar xvf apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1
- cd /opt/tomcat
- chgrp -R tomcat /opt/tomcat
- chmod -R g+r conf
- chmod g+x conf
- chown -R tomcat webapps/ work/ temp/ logs/
- vi /etc/systemd/system/tomcat.service
`
# Systemd unit file for tomcat
[Unit]
Description=Apache Tomcat Web Application Container
After=syslog.target network.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment='CATALINA_OPTS=-Xms512M -Xmx4096M -server -XX:+UseParallelGC'
Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/bin/kill -15 $MAINPID

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
`
- systemctl daemon-reload
- systemctl start tomcat
- systemctl status tomcat
- systemctl enable tomcat 
- firewall-cmd --list-all
- firewall-cmd --zone=public --add-port=8080/tcp --permanent
- firewall-cmd --reload
- curl localhost:8080

## config
