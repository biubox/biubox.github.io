# Linux系统主机分辨率调节/投屏/双屏


## Linux系统主机分辨率调节/投屏/双屏

xrandr 指令可以用来改变X环境的桌面大小和屏幕频率 

`xrandr`: 列出目前环境支持的解析度和频率 

`xrandr -q`: 同上 ，当前使用的分辨率会带上 “ * “ 号 

### xrandr和cvt命令添加自定义的分辨率模式

使用xrandr -q命令查看当前支持的分辨率模式: 
例如,需要创建800x750的分辨率模式,步骤如下:

1. 使用cvt命令创建新的分辨率:

`cvt 800 750`

2. 使用xrandr -newmode modeline信息(cvt命令产生的结果) 创建新的mode:

`xrandr --newmode "800X750_60.00" 48.50 800 840 920 1040 750 753 763 779 -hsync +vsync`

3. xrandr -addmode 设备名 mode 来为设备添加新的mode:

`xrandr -addmode VGA-1 800X750_60.00`

4. 使用xrandr -out 设备名 -mode mode 来使用新的分辨率模式

`xrand -out VGA-1 -mode 800X750_60.00`

以上步骤只是**临时添加**了新的分辨率,重启后就会消失,要永久保存,需要将modeline的信息保存到配置文件中.



### 更改分辨率

`xrandr -s 1024x768`   这种方式可以 

`xrandr -s n`  (n: xrandr 列出来的模式对应的数字)  这种方式也是可以的

用法举例：`xrandr -s 1024x768 -r 75`

这样就可以将显示器的分辨率和刷新率立即更改为`1024x768＠75`，**注意`1024x768`中间一定要是`x`不可以是`*`.**

设置分辨率时需要指定设置的output及mode，如将eDP1的分辨率改为1920x1080，命令就是：

```
xrandr --output eDP1 --mode 1920x1080
--output:指定显示器。
--mode:指定一种有效的分辨率。
--rate:指定刷新率。

```

---

电脑的分辨率必须和投影率的分辨率相同，才能正常使用

将笔记本屏慕内容克隆到屏幕

`xrandr --output VGA --same-as LVDS --auto` (LVDS:代表笔记本液晶屏)

### xrandr 命令行切换双屏

常用方式如下，其他的可以自己探索：

* 打开外接显示器(最高分辨率)，与笔记本液晶屏幕显示同样内容（克隆）

`xrandr --output VGA --same-as LVDS --auto`

*  打开外接显示器(分辨率为1024x768)，与笔记本液晶屏幕显示同样内容（克隆）

`xrandr --output VGA --same-as LVDS --mode 1024x768`

* 打开外接显示器(最高分辨率)，设置为右侧扩展屏幕

`xrandr --output VGA --right-of LVDS --auto`

*关闭外接显示器

`xrandr --output VGA --off`

* 打开外接显示器，同时关闭笔记本液晶屏幕（只用外接显示器工作）

`xrandr --output VGA --auto --output LVDS --off`

* 关闭外接显示器，同时打开笔记本液晶屏幕 (只用笔记本液晶屏)

`xrandr --output VGA --off --output LVDS --auto`

