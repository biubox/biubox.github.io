# Ubuntu清除卸载后的软件包数据




## Ubuntu清除卸载后的包数据

### 单独卸载包时清除配置

```bash
sudo apt-get 包名 --purge
sudo apt-get purge 包名
```
### 卸载系统全部不用的包

```bash
sudo apt-get autoremove --purge
```

### 清除全部已卸载的包配置文件

```bash
sudo dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```

