# centos7 add user

## check
- cat /etc/group
- cat /etc/passwd

## add path
- mkdir /usr/local/ebidmin-cloud
- chmod -R 750 /usr/local/ebidmin-cloud

## add group (not use)
- groupadd javadeveloper
- chgrp javadeveloper /usr/local/ebidmin-cloud

## add user
- useradd zhangzheng
- passwd zhangzheng
- zz@0301
- id zhangzheng
- usermod -d /usr/local/ebidmin-cloud/ -u 1000 zhangzheng
