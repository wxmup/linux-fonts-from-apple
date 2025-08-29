# 获得类似 mac os 的字体体验

不喜欢linux默认使用的中文字体（Noto fons CJK / Souce Hans CJK）和西文字体（noto fonts），个人更喜欢修长的字体。
苹果的字体刚好符合我的要求，故有以下方案。



# 方案

- 中文字体: 苹方字体
- 英文字体： Inter Variable
- 等宽字体： Maple Mono NF CN
- emoji： Apple Color Emoji

**平方字体和苹果emoji不必多说。Inter风格类似于SF Pro，而且支持可变字体。Maple字体有着圆润修长的字形和连字，内嵌等宽中文字体和Nerd图标，可读性很强。**

> 不用SF Pro，因为SF Pro的小字体字体间隔会很奇怪。非要用的话可以试试aur上打了mac补丁的 [freetype](https://aur.archlinux.org/packages/freetype2-macos) 。



# 效果

### 中文字体和英文字体混搭效果

<img width="1879" height="1036" alt="图片" src="https://github.com/user-attachments/assets/51f702f1-25ba-4714-b1ff-4fce5cb8d23f" />

### 等宽

<img width="2480" height="1482" alt="图片" src="https://github.com/user-attachments/assets/67c8c018-ed01-44ed-b5c3-a47815fc48d5" />

### emoji

<img width="806" height="658" alt="图片" src="https://github.com/user-attachments/assets/65569daa-56b9-4327-bc11-57d4344f4614" />



# 用法

> 非arch系可以手动下载字体然后使用gnome字体管理器手动安装。谁叫你不用arch呢。就得这么麻烦。

对于arch, 请确保你已安装`yay`或`paru`：

首先，输入命令(如使用`paru`,替换'yay'即可)：
```
sudo pacman -S inter-font
yay -S otf-apple-pingfang ttf-apple-emoji ttf-maplemono-nf-unhinted
```

最后，把文件放到`~/.config/fontconfig/`里去，重启/注销登陆后**字体配置会自动生效**。



# 字体优先级问题与解决方案

是的。你可能会发现某些网站会仍然会优先使用noto sans,而不是inter. 有些网站优先使用noto sans mono,而不是maple.

你可以这样关掉firefox的这个设置，让网站使用系统指定的字体，但这样做并不完美，极有可能遇到网站字体显示的兼容性问题，因为有些网站字体安排的乱七八糟的。
<img width="1428" height="1154" alt="图片" src="https://github.com/user-attachments/assets/8e90d197-4ffb-4d1e-b99a-4eb7d3540f6c" />

你也可以直接修改系统文件，手动编排字体之间的优先级，这样做：
``
sudo nano /etc/fonts/conf.d/60-latin.conf
``

然后在sans-serif标签和monospace标签，手动添加优先级最高的字体到第一行。如图：
<img width="1680" height="1214" alt="图片" src="https://github.com/user-attachments/assets/d39bda4a-226e-4dec-bfd0-a5110ce34ca4" />
<img width="1680" height="1214" alt="图片" src="https://github.com/user-attachments/assets/328b7ab0-0c57-41c0-af3e-f1da39a5df0e" />

至此，理论上在大部分网站的字体显示都会达到预期。



# fonts.conf说明

arch linux不必特意添加渲染设置，因为字体渲染引擎已经默认启用如下的渲染设置(字体微调)：
- 抗锯齿
- BCI（字节码解释器）
- 微调风格-hintslight
- 次像素排列（RGBA）
- LCD滤镜：lcddefault

可能4k屏需要关闭字体微调, 以获得更好的字体显示效果? 因为ppi大于300的屏幕, 字体无需微调就会自动对齐.



# fonts.conf定制

fonts.conf上已经定义好了各种类型的字体，并且有注释, 按需修改即可:
- 无衬线字体
- 衬线字体
- 等宽字体

对于无衬线字体和衬线字体的设置,排在首位得是**英文字体**,第二个才是**中文字体**.这样才能确保只有在需要显示中文的情况下才使用中文字体.



# 检查fonts.conf是否有语法错误

1. 直接检查:
```
xmllint --noout ~/.config/fontconfig/fonts.conf
```

2. `重新生成字体缓存` 也能自动检查语法错误:
```
fc-cache -fv
```

**不管哪种方法, 无错误输出则语法正确.**




