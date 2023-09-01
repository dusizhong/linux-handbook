# centos7 add vsftp user

## add
- groupadd sftp
- useradd -g sftp -s /sbin/nologin gdyh
- passwd gdyh
- chown root:sftp /home/gdyh
- chmod 755 /home/gdyh
- vi /etc/ssh/sshd_config
`
Subsystem	sftp	internal-sftp #启用内置的sftp
Match group sftp                      #匹配sftp这个用户组
ChrootDirectory %h                    #禁锢用户在家目录
`
- systemctl restart sshd

## test
- ssh -P 9026 gdyh@124.239.222.121
- put local remote