# Centos7 修改SSH 端口

## 修改/etc/ssh/sshd_config

```shell
vi /etc/ssh/sshd_config

Port 22
Port 4850
```

## 修改firewall配置

```shell
# 添加到防火墙：
$ firewall-cmd --zone=public --add-port=4850/tcp --permanent
# (permanent是保存配置，不然下次重启以后这次修改无效)

# 重启：
$ firewall-cmd --reload

# 查看添加端口是否成功，如果添加成功则会显示yes，否则no
$ firewall-cmd --zone=public --query-port=4850/tcp
```

## 修改SELinux

```shell
# 查看当前SElinux 允许的ssh端口
$ semanage port -l | grep ssh

# 添加4850端口到 SELinux
$ semanage port -a -t ssh_port_t -p tcp 4850
$ semanage port -l | grep ssh
ssh_port_t                    tcp    4850, 22

$ systemctl restart sshd.service
```

