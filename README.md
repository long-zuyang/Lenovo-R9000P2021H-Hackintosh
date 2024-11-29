# Lenovo-Legion-R9000P2021H-Hackintosh

> 别名：Lenovo Legion 5 pro

2021款的R9000K、R9000X应该都能用，只不过可能需要微调，有任何问题Issues中反馈即可

使用前请先看完文档，更新时间(24-1129)



## 软件信息

> 我用的是 macOS Monterrey 12 基本没有什么问题，触控板也能正常驱动
>
> 如果要用 macOS 13 的话可能需要自己调一下配置，特别是AirportItlwm.kext，然后13的触控板可能有点问题，有时候会失灵
>
> 镜像用的是黑果小兵大佬的 [macOS Monterey-12.5.1-21G83](https://blog.daliansky.net/macOS-Monterey-12.5.1-21G83-Release-version-with-OC-0.8.4-CLOVER-5148-and-FirPE-original-image.html)



> ***macOS14暂时没有更新计划，14-14.3和14.4用的驱动都不一样，等驱动稳定点再看***



## 硬件信息

| 硬件名称 | 型号                               | 可用情况                                 |
| -------- | ---------------------------------- | ---------------------------------------- |
| CPU      | Ryzen7 R7 5800H                    | 可用                                     |
| 独立显卡 | NVIDIA RTX 3060 Laptop             | 无法驱动                                 |
| 核显     | AMD Radeon Vega 8                  | 可用（Bios调4GB显存，如果16G内存只有2G） |
| 内存     | Samsung 32GB 3200MHz DDR4          | 可用（内存基本都没问题）                 |
| 网卡     | Intel(R) Wi-Fi 6E AX210 160MHz     | 可用（原装联发科网卡无法驱动）           |
| 蓝牙     | Intel(R) Wi-Fi 6E AX210 160MHz     | 可用（隔空投送无法使用）                 |
| 硬盘1    | WD Black SN770 1T                  | 可用（加装的）                           |
| 硬盘2    | SKHynix_HFS512GDE9X084N 512G       | 无法驱动（原装海力士的都需要屏蔽）       |
| 键盘     |                                    | 可用                                     |
| 触控板   |                                    | 可用                                     |
| 声卡     | AL287                              | 可用（layout-id=13）                     |
| 屏幕     | 京东方 2560*1600 165HZ(只能用60HZ) | 可用（华星光电可用165HZ）                |
| 麦克风   |                                    | 内置的貌似可用，可以外接USB麦克风        |



## SSDT（必须开启）

| 名称                      | 作用               |
| ------------------------- | ------------------ |
| SSDT-dGPU-Optimus-Off.aml | 禁用独立显卡       |
| SSDT-DISABLE-NVME.aml     | 禁用原厂海力士硬盘 |



## 屏蔽硬盘

先看[这个](https://heipg.cn/tutorial/block-nv-dgpu-or-pm981.html#%E4%BF%AE%E6%94%B9%E9%A2%84%E7%BC%96%E8%AF%91%E7%9A%84-SSDT)

然后可以参考[这里](https://github.com/mocehu/Lenovo-Legion-R9000X2021R-Hackintosh?tab=readme-ov-file#%E7%A1%AC%E7%9B%98%E5%B1%8F%E8%94%BD%E8%AF%B4%E6%98%8E)

如果身边没有Mac电脑可以在 issue 中留言，我可以帮忙编译



## 注意事项

目前EFI适用于macOS Ventura ，如需使用macOS Monterrey请把Backup文件夹内macOS Monterrey文件夹里面的所有驱动文件覆盖到EFI/OC/Kexts中，否则连接WIFI则会引起内核崩溃重启

**提供的文件中没有序列号等信息，请使用OC编辑器自动生成**

本文件默认开启核显，**安装**或者**升级**系统的时候请**关闭驱动（NootedRed.kext）**

**千万记得开启混合模式，否则会无限重启**

**关闭睡眠模式以及屏幕保护模式，把这些都调到永不，否则睡眠会引起系统崩溃**

**安装系统界面可能会是俄语**，我是用翻译安装完后去设置里添加了中文，加了个新账户把原来的俄语账户删了，安装过程就不多赘述了，大家可以百度



## 关于版本更新

<strike>小版本更新（比如13.5更新13.6）**不用关闭任何驱动**，直接下载更新即可</strike>

<strike>大版本更新（比如12更新13）需要**关闭驱动（NootedRed.kext）**，并且大版本无法通过设置进行更新，需要手动烧录到U盘更新</strike>

***NootedRed 作者在八月的一次更新修复了这个问题，无论大小版本更新都无需禁用 NootedRed.kext***



# 发现的问题

Fusion 360 无法打开

Adobe 软件无法使用

chromium 内核的浏览器需要关闭硬件加速

**亮度调整范围0-20%**,可以下个**BetterDisplay**或者使用**电脑快捷键**更方便

**睡眠会系统崩溃**



# 关于使用 chromium 内核的软件花屏的问题

在Nootedred开源仓库的issue中的 [#158](https://github.com/ChefKissInc/NootedRed/issues/158) 解释了这一问题

主要出现问题的是Chrome和Sublime Text4，然后新版的QQ也有可能会出现

导致这个问题的原因是使用 “双源混合” 的 OpenGL 应用程序会导致 NootedRed崩溃

解决办法：把 ANGLE 切换成 OpenGL 然后将 ANGLE 的功能标志切换成disableBlendFuncExtended 即可解决

**可以通过 [GLFriend](https://github.com/ovoME/GLFriend) 项目快速切换，使用详情请进入项目内查看**



# 感谢

[NootedRed](https://github.com/ChefKissInc/NootedRed) 项目让AMD APU用上较完美的黑苹果

[Legion-5-Pro-Hackintosh](https://github.com/JamisonMurphy/Legion-5-Pro-Hackintosh)

[Lenovo-Legion-R9000X2021R-Hackintosh](https://github.com/mocehu/Lenovo-Legion-R9000X2021R-Hackintosh)
