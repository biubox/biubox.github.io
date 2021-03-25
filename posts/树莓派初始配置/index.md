# 树莓派初始配置




## 配置Wifi接入

`wpa_supplicant.conf`是linux无线网络管理软件`wpa_supplicant`的配置文件，该文件记录了无线网络的配置情况。

    vim /etc/wpa_supplicant/wpa_supplicant.conf

其中ssid为wifi名称，psk为wifi密码

添加 `network` 节点，添加后文件内容如下：

```shell
country=GB
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
##在此处之后添加
network={
        ssid="Honor 10"
        psk="zyj123#.."
        priority=5
      }
network={
        ssid="company"
        psk="companyPwd"
        priority=4
      } 
```

***其中priority为优先级，值越大，优先级越高。***

---
## 静态IP设置(Wifi和有线)

在 interfaces 文件的开头注释里告诉我们了要修改静态IP地址，需要修改的是 /etc/dhcpcd.conf 也就是 DHCP 的配置文件。

查看官方文档 man dhcpcd.conf 可知，需要配置 static IP 的话，只需修改以下参数：


    vi /etc/dhcpcd.conf
```sh
# 使用 vi 编辑文件，增加下列配置项
# 指定接口 eth0　或者 wlan0
interface eth0
# 指定静态IP，/24表示子网掩码为 255.255.255.0
static ip_address=192.168.1.20/24
# 路由器/网关IP地址
static routers=192.168.1.1
# 手动自定义DNS服务器
static domain_name_servers=192.168.1.1 114.114.114.114
# 修改完成后，按esc键后输入 :wq 保存。重启树莓派就生效了
```
---
## 查看CPU温度

    sudo cat/sys/class/thermal/thermal_zone0/temp

---
## HDMI热拔插/增强设置

树莓派有两个视频输出源（HDMI、模拟复合视频）。从原理上，HDMI口可以检测显示设备的有无及分辨率，模拟视频只能单纯输出，对目标设备没有任何检测（可以理解为开环）。

***不能双头同时输出，开机时的策略是有HDMI则HDMI优先，无则退化到模拟视频。***

可以通过修改config.txt来改动。设置`hdmi_force_hotplug=1`可以强制系统认为HDMI接口有设备插入。

找到`#hdmi_force_hotplug=1`这句话，把前面的`#`注释符号去掉，启用HDMI热插拔功能。
找到`#config_hdmi_boost=4`这句话，把前面的`#`注释符号去掉，启用加强HDMI信号。

注意强制HDMI输出时，树莓派不知道对面的显示设备是什么。

---
## 强制分辨率显示
所以你可能有必要用`hdmi_group`和`hdmi_mode`选项手动指定显示分辨率

找到`#hdmi_group=1`这句话，把前面的`#`注释符号去掉,强行指定显示器类型：



***1是连接老式电视，2代表连接新电视.***

配置 `hdmi_safe = 1`，可以显示，可是屏幕分辨率一直只有640 * 480。
hdmi_safe = 1强制使分辨率为640 * 480。

```sh
/opt/vc/bin/tvservice -m CEA  ＃CEA老屏幕，hdmi_group = 1
/opt/vc/bin/tvservice -m DMT  ＃新屏幕  hdmi_group = 2
```
查看屏幕支持的分辨率

![img](https://cdn.jsdelivr.net/gh/biubox/cdn@data/img/2019-06-29-19-18-35.png)

`/boot/config.txt` 里面设置如下

	hdmi_group=2  #设置为新式电视模式
	hdmi_mode=27  #选择合适的分辨率 "mode 码"

---
## 强制竖屏

	display_rotate=1




