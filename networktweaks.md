# Advanced networking tweaks

* https://docs.komodoplatform.com/mmV1/guides/mmV1-Network-Optimization.html
* https://wwwx.cs.unc.edu/~sparkst/howto/network_tuning.php#Steps
* https://wiki.mikejung.biz/Sysctl_tweaks

```
sudo modprobe tcp_bbr
sudo nano /etc/sysctl.d/01-barterdex.conf
```

tweaked
---
```
net.core.rmem_default = 1048576
net.core.wmem_default = 1048576
net.core.rmem_max = 16777216
net.core.wmem_max = 16777216
net.ipv4.tcp_rmem = 4096 87380 16777216
net.ipv4.tcp_wmem = 4096 65536 16777216
net.ipv4.udp_rmem_min = 16384
net.ipv4.udp_wmem_min = 16384
net.core.netdev_max_backlog = 262144
net.ipv4.tcp_max_orphans = 262144
net.ipv4.tcp_max_syn_backlog = 262144
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_max_tw_buckets = 2000000
net.ipv4.ip_local_port_range = 16001 65530
net.core.somaxconn = 20480
net.ipv4.tcp_low_latency = 1
net.ipv4.tcp_slow_start_after_idle = 0
net.ipv4.tcp_mtu_probing = 1
net.ipv4.tcp_fastopen = 3
net.ipv4.tcp_limit_output_bytes = 131072
```
If modprobe succeeded
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```

`nano /etc/modules-load.d/modules.conf`
add line to end
`tcp_bbr`

undo
---
```
net.core.rmem_max = 212992
net.core.wmem_max = 212992
net.core.netdev_max_backlog = 1000
net.core.somaxconn = 128
net.ipv4.tcp_rmem = 4096        87380   6291456
net.ipv4.tcp_wmem = 4096        16384   4194304
net.ipv4.tcp_no_metrics_save = 0
net.ipv4.tcp_tw_reuse = 0
net.ipv4.tcp_max_orphans = 262144
net.ipv4.tcp_max_syn_backlog = 2048
net.ipv4.tcp_fin_timeout = 60
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.tcp_keepalive_intvl = 75
net.ipv4.tcp_synack_retries = 5
net.ipv4.tcp_syn_retries = 6
net.ipv4.tcp_max_tw_buckets = 262144
net.ipv4.ip_local_port_range = 32768    60999
```
