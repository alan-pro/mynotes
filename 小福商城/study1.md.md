# 1 基础
## 1.1 终端连接wsl中的ubuntu
```shell
wsl -d Ubuntu-20.04 -u ai

cd dev # 进入项目文件夹，通过配置.bashrc文件实现

[sudo] password for ai:12345
```


## 1.2 查询其中的ip地址
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


## 1.3 实现cd dev进入目的文件夹

-  方法一：使用符号链接（软链接）- 推荐
在 `/home/ai` 目录下创建一个指向 `dev` 的软链接：

```bash
cd ~
ln -s /home/ai/dev devlink
```
然后你就可以用 `cd devlink` 进入 `dev` 文件夹了。

但如果你想像你说的直接用 `cd dev`，可以创建同名的链接：
```bash
cd ~
ln -s /home/ai/dev dev
```
**注意**：如果 `~/dev` 目录已经存在，这个命令会失败。你可以先检查：
```bash
ls -la ~ | grep dev
```


- 方法二：使用 CDPATH 环境变量（更强大）
设置 `CDPATH` 让 `cd` 命令在指定目录中搜索：

在 `~/.bashrc` 或 `~/.bash_profile` 中添加：
```bash
export CDPATH=.:/home/ai
```
然后重新加载配置：
```bash
source ~/.bashrc
```
之后无论你在哪里，只要输入 `cd dev`，系统就会自动在 `/home/ai` 目录下查找 `dev` 文件夹并跳转。

- 方法三：使用别名（alias）
在 `~/.bashrc` 中添加别名：
```bash
alias cddev='cd /home/ai/dev'
```
然后输入 `cddev` 就可以跳转。

---

**推荐使用方法二**（CDPATH），因为它最接近你想要的效果：无论在哪里，输入 `cd dev` 就能直接进入 `/home/ai/dev`（只要没有同名的当前目录干扰）。

```shell
cd ~          # 先回主目录
cd /mnt/c/Users/pro  # 去 Windows 目录
cd dev        # 现在应该能直接跳转到 /home/ai/dev
```

## 1.4 Linux创建python环境

- 当Liunx中python版本与项目版本不一致时
```shell
# Ubuntu系统安装Python 3.9
sudo apt update  # 更新软件列表（获取最新信息）
sudo apt install python3.9 python3.9-venv python3.9-dev -y

# 安装后用Python 3.9创建虚拟环境
# python -m venv venv
python3.9 -m venv venv
source venv/bin/activate
python --version  # 应该显示Python 3.9.x
```

## 1.5 apt下载速度太慢
修改 sources.list（推荐，永久生效）

1. 备份原文件
```shell
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

2. 编辑 sources.list

```shell
sudo vim /etc/apt/sources.list
```

3. 替换为国内源（以清华源为例）

按 `dd` 删除所有内容，然后粘贴以下内容：

```shell
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

# 以下是 Ubuntu 官方合作伙伴源（包含一些第三方软件）
deb http://archive.canonical.com/ubuntu/ focal partner

# Docker 阿里云官方源
deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu focal stable
```

**注意**：上面的 `focal` 是 Ubuntu 22.04 的代号。请根据你的 Ubuntu 版本替换：

| Ubuntu版本 | 代号     |
| -------- | ------ |
| 24.04    | noble  |
| 22.04    | jammy  |
| 20.04    | focal  |
| 18.04    | bionic |

查看你的版本：

```shell
lsb_release -c
```

## 1.5 