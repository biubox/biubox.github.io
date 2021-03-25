# Mitools准备和安装


## 前言

1. 本人严重讨厌通知栏广告，权限滥用。
2. 每次系统更新看见有想用的功能了很是头疼，更新后部分软件重新预装。单个卸载删除太麻烦。
3. 部分应用临时用不上，批量冻结。
4. 登录过的WiFi给忘了密码，扫码什么的太麻烦。
5. 需要设置Hosts,禁广告。
6. 批量删除根目录广告、空文件夹。

***纯脚本,需开启Root.自定义食用效果更佳***


---
### 前期准备(必须)：

> 部分功能个人定义的，需要用到BusyBox

* 开发版用户-设置-授权管理-Root权限管理，开启Root权限。(每次升级完同样步骤)

* 手机开启USB调试，电脑端运行ADB(解锁system分区)

```
adb root
adb disable-verity
adb reboot now

```

* 点击链接**下载源码** 文件，解压后将 **su** 文件夹 **放在内存根目录** 。

{{< download su.zip "https://cdn.jsdelivr.net/gh/biubox/cdn@data/download/su.zip" >}}

---
### 使用手机终端控制台:

```
su

cp /sdcard/su/tool.sh /data/

chmod +x /data/tool.sh

```

至此，工具安装完成。

以后每次输入

`/data/tool.sh`

即可进入工具(**可添加为代码片段或者短语，使用更方便**)

## 基本目录解析

![](https://cdn.jsdelivr.net/gh/biubox/cdn@data/img/Screenshot_2019-06-02-19-11-38-525.png)


|文件名称|说明|
|---|---|
|all-app.list|读取系统安装的所有包|
|ban-app.list|需要禁用的包名|
|remove.list|需要卸载的包名|
|del-dir.list|需要批量清理的文件夹名|
|hosts|自定义Hosts文件，我提供的里面禁止了部分广告|
|wifi.pw|自动导出的WiFi密码|
|tool.sh|主脚本|


***切记运行前注意查看上面的配置文件，避免误删！！！***


(里面有的数据是我卸载的包名)

## 脚本使用

在模拟终端里面**su**使用Root权限。

运行
`/data/tool.sh`

根据**数字选择需要**的功能即可。
![](https://cdn.jsdelivr.net/gh/biubox/cdn@data/img/IMG_20190602_191231.jpg)

***切记运行前注意修改上面的配置文件！！！***
