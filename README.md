# linux-fonts-from-apple_style_fonts

## 方案

**仿mac os的字体方案，为了获得更加和谐的字体显示。**
- 中文字体: 苹方字体
- 英文字体： Inter 
- 等宽字体： maple font mono
- emoji： apple color emoji

不建议使用苹果的SF Pro作为西文字体, 因为在部分老旧的网站上(如phoronix)表现不理想，西文的排布过于紧凑。
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
下载仓库的`fonts.conf`,把文件移动到`/home/wuxuming/.config/fontconfig/`,然后注销当前登陆或重启，即可享受字体。


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




