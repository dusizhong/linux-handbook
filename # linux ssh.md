# ssh login

## add user
...

## add public key
- su houwenyao
- mkdir .ssh
- vi ~/.ssh/authorized_keys
- add pub key
`
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQD3L8q8JapFVbKNvIt2//++be9XBE4aiGZFKvVv8ytf4ol1aWKV11GEh0L+k3jA6ibd++NHI29xTpMAYVK1bhbra0b8CfOqT0MriyzIZGbeVTWcT6duppr4+aGApXc0AXtpRrhRi8ddD+Jr/fbMOqj0LxI4tKMjmbj/Ib61RDM27wB3dIywHJv/HwTVDDN6SmzQfyZl8Cn7VW7uC3pmhPtaYkLunzyw1lM7dkAji1ONNaIFGE40tIPL3TZkMAHRI0urmzl1BP6AkYw2+oReYDXDPTz0t/QAlqP9KIZvLp2qlBAfmf/Fa32pVkbTc+ebL/OfwwjxnWji4FYa+XDZl0ff 5663314@qq.com
`
- chmod 700  ~/.ssh
- chmod 0644  ~/.ssh/authorized_keys

- restorecon -R -v /home

- su root
- vi /etc/ssh/sshd_config
`
PasswordAuthentication no (禁用密码登录，可选)
RSAAuthentication yes
StrictModes no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
`

- systemctl restart sshd.service


## modify ssh port
- firewall-cmd --list-all
- firewall-cmd --zone=public --add-port=19520/tcp --permanent
- firewall-cmd --reload
- vi /etc/ssh/sshd_config
`
Port 22
Port 19520
`
- systemctl restart sshd.service
- systemctl status sshd
