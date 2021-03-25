# 命令行使用代理


## 命令行使用代理

>基本原理一样，触类旁通
>

### 设置环境变量,临时生效

```bash
export http_proxy=http://127.0.0.1:1080
export https_proxy=https://127.0.0.1:1080
export ftp_proxy="http://127.0.0.1:1080"
export all_proxy="socks5://127.0.0.1:1080"
```

### 设置环境变量,永久生效

修改 `~/.bash.rc`

```bash
export http_proxy="http://127.0.0.1:1080"
export https_proxy="http://127.0.0.1:1080"
export ftp_proxy="http://127.0.0.1:1080"
export all_proxy="socks5://127.0.0.1:1080"
# 无需代理的主机或域名，可使用通配符
export no_proxy="localhost, 127.0.0.1, ::1, 10.*.*.*,"
```

### 取消设置环境变量

```bash
unset http_proxy
unset https_proxy
unset ftp_proxy
unset all_proxy
unset no_proxy
```

### apt-get代理,临时生效

在命令行临时带入
在`apt`命令后面增加`-o`选项
```bash
sudo apt-get -o Acquire::http::proxy="http://127.0.0.1:1080/"  update
sudo apt-get -o Acquire::https::proxy="https://127.0.0.1:1080/"  update
sudo apt-get -o Acquire::socks::proxy="socks5://127.0.0.1:1080/"  update
# 注意上面的使用'socks'是正确的，链接才是'socks5'
```

### apt-get代理,永久生效
修改 `/etc/apt/apt.conf`
```bash
Acquire::socks::proxy "socks5://127.0.0.1:1080/";
Acquire::http::proxy "http://127.0.0.1:1080/";
Acquire::https::proxy "https://127.0.0.1:1080/";
Acquire::ftp::proxy "ftp://127.0.0.1:1080/";
```



<!--more-->
