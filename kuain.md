![开头](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/illust_68201490_20240129_063008.png)
>已经临近2024年2月份了 Nameless的A14也要来了 所以来一期8系刷nameless的图文教程 其他机型以及其他类原Rom大致通用🥳
---
### **步骤一 下载 ROM、驱动、工具**
你或许需要的工具
1. 大侠阿木的一加工具箱：[大侠阿木](https://optool.daxiaamu.com/optool/)
2. Fastboot、9008、Adb 工具箱
3. Adb、Fastboot 官方工具包 [Platform-Tools](https://wwp.lanzouj.com/iPsDf1mo644h "个人蓝奏盘")
4. Fastboot Enhance 工具：[Fastboot Enhance](https://wwp.lanzouj.com/iBfaX1mo0yah "个人蓝奏盘")（解包工具）
5. 以及如果需要ROOT 那么需要Magisk/[KSU](https://wwgm.lanzouj.com/b04r0zs7c "手机版将浏览器UA改为电脑可下载")/[APatch](https://wwgm.lanzouj.com/b04r0zs8d "手机版将浏览器UA改为电脑可下载")
6. 如果所需救砖包
「[大侠阿木网盘](https://yun.daxiaamu.com/OnePlus_Roms_2/%E4%B8%80%E5%8A%A08%20Pro/)」下载。 
### **步骤二 安装驱动**
用 一加工具箱 安装驱动

以及安装好Fastboot、Adb工具 
>以下教程默认工具环境齐全

### **步骤三 正式开始**
>📌**开始前请注意保证你的底包为你将要刷入类原生 ROM 的底包**

>### 目前 8 / 9 系用户都可以从最新OOS13版本作为底包。所需的固件包含在 ROM 中
##### <center>如果A14底包发生更改我再改图文</center>

#### 第一步 解除BL（bootloader lock）
- 开启开发者模式 在开发者模式中打开OEM解锁以及USB调试
>若氧OS的OEM解锁默认无法开启 提示联系运营商
解决方法 登录Google账号 / 恢复出厂设置

用电脑连接手机后 同意usb调试弹窗
- Win+R 打开运行框，输入 Cmd 并回车进入命令行
- 进入Bootloader
`adb reboot bootloader`
>如果提示不是内部或外部指令
则进入到 platform-tools 目录在地址栏输入cmd并回车打开命令行
或者使用其他adb工具箱

或手动进入（关机状态音量下加电源键）
成功进入后
- 解锁BL
一加8系 
`fastboot oem unlock`
新机型为
`fastboot flashing unlock`
>自行判断

- 进入确定界面
选择`UNLOCK THE BOOTLOADER`
音量键选择 电源键确定

![unlock](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/unlock.jpeg)
然后手机会自己清除数据并重启
**注意备份 注意备份 注意备份**

#### 第二步 准备刷入的文件
- 下载好你需要的类原生ROM包
解压并提出payload.bin

![payload](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/payload.bin.png)
提取payload.bin 中的
（8系含9R） dtbo.img、vbmeta.img、vbmeta_system.img（可不提）、recovery.img、boot.img文件
（9系不含9R） dtbo.img、vendor_boot.img、boot.img
##### 以下教程基于8系制作 9系刷入文件有些不同 （故只附上基础教程）
9系建议参考官方教程或其他教程

<center>8系</center>

- 打开FastbootEnhance
>你可以使用任意解包工具甚至MT管理器提取 教程使用FastbootEnhance工具

打开FastbootEnhance
![FastbootEnhance工具](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/Unpack.png)
- 浏览你解压的ROM包

![unpack](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/Unpack.png)
- 点击分区信息
选择dtbo.img、vbmeta.img、vbmeta_system.img（可不提）、recovery.img、boot.img
- 并依次提取 （提示非完整包就勾选允许非完整包）

![list](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/list.png)
提完类似上图

#### 第三步 使用Adb工具箱刷入文件
>本教程使用platform-tools 你也可以使用其他作者工具箱

- 进入到 platform-tools 目录

![address bar](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/Address%20bar.png)
- 在地址栏输入cmd并回车打开命令行

![cmd](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/cmd.png)
开刷

- 手机开机状态 注意同意usb调试弹窗
输入
`adb reboot bootloader`
进入fastboot模式

1. 刷入boot
`fastboot flash boot "把提取的boot.img文件拖入cmd窗口中"`

![drag](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/drag.png)
类似下图
![command](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/Command.png)
**注意 若你提取的文件路径带有中文 请用英文 " 符号 将路径引起来**
![cn path](https://raw.githubusercontent.com/stupidblank/Markdown-Photos/main/oneplus%20rom/Chinese%20path.png)
2. 刷入vbmeta （解除VAB）若官方提供 则直接刷入官方即可
与刷入boot同理 
`fastboot flash vbmeta "拖入提取的vbmeta.img"`
3. 刷入dtbo
同理
`fastboot flash dtbo "拖入提取的dtbo.img"`
4. 刷入 rec （若官方提供直接刷入官方 nameless官方提供和提取的是一样的）
`fastboot flash recovery "拖入提取的recovery.img"`

>如果你提的img文件位置都在platform-tools 目录，可以直接
```
fastboot flash boot boot.img
fastboot flash vbmeta vbmeta.img
fastboot flash dtbo dtbo.img
fastboot flash recovery recovery.img
```

>你也可以直接将提出的文件复制到platform-tools 目录中，就不用拖入再直接回车
用的其他工具箱自己视情况而定

<center>9系（基础教程）</center>

- 同样刷入提取的文件或官方提供的 刷入方式参考上面内容 **若不在同一目录则需要拖入**
```
fastboot flash dtbo dtbo.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash boot boot.img
```

<center>通用</center>

#### 第四步 进入Recovery模式

以上刷入完成后，现在你的手机还在fastboot模式
- 使用上下音量键选择到recovery mode
电源键确定 进入Rec

#### 第五步 刷入ROM

在Rec中（可电源键选择可触屏）
- 选择 Install update （也有其他Rec叫做Apply Update 这里说nameless的Rec）
- 再选择ADB Sideload

这时手机会显示
`Now send the package you want to apply
to the device with "adb sideload <filename>"...`

- 现在回到电脑 在cmd中输入
`adb sideload "拖入你的类原ROM.zip"`

这里还是如果路径带有中文 需要用"引起来 
>**注意拖入zip文件 不是解压缩后的文件夹**

**接下来 耐心等待刷入（时间以包大小 线材 接口等等而定）**

>通常 你会遇见以下情况
`在47%中止并报告Total xfer: 1.00x`
`failed to read command`
`...`
这些情况都是正常现象

#### 后续工作
安装完成后
- 点击左上角箭头返回到Rec主界面

- 点击高级（Advanced） 选择第三个重启Rec（Reboot to recovery）

- 重启Rec后点击Factory reset 

- 点击 Format data / factory reset进行双清

**（务必记得双清）**
- 点击左上角箭头返回Rec主界面

- 点击Reboot system now进入系统

### 开始体验你的新Rom吧

>如果刷入后无法进入系统 请检查你的底包以及刷入文件是否正确 检查vab是否成功关闭
尝试刷入vbmeta_system
>>#目前Nameless-AOSP_instantnoodlep-13.0-20231121-0644-Official版本无法APatch修补内核

>### <center>如果有什么错误 你告诉我</center>