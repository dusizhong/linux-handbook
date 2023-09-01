# uos yum mysql5.7

## set rpm
- wget http://repo.mysql.com/mysql57-community-release-el7-10.noarch.rpm
- rpm -Uvh mysql57-community-release-el7-10.noarch.rpm

## install
- yum install -y mysql-community-server --nogpgcheck
- systemctl start mysqld.service
- systemctl enable mysqld.service
- systemctl daemon-reload

- grep 'temporary password' /var/log/mysqld.log
- mysql -uroot -p
- ALTER USER 'root'@'localhost' IDENTIFIED BY 'Uk9CWq*Ak';
- GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'Uk9CWq*Ak' WITH GRANT OPTION; //allow remote connnect
- FLUSH PRIVILEGES;
- exit;

- firewall-cmd --state (systemctl start firewalld)
- firewall-cmd --zone=public --add-port=3306/tcp --permanent
- firewall-cmd --reload

## remove rpm
- rpm -qa | grep mysql
- yum -y remove mysql57-community-release-el7-10.noarch


## config datadir
- vi /etc/my.cnf
