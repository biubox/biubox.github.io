# Ubuntu-1804-Gnome3-自定义系统登录背景


## Ubuntu-1804-Gnome3-自定义系统登录背景

>20.04LTS个人测试无效，暂没有找到解决方法

设置文件在`/etc/alternatives/gdm3.css`

找到`#lockDialogGroup` 开始设置他的属性。

**注意备份**

```css
#lockDialogGroup {
  background: #2c001e url(file:///usr/share/backgrounds/loginscreen.jpg);
  height: 100%;
  background-size: contain;
  background-attachment: fixed;
  background-position: 0px 0px;
  background-repeat: repeat; }
```
**注意,请使用和显示器分辨率比例相同的图片**

---
## PS:

图片裁剪软件，又不想装PS的话，可以用一下我自己写的剪切小工具，c#写的(vs2008)

[https://github.com/Sth32/cut-pic-with-2-point](https://github.com/Sth32/cut-pic-with-2-point)

首先，介绍一下我的情况,小笔记本屏幕再带一个外置显示器.

系统开机时自动设置两者分辨率为1920x1080，因此我的解锁的壁纸要为1920x1080的。但是小显示器太小了，这个分辨率看不清，于是在我login后，分辨率被调整为了1600x900，这时候再锁屏，如果固定了壁纸的大小，就会导致壁纸显示不完全，好在这个分辨率和上面的分辨率都是一个比例(16:9)，因此我们让壁纸自适应屏幕的高度，然后自动调整宽度，就可以在两种分辨率下达到完美显示的效果了。

```css
background 						属性，设置壁纸的位置。
height
background-size 
background-attachment: fixed;
background-position: 0px 0px;
background-repeat: repeat;	
```

## 转载于[[Sth32]](https://blog.csdn.net/My__Code/article/details/83988525)
