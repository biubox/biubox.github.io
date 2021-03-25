# Git命令使用方法


[toc]

## Git 恢复到上次提交

```bash
git log   #查询到需要恢复的版本

git reset --soft hash1  #--soft 保存本地文件
git reset --hard hash2  #--hard 本地文件也被恢复到上一个版本

git push origin HEAD --force
```

##  Git Add 撤销

撤销操作
```bash
git status 					#先看一下add 中的文件 
git reset HEAD 				#撤销上一次add 
git reset HEAD path/file.name #单独撤销某个文件
```
## Git 更改项目语言分类

在项目目录中创建一个名为 "`.gitattributes`" 的文件，添加以下代码：

```
*.js linguist-language=Java
```

  重新`git push`到 Github 上

---

## Git 强制放弃本地修改（新增、删除文件）

本地修改了一些文件，其中包含修改、新增、删除的，不需要了想要丢弃
`git check -- .`操作只放弃了修改的文件，新增和删除的仍然没有恢复
使用如下命令：
`git checkout . && git clean -df`

可以放弃所有修改、新增、删除文件
```bash
git checkout .  	//放弃本地修改，没有提交的可以回到未修改前版本
git clean  			//是从工作目录中移除没有track的文件
```

通常的参数是

```bash
git clean -df 
	-d 	#表示同时移除目录,
	-f  #表示force,在git的配置文件中, clean.requireForce=true,如果不加-f,clean将会拒绝执行.
```

---



## Git 工具 - 子模块

***项目嵌套子项目（仓库）***

子模块允许你将一个 Git 仓库作为另一个 Git 仓库的子目录。 它能让你将另一个仓库克隆到自己的项目中，同时还保持提交的独立。

### 开始使用子模块

首先将一个**已存在的 Git 仓库**添加为**正在工作的仓库的子模块**。 你可以通过在 `git submodule add` 命令后面加上想要跟踪的项目的相对或绝对 URL 来添加新的子模块。 

在本例中，我们将会添加一个名为 “DbConnector” 的库。

```bash
$ git submodule add https://github.com/chaconinc/DbConnector
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
```

默认情况下，子模块会将子项目放到一个与仓库同名的目录中，如果你想要放到其他地方，那么可以在命令结尾添加一个不同的路径。

运行 `git status`

```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   .gitmodules
	new file:   DbConnector
```

注意产生到新的 `.gitmodules` 文件。 该配置文件保存了项目 **URL **与已经拉取的**本地目录**之间的映射：

```bash
[submodule "DbConnector"]
	path = DbConnector
	url = https://github.com/chaconinc/DbConnector
```

如果有多个子模块，该文件中就会有多条记录。 要重点注意的是，该文件也像 `.gitignore` 文件一样受到版本控制。 它会和该项目的其他部分一同被拉取推送。 这就是克隆该项目的人知道去哪获得子模块的原因。

可以根据自己的需要，通过在本地执行 `git config submodule.DbConnector.url <私有URL>` 来覆盖这个选项的值

`DbConnector` 是工作目录中的一个子目录，但 Git 还是会将它视作一个子模块。当你不在那个目录中时，Git 并不会跟踪它的内容， 而是将它看作子模块仓库中的某个具体的提交。

### 克隆含有子模块的项目

```bash
$ git clone https://github.com/chaconinc/MainProject
Cloning into 'MainProject'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 14 (delta 1), reused 13 (delta 0)
Unpacking objects: 100% (14/14), done.
Checking connectivity... done.
$ cd MainProject
$ ls -la
total 16
drwxr-xr-x   9 schacon  staff  306 Sep 17 15:21 .
drwxr-xr-x   7 schacon  staff  238 Sep 17 15:21 ..
drwxr-xr-x  13 schacon  staff  442 Sep 17 15:21 .git
-rw-r--r--   1 schacon  staff   92 Sep 17 15:21 .gitmodules
drwxr-xr-x   2 schacon  staff   68 Sep 17 15:21 DbConnector
-rw-r--r--   1 schacon  staff  756 Sep 17 15:21 Makefile
drwxr-xr-x   3 schacon  staff  102 Sep 17 15:21 includes
drwxr-xr-x   4 schacon  staff  136 Sep 17 15:21 scripts
drwxr-xr-x   4 schacon  staff  136 Sep 17 15:21 src
$ cd DbConnector/
$ ls
$
```

 `DbConnector` 目录是空的。 

你必须运行两个命令：

`git submodule init` 用来初始化本地配置文件

`git submodule update` 则从该项目中抓取所有数据并检出父项目中列出的合适的提交。

现在 `DbConnector` 子目录是处在和**之前提交时相同的状态**了

> 更简单一点的方式。 如果给 `git clone` 命令传递 `--recurse-submodules` 选项，它就会自动初始化并更新仓库中的每一个子模块， 包括可能存在的嵌套子模块。


#### 单独克隆了模块但忘记添加子模块（注意）
已经克隆了项目但忘记了 `--recurse-submodules`，

那么可以运行 `git submodule update --init` 将 `git submodule init` 和 `git submodule update` 合并成一步。

如果还要初始化、抓取并检出任何嵌套的子模块， 请使用简明的 `git submodule update --init --recursive`。

### 从子模块的远端拉取上游修改
如果你不想在子目录中手动抓取与合并，那么还有种更容易的方式。 运行 `git submodule update --remote`，Git 将会进入子模块然后抓取并更新。
```bash
$ git submodule update --remote DbConnector
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 2), reused 4 (delta 2)
Unpacking objects: 100% (4/4), done.
From https://github.com/chaconinc/DbConnector
   3f19983..d0354fc  master     -> origin/master
Submodule path 'DbConnector': checked out 'd0354fc054692d3906c85c3af05ddce39a1c0644'
```
此命令默认会假定你想要更新并检出子模块仓库的 `master` 分支。

### 从项目远端拉取上游更改

协作者的视角，他自己的 `MainProject` 仓库的本地克隆， 只是执行 `git pull` 获取子模块的新提交的更改还不够：

```bash
$ git pull
From https://github.com/chaconinc/MainProject
   fb9093c..0a24cfc  master     -> origin/master
Fetching submodule DbConnector
From https://github.com/chaconinc/DbConnector
   c3f01dc..c87d55d  stable     -> origin/stable
Updating fb9093c..0a24cfc
Fast-forward
 .gitmodules         | 2 +-
 DbConnector         | 2 +-
 2 files changed, 2 insertions(+), 2 deletions(-)
```
```bash
$ git status
 On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   DbConnector (new commits)

Submodules changed but not updated:

* DbConnector c87d55d...c3f01dc (4):
  < catch non-null terminated lines
  < more robust error handling
  < more efficient db routine
  < better connection routine

no changes added to commit (use "git add" and/or "git commit -a")
```

默认情况下，`git pull` 命令会递归地**抓取子模块的更改**，如上面第一个命令的输出所示。 然而，它**不会在主项目中更新子模块**。

这点可通过 `git status` 命令看到，它会显示子模块“已修改”，且“有新的提交”。 

此外，左边的尖括号（<）指出了新的提交，表示这些提交已在 MainProject 中记录，但尚未在本地的 `DbConnector` 中检出。 

为了完成在主项目的更新，你需要运行 `git submodule update`：

```bash
$ git submodule update --init --recursive
Submodule path 'vendor/plugins/demo': checked out '48679c6302815f6c76f1fe30625d795d9e55fc56'

$ git status
 On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
```







---

## Git基本常用命令如下：

```
　　mkdir：         XX (创建一个空目录 XX指目录名)

　　pwd：          显示当前目录的路径。

　　git init          把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

　　git add XX       把xx文件添加到暂存区去。

　　git commit –m “XX”  提交文件 –m 后面的是注释。

　　git status        查看仓库状态

　　git diff  XX      查看XX文件修改了那些内容

　　git log          查看历史记录

　　git reset  --hard HEAD^ 或者 git reset  --hard HEAD~ 回退到上一个版本

　　(如果想回退到100个版本，使用git reset –hard HEAD~100 )

　　cat XX         查看XX文件内容

　　git reflog       查看历史记录的版本号id

　　git checkout -- XX  把XX文件在工作区的修改全部撤销。

　　git rm XX          删除XX文件

　　git remote add origin https://github.com/username/testgit 关联一个远程库

　　git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

　　git clone https://github.com/username/testgit  从远程库中克隆

　　git checkout –b dev  创建dev分支 并切换到dev分支上

　　git branch  查看当前所有的分支

　　git checkout master 切换回master分支

　　git merge dev    在当前的分支上合并dev分支

　　git branch –d dev 删除dev分支

　　git branch name  创建分支

　　git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作

　　git stash list 查看所有被隐藏的文件列表

　　git stash apply 恢复被隐藏的文件，但是内容不删除

　　git stash drop 删除文件

　　git stash pop 恢复文件的同时 也删除文件

　　git remote 查看远程库的信息

　　git remote –v 查看远程库的详细信息

　　git push origin master  Git会把master分支推送到远程库对应的远程分支上
```

## 文献地址

部分文献摘录于：[git-scm.com](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97)


