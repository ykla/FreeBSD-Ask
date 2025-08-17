# 3.9 云服务器安装 FreeBSD（基于腾讯云轻量云）


## 使用 virtio 技术半虚拟化的虚拟机

> **注意**
>
> 以下内容仅供参考，有待测试。如果你测试通过，请告知我们！

根据反馈，在 VMware EXSI 等半虚拟化平台上安装或升级 FreeBSD 会遇到故障（如阿里云 virtio-blk 驱动会出问题），需要在开机时按 **ESC** 键，然后输入 `set kern.maxphys=65536` 回车，再输入 `boot` 即可正常启动。安装好后需要在 `/boot/loader.conf` 加入 `kern.maxphys=65536` 即可避免每次开机重复操作。阿里云升级完成后可能会因为此类问题卡在引导界面，此时需要重启并进 VNC 再进行上述操作。

> **注意**
>
> **对于不再受安全支持的版本如 `9.2`，请参考本文并结合手动安装 FreeBSD 章节操作。**

>**警告**
>
>**安装前请在原有的 Linux 系统上看看自己的 IP 及 netmask，可以用命令 `ip addr` 及 `ip route show` 查看网关信息。因为有的服务器并不使用 DHCP 服务，而需要手动指定 IP。**

## 概述

[腾讯云轻量应用服务器（即腾讯云轻量云）](https://cloud.tencent.com/product/lighthouse) 以及 [阿里云轻量应用服务器](https://www.aliyun.com/product/swas) 等机器都没有 FreeBSD 系统的支持，只能通过特殊的的方法自己暴力安装。

>**警告**
>
>请注意数据安全，以下教程有一定危险性和要求你有一定的动手能力。

## 方案一：使用 grub 引导 mfsBSD ISO

此方案主要面向 GPT 分区表，MBR 或可参见方案二。

```sh
# wget https://mirrors.nju.edu.cn/freebsd/releases/ISO-IMAGES/14.3/FreeBSD-14.3-RELEASE-amd64-bootonly.iso
# mv FreeBSD-14.3-RELEASE-amd64-bootonly.iso /boot/bsd.iso
```

```sh
# grub2-editenv - unset menu_auto_hide
```

按 `c`进入编辑模式“

```sh
linux16 /boot/memdisk
initrd16 (hd0,gpt2)/bsd.iso


set iso=(hd0,gpt2)/bsd.iso
loopback loop $iso
set root=(loop)

chainloader /boot/loader.efi

initrdefi /boot/loader.efi


boot # 输入 boot 后回车即可继续启动
```

#### 参考文献

- [GRUB2 配置文件“grub.cfg”详解（GRUB2 实战手册）](https://www.jinbuguo.com/linux/grub.cfg.html)，作者：金步国。参数解释参见此处，有需要的读者请自行阅读。下同。
- [关于启动时不显示 grub 界面的问题](https://phorum.vbird.org/viewtopic.php?f=2&t=40587)

## 方案二：使用 mfsLinux 再 dd mfsBSD

此方案面向 MBR 分区表，GPT 分区表下一定会报错。

我们先把从 ISO 放在 `/boot/` 目录下，然后重启机器进入 GRUB 的命令行界面（可在倒计时的时候按 `c` 进入编辑模式，然后输入 `boot` 后回车即可继续启动操作系统。

- 下载安装镜像：

```sh
# wget https://mirrors.nju.edu.cn/freebsd/releases/ISO-IMAGES/14.3/FreeBSD-14.3-RELEASE-amd64-bootonly.iso
# mv FreeBSD-14.3-RELEASE-amd64-bootonly.iso /boot/bsd.iso
```

>**技巧**
>
>建议在此处使用服务器的“快照”功能对服务器进行备份，以防以下教程操作失误重来耽误时间。

```sh
ls # 显示磁盘
ls (hd0,msdos1)/ # 显示磁盘 (hd0,msdos1) 下的内容
linux16 /boot/memdisk iso
initrd (hd0,msdos1)/boot/bsd.iso
boot # 输入 boot 后回车即可继续启动
```

>**技巧**
>
>不一定是 **(hd0,msdos1)**，以实际为准，不要一下都删掉了看不出来了。


## 安装 FreeBSD

ssh 连接服务器后，使用 `kldload zfs` 加载 zfs 模块，然后运行 `bsdinstall`，在出现以下图片时，点 `Other` 输入图中的指定镜像版本（地址里有即可，你可以自己改哦）：

示例：如 <https://mirrors.ustc.edu.cn/freebsd/releases/amd64/14.3-RELEASE/> 或 <https://mirrors.nju.edu.cn/freebsd/snapshots/amd64/15.0-CURRENT/>

![腾讯云轻量云及其他服务器安装 FreeBSD](../.gitbook/assets/installBSD1.png)

![腾讯云轻量云及其他服务器安装 FreeBSD](../.gitbook/assets/installBSD2.png)

![腾讯云轻量云及其他服务器安装 FreeBSD](../.gitbook/assets/installBSD3.png)


- 我们还可以手动下载 FreeBSD 的安装文件，以 `MANIFEST` 文件为例：

```sh
# mkdir -p /usr/freebsd-dist # 创建目录
# cd /usr/freebsd-dist # 切换目录
# fetch http://ftp.freebsd.org/pub/FreeBSD/releases/amd64/14.3-RELEASE/MANIFEST # 下载所需文件
```

## 故障排除与未竟事宜

### 为何不能直接 dd？（错误示范，仅供说明，请勿执行）

直接 dd 会报错如图：

![](../.gitbook/assets/1.png)

### lvm

如果服务器使用了 LVM，则需要把镜像放到 `/boot` 里面，要不然无法识别。

## 参考资料

- [Remote Installation of the FreeBSD Operating System Without a Remote Console](https://docs.freebsd.org/en/articles/remote-install/)

