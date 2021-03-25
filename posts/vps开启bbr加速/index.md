# VPS开启bbr加速




## VPS开启BBR加速

#### 命令行终端：

```sh
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh
chmod +x bbr.sh
./bbr.sh
```

安装完成后，脚本会提示需要重启 VPS，输入 y 并回车后重启。

重启完成后，进入 VPS.

#### 验证是否成功安装

```bash
uname -r
查看内核版本，含有 4.13 就表示OK 了

sysctl net.ipv4.tcp_available_congestion_control
返回值一般为：
net.ipv4.tcp_available_congestion_control =bbr cubic reno

sysctl net.ipv4.tcp_congestion_control
返回值一般为：
net.ipv4.tcp_congestion_control = bbr

sysctl net.core.default_qdisc
返回值一般为：
net.core.default_qdisc = fq

lsmod | grep bbr
返回值有 tcp_bbr 模块即说明bbr已启动。
```

