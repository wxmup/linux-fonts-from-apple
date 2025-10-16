# 获得类似 mac os 的字体体验

不喜欢linux默认使用的中文字体（Noto fons CJK / Souce Hans CJK）和西文字体（noto fonts），个人更喜欢修长的字体。
苹果的字体刚好符合我的要求，故有以下方案。



# 方案

- 中文字体: 苹方字体
- 英文字体： Inter
- 等宽字体： Maple Mono CN
- emoji： Apple Color Emoji
- icon： Symbols Nerd Font Mono

**平方字体和苹果emoji不必多说。Inter风格类似于SF Pro。Maple字体有着圆润修长的字形和连字，并且使用symbols获得正确的终端icon显示**

> 不用SF Pro，因为SF Pro的小字体字体间隔会很奇怪。非要用的话可以试试aur上打了mac补丁的 [freetype](https://aur.archlinux.org/packages/freetype2-macos) 。



# 效果

### 中文和英文效果

<img width="1600" height="409" alt="图片" src="https://github.com/user-attachments/assets/e719032c-b2b9-462d-876b-f998abb6af92" />


### 等宽展示
<img width="2306" height="1580" alt="图片" src="https://github.com/user-attachments/assets/dadd2bd2-5c89-4ef0-af9b-7ae650f68e2a" />


### emoji

<img width="1370" height="1180" alt="图片" src="https://github.com/user-attachments/assets/8105900c-2a35-4528-b2f9-d1d196db650d" />


### 终端icon图标显示

<img width="2306" height="1580" alt="图片" src="https://github.com/user-attachments/assets/06abdcbd-7653-4975-90ef-b4b597cdb6cf" />

<img width="1848" height="1486" alt="图片" src="https://github.com/user-attachments/assets/450fcc72-fd97-458f-a50f-1b119ee79a1a" />




# 用法

> 非arch系可以手动下载字体然后使用gnome字体管理器手动安装。谁叫你不用arch呢。就得这么麻烦。

对于arch, 请确保你已安装`yay`或`paru`：

首先，输入命令(如使用`paru`,替换'yay'即可)：
```
sudo pacman -S inter-font ttf-nerd-fonts-symbols-mono 
yay -S otf-apple-pingfang ttf-apple-emoji ttf-maplemono-cn-unhinted
```

最后，把文件放到`~/.config/fontconfig/`里去，重启/注销登陆后**字体配置会自动生效**。

> tips: 下载ttf-maplemono-nf-unhinted时，aur会默认下载maple的所有的分支，然后只安装其中的ttf-maplemono-cn-unhinted。无解，介意请使用arch linux cn.



# 字体优先级问题与解决方案

就我的使用场景，新版文件已解决问题，理论上不需要在手动设置。如有问题请提issue.



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




