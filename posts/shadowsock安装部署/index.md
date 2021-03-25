# Shadowsock安装部署|bbr




## Shadowsocks-install

---
### 升级软件更新系统

```bash
 	yum update -y
	yum upgrade -y
```
---

### 官方安装说明

#### 安装

Debian / Ubuntu:

    apt-get install python-pip
    pip install git+https://github.com/shadowsocks/shadowsocks.git@master

CentOS:

    yum install python-setuptools && easy_install pip
    pip install git+https://github.com/shadowsocks/shadowsocks.git@master

CentOS 7 如果需要 AEAD 密码, 请安装 libsodium
```
dnf install libsodium python34-pip
pip3 install  git+https://github.com/shadowsocks/shadowsocks.git@master
```
带有[snap](http://snapcraft.io/)的Linux发行版:

    snap install shadowsocks

Windows:

请查看: [Install Shadowsocks Server on Windows](https://github.com/shadowsocks/shadowsocks/wiki/Install-Shadowsocks-Server-on-Windows).

#### 用法

    ssserver -p 443 -k password -m aes-256-cfb

后台运行:

    sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start

停止:

    sudo ssserver -d stop

检查日志 log:

    sudo less /var/log/shadowsocks.log

通过检查所有选项`-h`。您也可以改用[配置]文件。

如果安装了[snap](http://snapcraft.io/) 软件包，则必须在命令前面加上`shadowsocks`.，例如：

    shadowsocks.ssserver -p 443 -k password -m aes-256-cfb

#### 使用配置文件

[Create configuration file and run](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File)

启动:

    ssserver -c /etc/shadowsocks.json

---

###  pip 安装说明

#### 安装python和pip

```bash
	yum install python python-pip -y	#安装python和pip
	pip install shadowsocks
	#安装shadowsocks 如果报错,按提示升级pip
	pip install --upgrade pip
```
---
#### config

* 配置文件需拷贝进 /etc 目录下
``` bash
	#多用户配置文件
	vim /etc/shadowsocks.json
	
	{
    "server": "0.0.0.0",
    "port_password": {
        "8381": "foobar1",
        "8382": "foobar2",
        "8383": "foobar3",
        "8384": "foobar4"
    },
    "timeout": 300,
    "method": "aes-256-cfb"
	}
```

* shadowsocks.service
```bash
	vim /etc/systemd/system/shadowsocks.service
	#文件放置在	/etc/systemd/system/ 目录下.
```
```bash
[Unit]  
Description=Shadowsocks  
  
[Service]  
TimeoutStartSec=0  
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json  
  
[Install]  
WantedBy=multi-user.target
```

```bash
chmod +x  /etc/systemd/system/shadowsocks.service
```

* 如下报错请修改

```bash
vim /usr/lib/python2.7/site-packages/shadowsocks/crypto/openssl.py


libcrypto.EVP_CIPHER_CTX_cleanup.argtypes = (c_void_p,)
## 改成
libcrypto.EVP_CIPHER_CTX_reset.argtypes = (c_void_p,)

libcrypto.EVP_CIPHER_CTX_cleanup(self._ctx)
## 改成
libcrypto.EVP_CIPHER_CTX_reset(self._ctx)

```

```bash
INFO: loading config from /etc/shadowsocks.json
2021-03-07 08:46:36 INFO     loading libcrypto from libcrypto.so.10
2021-03-07 08:46:36 INFO     starting server at 207.246.108.196:8001
Traceback (most recent call last):
  File "/usr/bin/ssserver", line 11, in <module>
    load_entry_point('shadowsocks==2.8.2', 'console_scripts', 'ssserver')()
  File "/usr/lib/python3.4/site-packages/shadowsocks/server.py", line 68, in main
    tcp_servers.append(tcprelay.TCPRelay(a_config, dns_resolver, False))
  File "/usr/lib/python3.4/site-packages/shadowsocks/tcprelay.py", line 582, in __init__
    server_socket.bind(sa)
OSError: [Errno 99] Cannot assign requested address

```


* 启动'停止'查看状态:
```bash
	systemctl start shadowsocks
	systemctl stop shadowsocks
	systemctl status shadowsocks
```
* bbr加速脚本
```bash
	./bbr.sh	#自动配置安装脚本.
```
---

