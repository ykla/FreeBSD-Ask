# FreeBSD 从入门到跑路

~~为了拯救即将归档（Archived）的 FreeBSD.....我们决定写一本书。让我们一起，以温柔的心随坚定的信念，为 FreeBSD 的未来添砖加瓦！~~

FreeBSD 是真正自由（Liberal）的操作系统，在这个大流变的世界中仍然坚守 BSD UNIX 哲学——恪守古老的法则，追寻真正的自由。

>**技巧**
>
>视频教程合集见 《[FreeBSD 从入门到跑路 第二版](https://www.bilibili.com/video/BV1Qji2YLEgS)》

## 贡献指南

如果你想让你的教程出现在本书中，你可以这样做：

- 如果你熟悉 GitHub，可以点击电脑端右侧的“编辑此页”，进入项目进行操作。整个项目使用 Markdown 语法 +  Gitbook，简单易上手（具体详见项目 WiKi）；
- 如果以上有困难，你还可以发 PDF、Word 或者 TXT 给我。请将文件发送至电子邮件 `yklaxds@gmail.com`；如果有视频教程，以各大云盘链接为宜。

本书现接受以下内容：

- 一切与 BSD 相关（包括不限于 FreeBSD，OpenBSD，NetBSD）以及各种体系结构的教程。你既可以扩充当前教程，也可以新建一节；
- 下方的 ToDo 列表；
- 你亦可在文学故事章节分享你与 BSD 的故事，你的个人心得体会。

你为什么要这样做？

- **可访问性**：随处可见，无需再到处寻找；
- **可复现性**：任何人都能轻松复现成果，显著提高工作和学习效率；
- **规模化测试**：可以对教程进行系统化测试，找出最优解；
- **社区支持**：社区将持续维护教程的可用性，并定期更新软件和教程版本；
- **节省时间**：当本教程内容愈加丰富，你花在网络索引上的无效时间就会越少；
- **互惠互利**：合并教程践行了开源哲学，惠及着无穷的远方，无数的人们；
- **增强协作**：促进 FreeBSD 在中国乃至亚洲、全世界的发展；
- **便于反馈**：快速迭代教程，并验证每一步骤的正确性与合理性；
- **易于分享**：本项目既支持在线浏览亦支持 PDF 文档导出，宽松的许可证、简单的项目结构允许自由部署。

唯一要注意的是，你的教程会以本项目的开源许可证（BSD）进行发布。

### 意见反馈

由于编写者水平所限，书中缺点和谬误之处自不可免，希望大家随时提出批评意见，以便修正。你可以利用 Github 提交 Issue 或者发邮件至 `yklaxds@gmail.com`。

## 现成的虚拟机镜像体验（本书自制）

具体详情请参见第 2 章节。

```json
14.1  磁力链接  magnet:?xt=urn:btih:496C343387D74457E441CAFA93B302E791F62924

15.0  磁力链接  magnet:?xt=urn:btih:CBD49C71E87BC0B1406710A437E7135EF3D8C155
```
## ToDo

- [ ] 整合现有的上游 FreeBSD 社区文章
- [ ] 重写“第 4.1 节 安装显卡驱动及 Xorg（必看）”，尤其是 N 卡驱动部分，目前是无效的，必须重写
- [ ] `pkg autoremove`（会把整个系统都带走）及 `pkg delete`（破坏依赖）都不是正经的卸载软件及孤包依赖的方法，`pkg-rmleaf` 亦已过时无法使用。需要找到正常合理的卸载软件包的方法。`pkg_rmleaves` 似乎可以
- [X] 补充一些 WinSCP、XShell 的替代工具，避免单一来源
  - [ ] 找到一款我认为能替代二者的工具
- [X] 将全书主观性文字转换为思考题供读者自行思考与判断
- [ ] 更新“第 16.7 节 Samba 服务器”
- [ ] 树莓派 5
  - [ ] 微信
- [ ] Bhyve
  - [ ] `sysutils/bhyvemgr` GUI
  - [ ] Windows 11
  - [ ] ~~Windows XP~~
  - [ ] Ubuntu
  - [ ] FreeBSD
  - [ ] ~~MacOS~~
- [ ] 删除重写部分来源于网络的错误内容
  - [ ] 防火墙
  - [ ] jail
  - [ ] 用户与权限
  - [ ] geom
  - [ ] DTrace
- [ ] 完全面向新手介绍 FreeBSD
  - [ ] 对比 Linux、Windows、MacOS、Android 和 IOS 等常见操作系统
  - [ ] 客观化论证
    - [ ] 删除冗余，精简论证
    - [X] 补充参考文献
    - [ ] 客观陈述不足，面对现实
- [X] 重写第一章，考虑加入硬件常识，整合现有的树莓派章节相关内容
- [ ] 文学故事章节需要重写
  - [ ] 说明真实看法，避免曲解和误导，旨在强调对 Linux 和开源没有恶意
  - [ ] 删除冗余，精简论证
  - [ ] 客观化
    - [ ] 名人名言
    - [ ] 图片
    - [ ] 视频
    - [X] 参考文献
    - [ ] 说明各大 Linux 操作系统的优势
- [ ] 补充一些实验
  - [ ] 我的世界（服务器、客户端）
- [ ] ZFS（可以参考 [Oracle Solaris 管理：ZFS 文件系统](https://docs.oracle.com/cd/E26926_01/html/E25826/index.html)）
  - [ ] ZFS 共享
  - [ ] ZFS 加密
  - [ ] ZFS 调优
  - [ ] ZFS iSCSI
  - [ ] 补充 ZFS 委托管理
  - [ ] 归档快照和根池恢复
  - [ ] ZFS 故障排除
  - [ ] ZFS 克隆
  - [ ] ZFS 与 ACL
  - [ ] ZFS 高级主题
  - [ ] ZFS 池管理
  - [ ] ZFS 与 RAID
- [X] 将小说诗歌杂记等与 FreeBSD 无关内容下线
- [ ] 参照 FreeBSD handbook、鸟哥的 Linux 私房菜服务器篇改写服务器相关章节
  - [ ] BSD 常用网络命令
  - [ ] 链路聚合
  - [ ] IPv6 配置
    - [ ] WiFi
    - [ ] 以太网
  - [ ] DNS
  - [ ] DHCP
  - [ ] 更新：第 17.8 节 PostgreSQL 与 pgAdmin4
  - [ ] NTP
  - [ ] NFS
  - [ ] iSCSI
  - [ ] Postfix
  - [ ] LDAP（OpenLDAP，也许可以参考 [WiKi LDAP/Setup](https://wiki.freebsd.org/LDAP/Setup)）
- [X] NextCloud（最好基于 PostgreSQL）
- [ ] KDE6（注意：**不**应使用 Port x11/kde6：kde6-devel）
  - [ ] 基于 Xorg
  - [ ] 基于 Wayland
- [ ] Wayland
  - [ ] 远程软件
  - [ ] KDE5
  - [ ] Gnome
  - [ ] 经典登录管理器
  - [ ] 窗口管理器
  - [ ] 基础知识
- [ ] FreeBSD 路由器
- [ ] Wine
  - [ ] 填充实质性内容
  - [ ] 64 位 Windows 程序（64 位 Wine？）
- [ ] FreeBSD 安全加固（可参照 [FreeBSD 14 CIS 基准](https://www.cisecurity.org/cis-benchmarks)，[阿里云盘](https://www.alipan.com/s/9Vced5R3Wit)）
  - [ ] 云服务器
  - [ ] 路由器
  - [ ] 小主机
  - [ ] 桌面用户
  - [ ] 虚拟机
  - [ ] 限制端口
  - [ ] 防火墙
- [X] 微信
  - [ ] 微信双开
- [ ] WPS
  - [ ] 解决 fcitx、fcitx5 输入法不能输入的问题
---

- [ ] OpenBSD
  - [ ] KDE5（现在进入桌面黑屏）
  - [ ] QQ？原生可能吗
  - [ ] 微信？原生可能吗
  - [ ] Wine
  - [ ] OpenBSD 调优
  - [ ] OpenBSD 安全加固
  - [ ] 网络
    - [ ] DNS
    - [ ] FTP
    - [ ] NTP
    - [ ] DHCP
    - [ ] 各式代理
    - [ ] 邮件服务器
    - [ ] PF 等防火墙
    - [ ] IPv6
    - [ ] 常用网络命令
  - [ ] OpenBSD 路由器（可参考 [OpenBSD 路由器指南](https://translated-articles.bsdcn.org/2023-nian-9-yue/openbsd-router-guide)）
    - [ ] WiFi
    - [ ] 链路聚合
    - [ ] 路由表
    - [ ] 默认路由
  - [ ] OpenBSD 基础知识
    - [ ] 版本概况
    - [ ] 开发宗旨与项目目标
    - [ ] 性能参数
    - [ ] 注意事项
    - [ ] 跟踪新版本
    - [ ] pkgsrc
  - [ ] 嵌入式

---

- [ ] NetBSD
  - [ ] NetBSD 调优
  - [ ] 桌面
    - [ ] 火狐浏览器
    - [ ] Chromium
    - [ ] KDE 4（现在进入桌面黑屏）
    - [ ] QQ
    - [ ] 微信
    - [ ] Wine
  - [ ] 树莓派 4 & 5
  - [ ] NetBSD 安全加固
  - [ ] NetBSD 基础知识
    - [ ] 版本概况
    - [ ] 开发宗旨与项目目标
    - [ ] 注意事项
    - [ ] 跟踪新版本
    - [ ] pkgsrc
  - [ ] 嵌入式  
  - [ ] 网络
    - [ ] DNS
    - [ ] FTP
    - [ ] NTP
    - [ ] DHCP
    - [ ] 各式代理
    - [ ] 邮件服务器
    - [ ] PF 等防火墙
    - [ ] IPv6
    - [ ] 常用网络命令
  - [ ] NetBSD 路由器
    - [ ] WiFi
    - [ ] 链路聚合
    - [ ] 路由表
    - [ ] 默认路由

---
       
      
- [ ] DragonFlyBSD
  - [ ] DragonFlyBSD调优
  - [ ] 桌面
    - [ ] KDE5
    - [ ] Gnome
    - [ ] QQ
    - [ ] 微信
    - [ ] Wine
    - [ ] XFCE
    - [ ] 火狐浏览器
    - [ ] Chromium
  - [ ] DragonFlyBSD 安全加固
  - [ ] DragonFlyBSD 基础知识
    - [ ] 版本概况
    - [ ] 开发宗旨与项目目标
    - [ ] 注意事项
    - [ ] 跟踪新版本
    - [ ] pkgsrc
    - [ ] FreeBSD Ports
  - [ ] 换源与包管理器

## 规范化质量审核

|**图例**|✅|❌|ⁿ/ₐ|
|:---:|:---:|:---:|:---:|
|**状态**|已完成|未完成|不适用|

|项目|**可再现性**|**可查可信**|**结果验证**|**代码注释**|**图解/视频**|**故障排除/问题反馈**|**安全规范**|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|**第 2.0 节 FreeBSD 安装图解**|✅①|✅|✅|ⁿ/ₐ|✅|✅|❌|
|**第 2.1 节 手动安装双系统**|❌|❌|❌|❌|❌|❌|❌|
|**第 2.2 节 安装 FreeBSD——基于 Hyper-V**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 2.3 节 安装 FreeBSD——基于 Virtual Box**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 2.4 节 安装 FreeBSD——基于 Vmware Workstation Pro**|❌|❌|❌|❌|✅|❌|❌|
|**第 2.5 节 腾讯云轻量云及其他云服务器安装 FreeBSD**|❌|❌|❌|❌|✅|❌|❌|
|**第 2.6 节 普通电脑下载安装哪个镜像，如何刻录镜像？**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 2.7 节 SSH 相关软件推荐与 SSH 配置**|❌|❌|❌|❌|✅|❌|❌|
|**第 2.8 节 自带文本编辑器 ee 的用法**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 3.2 节 FreeBSD 换源方式**|❌|❌|❌|❌|✅|❌|❌|
|**第 3.3 节 gitup 的用法**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 3.4 节 软件包管理器 pkg 的用法**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 3.5 节 使用 ports 以源代码方式安装软件**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 3.6 节 通过 DVD 安装软件**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 3.7 节 通过 freebsd-update 更新 FreeBSD**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 3.8 节 通过源代码更新 FreeBSD**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 3.9 节 使用 pkgbase 更新 FreeBSD**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.0 节 概述（必看）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.1 节 安装显卡驱动及 Xorg（必看）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.2 节 安装 KDE5**|❌|❌|❌|❌|✅|❌|❌|
|**第 4.3 节 安装 Gnome**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.4 节 安装 Mate**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.5 节 安装 Xfce**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.6 节 安装 Cinnamon**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.7 节 安装 Lumina**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.8 节 安装 LXQt**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.9 节 安装 bspwm**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.10 节 root 登录桌面**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.11 节 主题与美化**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.12 节 远程桌面管理**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.13 节 安装 Wayland （可选）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.14 节 安装 Pantheon**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.15 节 安装 i3wm**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.16 节 安装 CDE**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.17 节 安装 Hyprland**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.18 节 打印机的安装（没有打印机无法测试）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.19 节 触摸板的设置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 4.20 节 声卡设置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.0 节 输入法与环境变量**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.1 节 Fcitx 输入法框架**|❌|❌|❌|❌|✅|❌|❌|
|**第 5.2 节 Ibus 输入法框架**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.3 节 五笔输入法**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.4 节 Firefox 与 Chromium 安装**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.5 节 FreeBSD 安装金山 WPS（Linux 版）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.6 节 FreeBSD 安装 QQ（Linux 版）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.7 节 更换字体**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.8 节 wine**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.9 节 压缩与解压**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 5.10 节 FreeBSD 安装微信（Linux 版）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.1 节 UFS**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.2 节 ZFS**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.3 节 磁盘扩容**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.4 节 NTFS**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.5 节 SWAP 交换分区的设置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.6 节 Ext 2/3/4 等文件系统**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.7 节 ZFS 磁盘加解密**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 6.8 节 自动挂载文件系统**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 7.1 节 HTTP 代理**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 7.2 节 V2ray**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 7.3 节 Clash**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 7.4 节 OpenVPN**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 8.1 节 sudo**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 8.2 节 添加用户**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 8.3 节 组**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 8.4 节 用户权限**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 9.1 节 jail 与 docker 的比较**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 9.2 节 jail 配置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 9.3 节 jail 更新**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 9.4 节 使用 qjail 管理 jail**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 10.1 节 虚拟化简介**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 10.2 节 安装 Virtual Box**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 10.3 节 使用 bhyve 安装 Windows 10**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 14.1 节 TCP BBR**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 14.2 节 WiFi**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 14.3 节 USB RNDIS (USB 网络共享)**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 14.4 节 蓝牙**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 14.5 节 以太网卡**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 14.6 节 USB 以太网卡和 USB 无线网卡**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 15.1 节 网络参数配置命令**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 15.2 节 PF**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 15.3 节 IPFW**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 15.4 节 IPFILTER (IPF)**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.1 节 FTP 服务器**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.2 节 MinIO 对象存储服务**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.3 节 Nodejs 相关**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.4 节 时间服务**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.5 节 Wildfly**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.6 节 rsync 同步服务**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.7 节 Samba 服务器**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.8 节 NFS 服务器**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 16.9 节 Webmin**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.1 节 Apache**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.2 节 Nginx**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.3 节 PHP 8.X**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.4 节 MySQL 5.X**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.5 节 MySQL 8.X**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.6 节 NextCloud——基于 PostgreSQL**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.7 节 Telegraf+InfluxDB+Grafana 监控平台**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.8 节 PostgreSQL 与 pgAdmin4**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 17.9 节 AList**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 20.1 节 游戏**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 20.2 节 音视频播放器与剪辑**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 20.3 节 科研与专业工具**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.1 节 Linux 兼容层实现**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.2 节 Linux 兼容层——基于 CentOS（FreeBSD Port）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.3 节 Linux 兼容层——基于 Ubuntu/Debian**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.4 节 Linux 兼容层——基于 ArchLinux bootstrap**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.5 节 Linux 兼容层——基于 archlinux-pacman**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.6 节 Linux 兼容层——基于 OpenSUSE**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.7 节 Linux 兼容层——基于 Gentoo Linux**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.8 节 Linux 兼容层——基于 Rocky Linux**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.9 节 Linux 兼容层——基于 Slackware Linux**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.10 节 RockyLinux 兼容层（FreeBSD Port）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.11 节 Linux 兼容层——基于 Deepin**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.12 节 高级教程：Linux 兼容层与 Jail**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 21.13 节 Linux 兼容层故障排除与配置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.4 节 C/C++ 环境的配置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.5 节 Java 环境的配置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.6 节 QT 环境的配置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.7 节 Python 与 VScode**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.8 节 Rust/Go 环境的配置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.9 节 Csh 与其他 Shell**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.10 节 通过 IDA 7 调试 FreeBSD**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.11 节 Git**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.12 节 安装 code-server 和 clangd**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 22.13 节 安装 code-server 和 clangd（不使用 Linux 兼容层）**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 23.1 节 恢复模式与密码重置**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 23.2 节 FreeBSD 多硬盘 EFI 引导统一**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 23.3 节 FreeBSD 中文 TTY 控制台**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 23.4 节 引导界面**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 23.5 节 Grub 及其他引导**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 24.1 节 BSD INIT 管理服务**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 24.2 节 FreeBSD 目录结构**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 24.3 节 bsdinstall 与 bsdconfig**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 24.4 节 禁用 Sendmail**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 24.5 节 利用脚本自动生成 BSDlibc 库文本**|❌|❌|❌|❌|❌|❌|❌|❌|
|**第 24.6 节 BSD 风格的 make/grep/sed/awk**|❌|❌|❌|❌|❌|❌|❌|❌|

注释：

- ①：找了学力偏下的初二学生和非计算机专业大专毕业生进行了验证，可顺利在 VMware 虚拟机中安装 FreeBSD。

## PDF 文档

> **PDF 文档导出流程**
>
> - 使用由 [safreya](https://github.com/safreya) 提供的脚本：
>   
>> 　　<https://github.com/FreeBSD-Ask/gitbook-pdf-export> 用于导出本书的 PDF 文档。该脚本使用 Python 3 编写，仅在 Windows 10、FreeBSD 14 上测试过。
>> 
>> 具体使用方法见该项目的 README.

## 概述

FreeBSD 从入门到跑路诞生于 2021 年 12 月 19 日。

本书定位：本书旨在敉平新手与进阶之间的台阶。

## 资源

QQ 群：787969044（须答题验证）

微信公众号: rpicn2025 （扫码关注）

![](./.gitbook/assets/qr.png)

Telegram 群组：[https://t.me/oh_my_BSD](https://t.me/oh_my_BSD)

Skype: [https://join.skype.com/xktkQtXZopfv](https://join.skype.com/xktkQtXZopfv)

FreeBSD 需要兼容层才能运行 QQ；Telegram 可原生运行；Skype 可使用 pidgin+ 插件 [net-im/pidgin-skypeweb](https://forums.freebsd.org/threads/skype.66115/)

HandBook 翻译：[https://handbook.bsdcn.org](https://handbook.bsdcn.org/)

FreeBSD Port 开发者手册翻译：[https://porters-handbook.bsdcn.org](https://porters-handbook.bsdcn.org/)

FreeBSD 入门书籍：[https://book.bsdcn.org](https://book.bsdcn.org/)

FreeBSD 中文 man 手册：[https://man.bsdcn.org](https://man.bsdcn.org/)

## 内容提要

《FreeBSD 从入门到跑路》 由 FreeBSD 中文社区发起。我们尝试从 0 开始，和所有人一同徜徉 FreeBSD 世界。

## 捐赠

![](.gitbook/assets/proud_donor.png)

[点此捐赠 FreeBSD 基金会](https://freebsdfoundation.org/donate)

有多的钱请捐给 FreeBSD 基金会吧。

