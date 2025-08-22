# linux-fonts-from-apple_style_fonts

linux默认采用的一般是思源黑体(Noto fons CJK / Souce Hans CJK)为中文字体和noto fonts作为西文字体，但是这些字体相对比较胖，个人更喜欢修长的字体。
苹果的字体质量是比较高的，故有以下方案。

## 方案

**仿mac os的字体方案，为了获得更加和谐的字体显示。**
- 中文字体: 苹方字体
- 英文字体： Inter 
- 等宽字体： maple font mono
- emoji： apple color emoji

tips：
> 不建议在linux上使用苹果的SF Pro作为西文字体, 网页显示表现不佳，字体间距很紧凑，非常奇怪。SF Pro Display好一点，但是还是没有Inter的间距协调。
**Inter在各个网站的表现都比较一致。并且Inter的字体风格本来就类似于SF Pro, 和苹方字体搭配很和谐。**


## 效果

### 中文字体

![图片](https://github.com/user-attachments/assets/ebdd119d-469a-4ff9-9d87-f58710be8dcb)

### 西文字体

![图片](https://github.com/user-attachments/assets/693099b7-cfb0-4dd7-b197-3a1bbef4103e)

### 等宽

![图片](https://github.com/user-attachments/assets/247f7ee9-74d6-4dd6-8dea-23a4774796dd)

### emoji

![图片](https://github.com/user-attachments/assets/3050a8da-37b6-47a4-9660-5223b67de0bc)


## 用法

1. 安装字体
2. 移动我写好的`fonts.conf`到文件夹.重启/注销登陆后**字体配置会自动生效**.

### 首先，安装字体(对于arch)：
安装inter：
```
sudo pacman -S inter-font
```

安装苹方字体，苹果emoji，和maple等宽字体：(如使用yay,替换'paru'即可):
```
paru -S otf-apple-pingfang ttf-apple-emoji ttf-maplemono-nf-unhinted
```

如果硬是要sf-pro系列字体(sf-pro,sf-pro-mono):
```
paru -S ttf-mac-fonts
```

> debian,ubuntu系自行进入以下仓库下载字体，然后把字体放到`/usr/share/fonts`里去，等价于上述arch linux的安装操作。


### 最后，移动配置文件，然后注销/重启
下载仓库的`fonts.conf`,把文件移动到`~/.config/fontconfig/`,然后注销当前登陆或重启，即可享受字体。


## 字体优先级问题与解决方案

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



## fonts.conf说明

arch linux不必特意添加渲染设置，因为字体渲染引擎已经默认启用如下的渲染设置(字体微调)：
- 抗锯齿
- BCI（字节码解释器）
- 微调风格-hintslight
- 次像素排列（RGBA）
- LCD滤镜：lcddefault

可能4k屏需要关闭字体微调, 以获得更好的字体显示效果? 因为ppi大于300的屏幕, 字体无需微调就会自动对齐.

### fonts.conf定制

fonts.conf上已经定义好了各种类型的字体，并且有注释, 按需修改即可:
- 无衬线字体
- 衬线字体
- 等宽字体

对于无衬线字体和衬线字体的设置,排在首位得是**英文字体**,第二个才是**中文字体**.这样才能确保只有在需要显示中文的情况下才使用中文字体.

### 检查fonts.conf是否有语法错误

1. 直接检查:
```
xmllint --noout ~/.config/fontconfig/fonts.conf
```

2. `重新生成字体缓存` 也能自动检查语法错误:
```
fc-cache -fv
```

**不管哪种方法, 无错误输出则语法正确.**




