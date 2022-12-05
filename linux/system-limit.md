## 系统调优参数

```bash
tee /etc/sysctl.d/k8s.conf <<EOF
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
net.ipv4.neigh.default.gc_stale_time = 120
net.ipv4.conf.all.rp_filter = 0
net.ipv4.conf.default.rp_filter = 0
net.ipv4.conf.default.arp_announce = 2
net.ipv4.conf.lo.arp_announce = 2
net.ipv4.conf.all.arp_announce = 2
net.ipv4.ip_forward = 1
net.ipv4.tcp_max_tw_buckets = 5000
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_synack_retries = 2
# 要求iptables不对bridge的数据进行处理
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-arptables = 1
net.netfilter.nf_conntrack_max = 2310720
fs.inotify.max_user_watches=89100
fs.may_detach_mounts = 1
fs.file-max = 52706963
fs.nr_open = 52706963
vm.overcommit_memory=1
# 开启OOM
vm.panic_on_oom=0
# 禁止使用 swap 空间，只有当系统 OOM 时才允许使用它
vm.swappiness=0
# ipvs优化
net.ipv4.tcp_keepalive_time = 600
net.ipv4.tcp_keepalive_intvl = 30
net.ipv4.tcp_keepalive_probes = 10
EOF

sysctl --system
Copy
```

### 文件最大打开数

```bash
tee /etc/security/limits.d/k8s.conf <<EOF
*       soft    nproc   1048576
*       hard    nproc   1048576
*       soft    nofile  1048576
*       hard    nofile  1048576
root    soft    nproc   1048576
root    hard    nproc   1048576
root    soft    nofile  1048576
root    hard    nofile  1048576
EOF
Copy
```

### 优化日志处理，减少磁盘IO

```bash
sed -ri 's/^\$ModLoad imjournal/#&/' /etc/rsyslog.conf
sed -ri 's/^\$IMJournalStateFile/#&/' /etc/rsyslog.conf

sed -ri 's/^#(DefaultLimitCORE)=/\1=100000/' /etc/systemd/system.conf
sed -ri 's/^#(DefaultLimitNOFILE)=/\1=100000/' /etc/systemd/system.conf
```