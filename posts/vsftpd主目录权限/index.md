# vsftpd主目录权限（无法写入,连接失败）解决方法


## vsftpd主目录权限（无法写入,连接失败）
当**限定了用户不能跳出其主目录之后**，使用该用户登录FTP时往往会遇到这个错误：

    500 OOPS: vsftpd: refusing to run with writable root inside chroot ()


这个问题发生在最新的这是由于下面的更新造成的：

***Add stronger checks for the configuration error of running with a writeable root directory inside a chroot(). This may bite people who carelessly turned on chroot_local_user but such is life.***


从2.3.5之后，vsftpd增强了安全检查，如果**用户被限定在了其主目录下，则该用户的主目录不能再具有写权限**了！如果检查发现还有写权限，就会报该错误。

  要修复这个错误，可以用命令

    chmod a-w /home/user #去除用户主目录的写权限，注意把目录替换成你自己的。

  或者你可以在`vsftpd.conf`的配置文件中增加下列两项中的一项：


    allow_writeable_chroot=YES

