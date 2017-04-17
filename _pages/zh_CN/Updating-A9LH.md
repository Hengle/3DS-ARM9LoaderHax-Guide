---
title: "升级A9LH"
permalink: /updating-a9lh.html
---

### arm9loaderhax最后更新时间：2016年11月3日

arm9loaderhax的安装实际上就是把一些payload文件安装到了你设备NAND芯片的NFIRM分区中。而NAND是焊接在设备主板上的。这些payload文件很少更新，它们存在的目的就是为了运行SD卡上的`arm9loaderhax.bin`文件，而这个文件在本教程中是用来启动Luma3DS的。
{: .notice}

如果你不知道你现在使用的arm9loaderhax是什么版本，请直接按照以下步骤安装最新版。覆盖安装最新版不会有什么影响。
{: .notice--info}

如果你在Luma上启用了PIN，你必须暂时禁用PIN。完成更新后你可以重新启用PIN。
{: .notice--info}

如果你使用的payload不会初始化屏幕（如Bootanim9），你需要将其重命名为`arm9loaderhax_si.bin`，而不是`arm9loaderhax.bin`
{: .notice--info}

data_input的版本是指为了适配不同安装程序版本而修改的`.zip`压缩包版本，*并非*所更新的a9lh（payload文件）本身的版本。这个版本号只在安装阶段有实际意义。
{: .notice--info}

**你需要一个能进行BT下载的软件，如[Deluge](http://dev.deluge-torrent.org/wiki/Download)、[aria2](https://aria2.github.io/)或迅雷，才能下载本节教程中的[磁力链接](http://baike.baidu.com/item/%E7%A3%81%E5%8A%9B%E9%93%BE%E6%8E%A5)。**
{: .notice--info}

本节的操作同时也会更新其它payloads和AES密钥数据库。
{: .notice--success}

#### 你需要

* <i class="fa fa-magnet" aria-hidden="true" title="这个下载链接是磁力链格式的。请使用BT种子客户端进行下载。"></i> - [`aeskeydb.bin`](magnet:?xt=urn:btih:18b3a17f78e2376e05feaa150749d9fd689b25dc&dn=aeskeydb.bin&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)
* <i class="fa fa-magnet" aria-hidden="true" title="这个下载链接是磁力链格式的。请使用BT种子客户端进行下载。"></i> - [`data_input_v4.zip`](magnet:?xt=urn:btih:00f03ff69b5961307303d5e4778a2f65a528bf2d&dn=data%5Finput%5Fv4.zip&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)
* 最新版的[SafeA9LHInstaller](https://github.com/AuroraWright/SafeA9LHInstaller/releases/latest) *(the `.7z` file)*
* 最新版的[arm9loaderhax](https://github.com/AuroraWright/arm9loaderhax/releases/latest) *(the `.7z` file)*
* 最新版的[GodMode9](https://github.com/d0k3/GodMode9/releases/latest)

#### 操作指南

**对于以下所有操作，覆盖你SD卡上任何已有的文件。**
{: .notice--info}

##### 第一部分 - 准备工作

1. 关机
1. 将SD卡取出，插入电脑中
1. 删除SD卡根目录下的`aeskeydb.bin`文件
1. 如果在SD卡的根目录下存在`a9lh`目录，请删除
1. 将下载的`aeskeydb.bin`文件复制到SD卡的`/files9/`目录下
4. 解压缩GodMode9`.zip`压缩包，复制`GodMode9.bin`文件到`/luma/payloads/`目录下
5. 解压缩SafeA9LHInstaller`.zip`压缩包，复制`arm9loaderhax.bin`文件到SD卡`/luma/payloads/`目录下，并将其重命名为`down_safea9lhinstaller.bin`
7. 解压缩data_input`.zip`压缩包，将`a9lh`文件夹复制到SD卡的根目录下
8. 解压缩arm9loaderhax`.7z`压缩包，并复制*解压后的文件*到SD卡的 `\a9lh\` 目录下
9. 将SD卡插回你的机器

##### 第二部分 - Payload更新

1. 按住(Down)键开机，运行SafeA9LHInstaller
1. 按(Select)键更新arm9loaderhax
1. 关机
1. 将SD卡插入电脑
1. 删除SD卡根目录下的 `a9lh` 目录
1. 将`down_safea9lhinstaller.bin`从`/luma/payloads/`目录中删除
1. 将SD卡插回你的机器

##### 第三部分 - 配置Luma3DS

1. 按住(Select)键开机，进入Luma3DS的配置菜单
2. 通过方向键和(A)键来启用以下设置：
  + **"Autoboot SysNAND"**
  + **"Use SysNAND FIRM if booting with R"**
  + **"Show NAND or user string in System Settings"**
3. 如果你的设备是**新3DS**，你*还*可以启用如下设置：
  + **"New 3DS CPU"选项，请移动光标到"Clock+L2(x)"**
    + 这将提升许多游戏的帧率，但可能会造成某些游戏的不稳定
    + 如果有部分游戏不能正常运行，关闭这个选项并重试
4. 按下(Start)键保存设置并重启

##### 第四部分 - CTRNAND Luma3DS

1. 按住(Start)键重启，进入Luma3DS启动器菜单
1. 按(A)键进入GodMode9
1. 进入`SDCARD`
1. 选中`arm9loaderhax.bin`文件，按(Y)键复制
1. 按(B)键返回到主菜单
1. 进入`SYSNAND CTRNAND`
1. 按(Y)键粘贴`arm9loaderhax.bin`文件
1. 选择"Copy path(s)"（复制路径）
  + 如果出现提示，覆盖任何已有的`arm9loaderhax.bin`文件
1. 按(A)键解锁SysNAND (lvl1)写保护，然后按照提示输入按键组合
1. 按(B)键返回到主菜单
1. 按住(R)键的同时按(B)键，弹出SD卡
1. 将SD卡从机器中取出
1. 按(Start)键，在没有SD卡的情况下重启
  + 在没有SD卡的情况下至少开启一次你的机器，可以使你配置基于CTRNAND的Luma3DS
1. 使用方向键和(A)键来启用以下设置：
  + **"Show NAND or user string in System Settings"**
1. 将SD卡插回3DS
1. 按下(Start)键保存设置并重启
