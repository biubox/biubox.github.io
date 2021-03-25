# Linux启用SSH密钥登录




## Linux启用SSH密钥登录

在某些时候，使用密码作为登录服务器的认证方式是不太安全的，为避免密码被暴力破解，许多时候可以采用ssh密钥登录服务器，这里以CentOS为例。

### 第一步

　　生成秘钥对:

* **方法一**

在服务器上利用ssh-keygen生成:
输入:

    ssh-keygen -t rsa
一路enter跳过(当然你也可以自己定义，不过没必要);

会在`/root/.ssh`下生成公钥(id_rsa.pub)私钥(id_rsa);

（公钥是用于服务器端，私钥是用于客户端） 然后将私钥下载至电脑上(登录时会用到)。

* **方法二**

利用远程工具(如Xshell)生成
这里以Xshell为例，点击”工具-新建用户密钥生成向导”全部默认;

下一步，提示输入密钥加密的密码，这里可以为空;

下一步，将公钥保存为文件，命名为id_rsa.pub;

上传到服务器`/root/.ssh`下。

### 第二步
　　修改`/etc/ssh/sshd_config`如下部分:
```
RSAAuthentication yes 开启RSA验证
PubkeyAuthentication yes 是否使用公钥验证
AuthorizedKeysFile .ssh/authorized_keys 公钥的保存位置
PasswordAuthentication no 禁止使用密码验证登录
```
这里最好是禁止使用密码验证登录，否则用密钥就没多大意义了。
更改后保存。

### 第三步
　　进入到密钥保存的目录：
```
cd /root/.ssh
新建密钥验证文件”authorized_keys”，并将公钥输出重定向覆盖密钥验证文件:

touch authorized_keys  
cat id_rsa.pub >> authorized_keys   这里建议使用追加而不是覆盖
修改authorized_keys文件权限为600
chmod  600 /root/.ssh/authorized_keys
```
### 第四步
　　重启ssh服务
```
#CentOS 7之前的版本请执行:  
service sshd restart
#CentOS 7请执行:  
systemctl restart sshd.service
```
接下来就能够通过密钥登录服务器了:
在打开连接的时候会提示导入用户密钥，选择之前保存的私钥文件”id_rsa”即可。


**如何在Linux系统中用密钥方式连接其他的远程Linux主机呢？**

    ssh -i ~/.ssh/id_rsa root@192.168.1.1 -p 22

