# Centos7查看开启关闭firewalld




## Centos7查看开启关闭firewalld

    systemctl stop firewalld.service #停止firewall
    
    systemctl disable firewalld.service #禁止firewall开机启动
    
    firewall-cmd --state #查看默认防火墙状态
    #（关闭后显示notrunning，开启后显示running）

