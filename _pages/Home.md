---
layout: splash
permalink: /
title: "教程首页"
header:
  overlay_color: "#5e616c"
  overlay_image: images/home-page-feature.jpg
  overlay_filter: 0.5
  cta_label: "开始教程"
  cta_url: "/get-started"
  caption:
excerpt: '利用arm9loaderhax实现3DS运行自制固件的完整教程。<br />'
lang: zh_CN
ref: home
---

原版教程已更新到使用boot9strap，点击进入[新boot9strap教程](https://3dshax.cn)。如果你已经安装了arm9loaderhax，想升级到boot9strap，点击进入[升级到B9S教程](https://3dshax.cn/updating-to-boot9strap)。
{: .notice--info}

{% capture notice-home %}
**本教程仅适用于零售版的3DS (自行购买，而不是来自Nintendo Developer Program) ！
如果你的3DS属于开发机 ("PANDA"或"SNAKE")，请参见[devGuide](https://dev.3ds.guide)**
{% endcapture %}

<div class="notice--danger">{{ notice-home | markdownify }}</div>

**本教程中有大量下载链接是[磁力链](https://zh.wikipedia.org/zh-hans/%E7%A3%81%E5%8A%9B%E9%93%BE%E6%8E%A5)格式。你需要一个能进行BT下载的软件，如[Deluge](http://dev.deluge-torrent.org/wiki/Download)、[aria2](https://aria2.github.io/)或迅雷。**
{: .notice--info}

**请先阅读完本介绍页面后，再开始操作。**
{: .notice--warning}

点击[这里](https://3ds.guide/)阅读Plailect的英文教程。
{: .notice--info}

[Jixun Moe](https://github.com/JixunMoe)写了一个很棒的js脚本，可以实现教程预加载和英文教程直链。喜欢的朋友可以到[这里](https://greasyfork.org/zh-CN/scripts/26309-3ds-guide-streamlined)下载启用。
{: .notice--info}

## 什么是自制程序？

[**Homebrew（自制程序）**](https://en.wikipedia.org/wiki/List_of_homebrew_video_games) 通常指未经任天堂授权的软件。 它能让你运行自制游戏，使用像修改和备份存档的工具，以及运行模拟器。

大多数情况下，只需使用[Nintendo 3DS Sound（任天堂3DS声音）](homebrew-launcher-(soundhax))就能在你的机器上运行自制程序，且完全免费（如果你的系统版本在11.4.0及以上，目前仅能停留在运行自制程序阶段）。部分付费游戏和系统自带的浏览器中也有一些漏洞，可以使你运行自制程序。

## 什么是自制系统？

**Custom Firmware（自制系统）** ("CFW") 可以使你进行自制程序无法轻易做到的更高级的破解。 例如，签名补丁可以使你安装未签名的程序，并让它们出现在桌面中。

CFW可以很容易地在系统版本11.3.0及以下的设备上安装。

## 本教程将安装什么？

本教程的最终目的，是将一个未经修改过的装有原生系统的3DS
变成一个基于arm9loaderhax的自制系统。 在某些版本的机器上，本教程会使用自制程序作为手段，但是安装自制系统才是最终目的。

Arm9loaderhax是一种最新和最好的引导自制系统的方法，只需启动时几毫秒的时间，就能让你获得几乎全部系统权限，类似于Wii上面BootMii的作用。

相比于其它运行自制系统的方法，arm9loaderhax有许多优势。因此推荐使用本教程，而不是其它依赖已过时软件（例如menuhax或rxTools）的教程。

## 我可以在自制系统上做什么？

+ 跨区运行所有游戏卡带和eShop游戏
+ 使用玩家自制的[主题](https://3dsthem.es/)和[卡贴](https://badges.3dsthem.es/)来自定义你的桌面。
+ 对你已有的游戏进行"ROM hacks"
+ 进行游戏录像和程序截屏
+ [备份、修改和恢复](https://gbatemp.net/threads/release-jks-savemanager-homebrew-cia-save-manager.413143/)游戏存档
+ 使用模拟器（如RetroArch或其它独立模拟器）运行老系统的游戏 （在任天堂新3DS上效果最佳）
+ 安装自制程序，并让它们在你的桌面上出现
+ 将游戏卡带的内容导出为可安装的格式，从而可以无需卡带运行游戏
+ 仅限新3DS：使用NTR CFW将游戏录像在线输出到PC
+ 运行许多以前被禁的或者无法在任天堂3DS上使用的NDS卡带
+ 安全地升级到最新版本的系统，无需担心升级后无法访问自制程序

## 在开始之前我需要知道什么？

+ **在开始之前，你要知道破解3DS的风险：每次你修改系统的时候，都有可能会使你的3DS不可恢复的变砖。 这种情况很少见，但是仍然存在这样的可能性，所以请确保你完全按照本教程的指导进行操作。**
+ 如果你之前破解过你的3DS并安装了EmuNAND，想将原EmuNAND中的内容迁移到新的SysNAND CFW中，请依操作进行，并在[安装arm9loaderhax](installing-arm9loaderhax)这一步中依照提示还原的你EmuNAND。
+ 本教程适用于所有区域的新3DS，老3DS和2DS，固件版本在11.3.0及以下*（除神游/台版机）*。
+ 如果一切顺利，在安装完自制系统后你不会丢失任何数据（包括游戏、NNID、存档等）。
+ **确保你的设备在操作过程中接上电源线充电，防止因意外关机而造成数据丢失或机器损坏！**
+ 你的SD卡的分区表格式必须是[MBR，而不是GPT](http://www.howtogeek.com/245610/)(机器自带的SD卡的分区表格式默认是MBR)。
+ 如果你需要格式化一张新的SD卡，可以使用[`guiformat`](http://www.ridgecrop.demon.co.uk/index.htm?guiformat.htm)，并将Allocation Unit Size设置为32K。
+ 2DS所需的软件和老3DS一样，因而任何适用于老3DS的步骤也同样适用于2DS。
