# Centos7更改主机名




## 在CentOS7中，有三种定义的主机名:

---
***静态的（Static hostname）***
“静态”主机名也称为内核主机名，是系统在启动时从/etc/hostname自动初始化的主机名。

***瞬态的（Tansient hostname）***
“瞬态”主机名是在系统运行时临时分配的主机名，例如，通过DHCP或mDNS服务器分配。

***灵活的（Pretty hostname）***
“灵活”主机名也有人叫做“别名”主机名。
“灵活”主机名则允许使用自由形式（包括特殊/空白字符）的主机名，以展示给终端用户

***“静态”主机名和“瞬态”主机名都遵从作为互联网域名同样的字符限制规则。***

---

在CentOS 7中，使用`hostnamectl`命令行工具，可以查看或修改与主机名相关的配置。


### 查看主机名:

    //查看一下当前主机名的情况
    hostnamectl   
    
    //查看全部三种主机名
    hostnamectl status
    
    //只查看静态、瞬态或灵活主机名，分别使用--static，--transient或--pretty选项
    # hostnamectl --static
    
    # hostnamectl --transient
    
    # hostnamectl --pretty
    
    //瞬态的（Tansient hostname）
    hostname
    
    //查看主机名配置文件，（静态）（Static hostname）
    cat /etc/hostname

### 查看当前Linux操作系统相关信息 （内核版本号、硬件架构、主机名称和操作系统类型等）:

    uname -a			//查看到的是瞬态的（Tansient hostname）
    cat /etc/redhat-release		//查看操作系统环境


### 修改主机名:

* 临时有效

```sh
    hostname myname	//只能临时修改的主机名，当重启机器后，主机名称又变回来了。
```

* 永久生效

(修改配置文件/etc/hostname来实现主机名的修改)
```
vim /etc/hostname
hostname  myname
```
(命令行)

//永久性的修改主机名称，重启后能保持修改后的。
hostnamectl set-hostname xxx
    
//删除hostname
hostnamectl set-hostname ""
hostnamectl set-hostname "" --static
hostnamectl set-hostname "" --pretty

* 修改主机名：

```sh
# hostnamectl set-hostname myname
```
在修改静态/瞬态主机名时，任何特殊字符或空白字符会被移除，而提供的参数中的任何大写字母会自动转化为小写。

***一旦修改了静态主机名，`/etc/hostname` 将被自动更新。`/etc/hosts` 不会更新以保存所做的修改，所以每次修改主机名后一定要手动更新/`etc/hosts`，之后再重启CentOS 7。否则系统再启动时会很慢。***


* 手动更新/etc/hosts

```
vim /etc/hosts
#127.0.0.1   localhost localhost.localdomain
127.0.0.1  myname
#::1         localhost localhost.localdomain
::1        myname
```

重启CentOS 7

