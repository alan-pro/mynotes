# 1 基础
- 终端连接wsl中的ubuntu
```shell
wsl -d Ubuntu-20.04 -u ai
```
- 查询其中的ip地址
```shell
(base) ai@pro:/mnt/c/Users/pro$ ifconfig  # 使用net-tools

Command 'ifconfig' not found, but can be installed with:

sudo apt install net-tools

(base) ai@pro:/mnt/c/Users/pro$ ip addr  # 详细查询
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet 10.255.255.254/32 brd 10.255.255.254 scope global lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1460 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:a3:cc:3c brd ff:ff:ff:ff:ff:ff
    inet 172.18.254.30/20 brd 172.18.255.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::215:5dff:fea3:cc3c/64 scope link
       valid_lft forever preferred_lft forever
(base) ai@pro:/mnt/c/Users/pro$ hostname -I  # 简略查询
172.18.254.30
(base) ai@pro:/mnt/c/Users/pro$
```
