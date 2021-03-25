# Centos7查看开启关闭iptables




## iptables


CentOS 配置防火墙操作实例（启、停、开、闭端口）：

注：防火墙的基本操作命令：
```
查询防火墙状态:
[root@localhost ~]# service iptables status
停止防火墙:
[root@localhost ~]# service iptables stop
启动防火墙:
[root@localhost ~]# service iptables start
重启防火墙:
[root@localhost ~]# service iptables restart
永久关闭防火墙:
[root@localhost ~]# chkconfig iptables off
永久关闭后启用:
[root@localhost ~]# chkconfig iptables on
```

