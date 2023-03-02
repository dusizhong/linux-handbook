# uos mysql5.7

## check os version
- cat /etc/os-release

## delete mariadb
- rpm -qa|grep mariadb
- rpm -e --nodeps mariadb-libs-5.5.68-1.el7.x86_64

## tar zip
- tar -zxvf mysql-5.7.40
- mv mysql-5.7.40 mysql5.7

## add mysql user
- groupadd mysql
- useradd -r -g mysql mysql
- chown -R mysql:mysql /opt/mysql5.7/
- chmod -R 755 /opt/mysql5.7/

## install
- cd /opt/mysql5.7/bin
- ./mysqld --initialize --user=mysql --datadir=/opt/mysql5.7/data --basedir=/opt/mysql5.7
`
remember the temporary password: Kym9bujXos:a for root@localhost
`

## config
- vi /etc/my.cnf
`
[mysqld]
datadir=/opt/mysql5.7/data
port = 33066
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
symbolic-links=0
max_connections=400
innodb_file_per_table=1
`
- chmod -R 775 /etc/my.cnf
