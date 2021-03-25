# Tree命令详解




## 例如:
```sh
tree -C -L 3 -T "文件下载列表" -H "" -I "*.html|img|en-US|icons" --charset=utf8 -o index.html
tree -C -L 3 -D -h --dirsfirst -F -T "文件下载列表" -H "" -I "*.html|*.sh" --charset=utf8 -o index.html
```


## 详解:

<!--more-->
```bash
$ tree --help
usage: tree [-adfghilnpqrstuvxACDFNS] [-H baseHREF] [-T title ] [-L level [-R]]
        [-P pattern] [-I pattern] [-o filename] [--version] [--help] [--inodes]
        [--device] [--noreport] [--nolinks] [--dirsfirst] [--charset charset]
        [--filelimit #] [<directory list>]
  -a            All files are listed(列出所有文件).
  -d            List directories only(只列出目录).
  -l            Follow symbolic links like directories.(遵循象目录这样的符号链接)
  -f            Print the full path prefix for each file(打印每个文件的完整路径前缀).
  -i            Don't print indentation lines()不要打印压痕线.
  -q            Print non-printable characters as '?'.(将不可打印字符打印为'?'。)
  -N            Print non-printable characters as is.(按原样打印不可打印字符)
  -p            Print the protections for each file.(打印每个文件的保护)
  -u            Displays file owner or UID number(显示文件所有者或UID号).
  -g            Displays file group owner or GID number.(显示文件组所有者或GID编号)
  -s            Print the size in bytes of each file.(打印每个文件的字节大小)
  -h            Print the size in a more human readable way.(以更容易被人阅读的方式打印尺寸)
  -D            Print the date of last modification.(打印上次修改的日期)
  -F            Appends '/', '=', '*', or '|' as per ls -F.(根据ls -F添加'/'、'='、'*'或'|'。)
  -v            Sort files alphanumerically by version.(按版本对文件进行字母数字排序)
  -r            Sort files in reverse alphanumeric order.(按字母数字倒序排列文件。)
  -t            Sort files by last modification time.(按上次修改时间排序文件)
  -x            Stay on current filesystem only.(只保留当前文件系统)
  -L level      Descend only level directories deep.(只向下深入到级别目录)
  -A            Print ANSI lines graphic indentation lines.(打印ANSI线图形压痕线)
  -S            Print with ASCII graphics indentation lines.(用ASCII图形缩进行打印)
  -n            Turn colorization off always (-C overrides).(始终关闭着色(-C覆盖))
  -C            Turn colorization on always.(始终打开彩色化)
  -P pattern    List only those files that match the pattern given.(只列出与给定模式匹配的文件)
  -I pattern    Do not list files that match the given pattern.(不要列出与给定模式匹配的文件)
  -H baseHREF   Prints out HTML format with baseHREF as top directory.(打印出以baseHREF作为顶部目录的HTML格式)
  -T string     Replace the default HTML title and H1 header with string.(用字符串替换默认的HTML标题和H1标题)
  -R            Rerun tree when max dir level reached.(当达到最大dir级别时重新运行树)
  -o file       Output to file instead of stdout.(输出到文件而不是stdout。)
  --inodes      Print inode number of each file.(打印每个文件的inode编号)
  --device      Print device ID number to which each file belongs.(打印每个文件所属的设备ID号)
  --noreport    Turn off file/directory count at end of tree listing.(在树列表末尾关闭文件/目录计数)
  --nolinks     Turn off hyperlinks in HTML output(关闭HTML输出中的超链接).
  --dirsfirst   List directories before files.(在文件之前列出目录)
  --charset X   Use charset X for HTML and indentation line output.(使用charset X作为HTML和缩进行输出)
  --filelimit # Do not descend dirs with more than # files in them.(不要下载包含超过#文件的dirs)
```


