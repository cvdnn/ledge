
# 升级Linux内核
## 先导入elrepo的key，然后安装elrepo的yum源
```shell
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
```

## 列出可用的内核相关包
```shell
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```

## 升级为最新稳定版
```shell
yum --enablerepo=elrepo-kernel install kernel-ml
```

## 查看默认启动顺序
```shell
awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg
```

## 修改grub中默认的内核版本
```shell
vim /etc/default/grub
# grub2-set-default 0
```

## 重新创建内核配置
```
grub2-mkconfig -o /boot/grub2/grub.cfg

reboot
```

## 删除旧内核
```shell
rpm -qa | grep kernel
yum remove $(rpm -qa | grep kernel | grep -v $(uname -r))
```