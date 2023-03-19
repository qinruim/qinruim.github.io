# Pop!_OS系统安装


# Pop!_OS，Windows10双系统安装

笔记本自带Win10，由于电脑配置一般，当多开应用以及需要加载一些大文件是电脑时常出现卡顿，因此开始考虑安装Linux系统。但由于还需保留Win10系统娱乐使用以及以防万一，因此决定安装Win10和Pop!_OS双系统。

其实在此之前已经在朋友的帮助下完成过基于Arch的Manjaro系统的安装，出于对其滚动更新的忧虑，以及软件兼容性的考虑，此次决定安装基于Ubantu的Pop!_OS。

历经各种资料查阅和实际操作，安装途中也踩了一些坑，为了提醒自己，所以记录一下安装过程。

## Pop!_OS简介

1.Pop！_OS是基于Ubuntu的免费开源Linux发行版，有什么问题搜ubuntu也能找到解决方案。

2.具有自定义GNOME桌面。为AMD和Nvidia GPU提供了全面的开箱即用支持。

3.具有很好的自动网格布局。

4。Pop!_OS比Ubuntu和Manjaro GNOME都纯净，预装软件更少。

## 开始安装

### 1.制作启动盘

到[Pop!_OS下载页面](https://pop.system76.com/)下载镜像文件

建议下载LTS版本，根据自己电脑是否有NVIDIA独显选择合适的版本

<div align=center>
    <img src=pop1.png width=70% />
</div>

下载完成后制作启动盘，可以使用rufus、Etcher等软件制作，全凭个人喜好

插入u盘，运行rufus软件，点击选择刚刚下载镜像文件和u盘，点击制作即可。

### 2.在Win10系统下进行磁盘分区

进入磁盘管理，选择你早已准备好的一块空白区域，右键，压缩卷得到一块空白分区（压缩后会显示未分配），具体多大根据你实际情况来，硬盘空间大则多给一点，不够则少给一点，如图所示：

<div align=center>
    <img src=pop2.png width=70% />
</div>

### 3.重启进入BIOS

搜索引擎搜一下自己的电脑怎么进入BIOS，不同品牌的主板有所区别。

进入BIOS之后，找到启动选项，选择USB启动开始安装。

### 4.选择语言等设置

不出意外的话，此时电脑就会载入启动盘的引导系统，按提示选择语言，建议选择英语，以免安装后文件夹默认是中文，影响使用。要使用中文可以在安装完成之后进入系统设置更改语言。

然后选择Custom安装，如图所示：

![](image-20230318010456720.png)

### 5.分区

然后点击左下角modify partitions进入分区界面。

![image-20230318010831686](image-20230318010831686.png)

会看到前面分出来的空白区域，右键选择new或者点击左上角创建新分区

首先分出至少512MB的EFI启动分区，file system选择fat32：

![image-20230318011132141](image-20230318011132141.png)

然后分出swap分区，大小建议跟自己电脑一样内存一样，file system选择linux-swap

然后分出操作系统根目录（/），用户目录（home）大小自己根据实际情况确定，file system都选择ext4

确认后，点击工具栏确认按钮，提交分区计划，完成之后带你接close

### 6.配置各个分区的挂载内容

点击use partition

512M的EFI分区：![image-20230318011821341](image-20230318011821341.png)

swap分区：![image-20230318011836444](image-20230318011836444.png)

root（/）分区：

![image-20230318011900117](image-20230318011900117.png)

用户目录（home）：

![image-20230318011933486](image-20230318011933486.png)

### 7.分配完成后

点击左下角Erase and Install，输入账号密码开始安装

### 8.重启进入Pop!_OS

重启进入Pop!_OS之后，由于Pop_OS!默认不带GRUB，这一点不如Manjaro，需要手动安装GRUB，否则启动电脑时不能选择系统，无法使用Windows10系统

[Pop_OS!的GRUB安装教程]([How to Install grub on POP OS 20.04 – Jacci.Net](https://jacci.net/linux/pop-os/how-to-install-grub-on-pop-os-20-04/))

现在就可以愉快使用Pop!_OS啦！


