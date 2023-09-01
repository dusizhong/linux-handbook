# centos7 add user

## check
- cat /etc/group
- cat /etc/passwd

## add group
- groupadd mygroup

## add floder
- mkdir -p /var/www
- chown root:mygroup /var/www
- chmod 775 /var/www

## add user
`
注：
/bin/false是最严格的禁止login选项，一切服务都不能用。
/sbin/nologin只是不允许login系统。
`
- useradd -g mygroup [-s /sbin/nologin] houwenyao
- passwd houwenyao
- hwy@2580
- usermod -d /var/www houwenyao
