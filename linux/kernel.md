## 查看可使用的内核列表

```shell
$ awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg
0 : CentOS Linux (6.1.1-1.el7.elrepo.x86_64) 7 (Core)
1 : CentOS Linux (0-rescue-f6011318d1ac441ea220e3773ff41c80) 7 (Core)
```

## 删除旧内核

```shell
$ yum -y remove $(rpm -qa | grep kernel | grep -v $(uname -r))
已加载插件：fastestmirror
正在解决依赖关系
--> 正在检查事务
---> 软件包 kernel.x86_64.0.3.10.0-862.el7 将被 删除
---> 软件包 kernel.x86_64.0.3.10.0-1160.81.1.el7 将被 删除
--> 解决依赖关系完成

依赖关系解决

============================================================================================================
 Package              架构                版本                     源                大小
============================================================================================================
正在删除:
 kernel            x86_64             3.10.0-862.el7            @anaconda          62 M
 kernel            x86_64             3.10.0-1160.81.1.el7      @updates          66 M

事务概要
============================================================================================================
移除  2 软件包

安装大小：127 M
是否继续？[y/N]：y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在删除    : kernel.x86_64                             1/2
  正在删除    : kernel.x86_64                             2/2
  验证中      : kernel-3.10.0-1160.81.1.el7.x86_64        1/2
  验证中      : kernel-3.10.0-862.el7.x86_64              2/2

删除:
  kernel.x86_64 0:3.10.0-862.el7
  kernel.x86_64 0:3.10.0-1160.81.1.el7

完毕！
```

