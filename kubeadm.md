



## 关闭 selinux

```bash
$ setenforce 0
$ sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```

## 禁用 swap

```bash
# 临时关闭
$ swapoff -a

#永久关闭
$ sed -i '/swap/s/^\(.*\)$/#\1/g' /etc/fstab
```

## 修改 hostname 文件

```bash
$ hostnamectl set-hostname k8s-m1
```

## 修改 hosts 文件

```bash
$ vi /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

192.168.100.10 k8s-m1
192.168.100.20 k8s-n2
192.168.100.30 k8s-n3
```

## 关闭防火墙

```bash
$ systemctl disable --now firewalld

# $ systemctl stop firewalld
# $ systemctl disable firewalld
```

## 加载 `ipvs` 模块

```bash
tee /etc/modules-load.d/k8s-ipvs.conf <<EOF
ip_vs
ip_vs_rr
ip_vs_wrr
ip_vs_sh
nf_conntrack
EOF
```

## 将桥接的IPv4流量传递到iptables的链

```bash
$ cat > /etc/sysctl.d/k8s.conf << EOF
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

$ sysctl --system
```



## 配置时间同步

```bash
$ ntpdate time1.aliyun.com

$ crontab -e
0 */3 * * * /usr/sbin/ntpdate time1.aliyun.com
```

## 配置 `kubernetes` 源

```bash
$ tee /etc/yum.repos.d/kubernetes.repo <<EOF
[kubernetes]
name = kubernetes
baseurl = https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
enabled = 1
gpgcheck =1
gpgkey = https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg \
  https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
EOF
```

## 安装 `kubeadm` 包

```bash
# master
$ yum -y install kubeadm-1.23.13 kubectl-1.23.13 kubelet-1.23.13
# node
$ yum -y install kubeadm-1.23.13 kubelet-1.23.13
```

## 配置 `kubelet`

```bash
$ systemctl enable kubelet --now
```