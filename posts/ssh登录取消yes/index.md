# SSH登录取消yes


## SSH登录取消yes

ssh登录机器的时候，如果这台机器没有使用ssh登录过(严格来说应该是`~/.ssh/known_hosts`文件中没有这台机器的HostKey)

ssh会产生一个提示，询问是否需 要添加这台机器的HostKey，回答yes/no即可，虽然只要不删除`~/.ssh/known_hosts`文件中该机器的HostKey，则这个提示 将不会出现，书写一些自动化脚本的时候，就会成为问题。



---

`vi /etc/ssh/ssh_config`
下面的参数默认为ask，去掉前面的注释，设置为`no`即可。
`StrictHostKeyChecking no`

---



以后ssh将会自动添加HostKey到`~/.ssh/known_hosts`，不会再询问。

默认该项配置是`ask`，所以会询问。

最严格的配置是`yes`，每次必须手动将hostkey添加到`~/.ssh/known_hosts`文件中。

