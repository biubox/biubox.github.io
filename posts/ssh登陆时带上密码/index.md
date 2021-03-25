# SSH登陆时带上密码


## SSH登陆时带上密码

在ssh的同时带上密码，不用手动输入
先安装一个软件包

`yum install -y sshpass`

只需要在ssh命令的前面带上sshpass就可以


`sshpass -p 'your passwd' ssh root@192.168.1.1 systemctl restart nginx`

