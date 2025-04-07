# linux-fonts-from-apple

## 方案

**仿mac os的字体方案，为了获得更加和谐的字体显示。**
- 中文字体: 苹方字体
- 英文字体： Inter 
- 等宽字体： maple font mono
- emoji： apple color emoji

英文字体不用sf pro,因为在部分网站上(如phoronix)表现不理想，西文会过于紧凑。
**inter在各个网站的表现都比较一致。并且inter的字体风格本来就类似于sf pro。**


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

### 首先，安装字体(对于arch)：
安装inter：
```
sudo pacman -S inter-font
```

安装苹方字体，苹果emoji，和maple等宽字体：(如使用yay,替换'paru'即可):
```
paru -S otf-apple-pingfang ttf-apple-emoji ttf-maplemono
```

如果硬是要sf-pro系列字体(sf-pro,sf-pro-mono):
```
paru -S ttf-mac-fonts
```

> debian,ubuntu系自行进入以下仓库下载字体，然后把字体放到`/usr/share/fonts`里去，等价于上述arch linux的安装操作。


### 最后，移动配置文件，然后注销/重启
下载仓库的`fonts.conf`,把文件移动到`/home/wuxuming/.config/fontconfig/`,然后注销当前登陆或重启，即可享受字体。


## fonts.conf说明

不必添加渲染设置，因为你的字体渲染引擎已经默认启用如下的渲染设置：
- 抗锯齿
- BCI（字节码解释器）
- 微调风格-hintslight
- 次像素排列（RGBA）
- LCD滤镜：lcddefault

### fonts.conf定制

fonts.conf上已经定义好了各种类型的字体，按需修改即可:
- 无衬线字体
- 衬线字体
- 等宽字体












