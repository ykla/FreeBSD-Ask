# 4.5 使用 Ports 以源代码方式安装软件

一款软件的相关文件或文件夹的（补丁文件、校验码、Makefile 等）集合（表现为一个文件夹）为一个 Port，所有 Port（移植软件）的集合即 Ports Collection，即 Ports。

NetBSD 和 OpenBSD 也使用 Ports（不通用）。

> **注意**
>
> ports 和 pkg 可以同时使用，而且大部分人也是这么用的。但是要注意 pkg 的源必须是 latest，否则会存在一些依赖上的问题（比如 ssl）。latest 的源也比主线上的 ports 要出来的晚（是从中编译出来的），因此即使是 latset 源也可能会出现上述问题，总之有问题出现时就卸载那个 pkg 安装的包，重新使用 ports 编译即可。

![Ports 流程图](../.gitbook/assets/ports-pkg.png)


>**技巧**
>
>ports 下载路径是 `/usr/ports/distfiles/`。


## 使用 ports 压缩包

使用压缩包成功地规避了先有鸡还是先有蛋的哲学问题（要安装 Git 但是没有 Ports 也不想用 pkg 的话）。

### 下载 ports 压缩包

- NJU:

```sh
# fetch https://mirrors.nju.edu.cn/freebsd-ports/ports.tar.gz
```

- 或 USTC

```sh
# fetch https://mirrors.ustc.edu.cn/freebsd-ports/ports.tar.gz
```

- 又或 FreeBSD 官方

```sh
# fetch https://download.freebsd.org/ftp/ports/ports/ports.tar.gz
```

### 解压 ports 压缩包


```sh
# tar -zxvf ports.tar.gz -C /usr/ # 解压至路径
# rm ports.tar.gz # 删除存档
```


## 使用 Git 获取 Ports

### 安装 Git

- 使用 pkg 安装：

```sh
# pkg install git
```

### 拉取 Ports 存储库（USTC）浅克隆

```sh
# git clone --filter=tree:0 https://mirrors.ustc.edu.cn/freebsd-ports/ports.git /usr/ports
```

### 拉取 Ports 存储库（FreeBSD 官方）浅克隆

```sh
# git clone --filter=tree:0 https://git.FreeBSD.org/ports.git /usr/ports
```

### 完全拉取 Ports 存储库（FreeBSD 官方）并指定分支

```sh
# git clone https://git.FreeBSD.org/ports.git /usr/ports
```

查看所有分支：

```sh
# cd /usr/ports/ # 切换到 git 项目
# git branch -a
* main # * 代表当前分支
  remotes/origin/2014Q1

	……省略…………

  remotes/origin/2025Q1
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```

切换到 `2025Q1` 分支：


```sh
root@ykla:/usr/ports # git switch 2025Q1
正在更新文件: 100% (14323/14323), 完成.
分支 '2025Q1' 设置为跟踪 'origin/2025Q1'。
切换到一个新分支 '2025Q1'
```

查看本地分支：

```sh
root@ykla:/usr/ports # git branch
* 2025Q1
  main
```

已经切换成功。


### 同步更新 Ports Git


```sh
root@ykla:/ # cd /usr/ports/ # 切换目标目录
root@ykla:/usr/ports # git pull # 同步更新上游 Ports
```

如果提示本地已经修改，放弃本地修改，再更新：

```sh
root@ykla:/usr/ports # git checkout . # 放弃本地修改
root@ykla:/usr/ports # git pull
```

### 故障排除与未竟事宜


```sh
fatal: unable to access 'https://mirrors.ustc.edu.cn/freebsd-ports/ports.git/': SSL certificate problem: certificate is not yet valid
```

先检查时间：

```sh
# date
Fri May 31 12:09:26 UTC 2024
```

时间错误。校对时间：


```sh
# ntpdate -u pool.ntp.org
 5 Oct 08:39:16 ntpdate[3276]: step time server 202.112.29.82 offset +10960053.088901 sec
```

检查时间：

```sh
# date
Sat Oct  5 08:39:21 UTC 2024
```

## 使用 `whereis` 查询软件路径

如

```sh
# whereis python
```

将输出

```sh
python: /usr/ports/lang/python
```



## 查看依赖

已经安装：

```sh
root@ykla:~ # pkg info -d screen
screen-4.9.0_6:
	indexinfo-0.3.1
```

未安装：

```sh
root@ykla:/usr/ports/sysutils/htop # make all-depends-list
/usr/ports/ports-mgmt/pkg
/usr/ports/devel/pkgconf
/usr/ports/devel/kyua
……省略一部分……
```


## 看看 python 的 ports 在哪

```sh
# whereis python
# python: /usr/ports/lang/python
```

## 安装 python3

```sh
# cd /usr/ports/lang/python
# make BATCH=yes clean
```

其中 `BATCH=yes` 意味着使用默认参数进行编译。

## 如何设置全部所需的依赖

```sh
# make config-recursive
```

## 如何使用 pkg 安装依赖

不使用 Ports 来编译依赖，仅使用 Ports 来编译软件包本体：

```sh
# make install-missing-packages
```

  以 `chinese/fcitx` 为示例：

```sh
root@ykla:~ # cd /usr/ports/chinese/fcitx
root@ykla:/usr/ports/chinese/fcitx # make install-missing-packages
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
Updating FreeBSD-base repository catalogue...
FreeBSD-base repository is up to date.
All repositories are up to date.
Updating database digests format: 100%
The following 2 package(s) will be affected (of 0 checked):

New packages to be INSTALLED:
	e2fsprogs-libuuid: 1.47.1 [FreeBSD]
	enchant2: 2.2.15_5 [FreeBSD]

Number of packages to be installed: 2

94 KiB to be downloaded.

Proceed with this action? [y/N]: 
```

## 如何删除当前 port 及其依赖的配置文件

```sh
# make rmconfig-recursive
```

## 如何一次性下载所有需要的软件包

```sh
# make BATCH=yes fetch-recursive
```

## ports 编译的软件也可以转换为 pkg 包

```sh
# pkg create nginx
```

## 更新 FreeBSD 软件包/Port

先同步更新 Ports Git。

然后列出过时 Port 软件：

```sh
root@ykla:/usr/ports # pkg version -l '<'
chromium-127.0.6533.99             <
curl-8.9.1_1                       <
ffmpeg-6.1.2,1                     <
vlc-3.0.21_4,4                     <
w3m-0.5.3.20230718_1               <
```

下边分别列出 2 种 FreeBSD 手册中提及的升级工具：

### ① portmaster（推荐）

- 更新：

```sh
# cd /usr/ports/ports-mgmt/portmaster && make install clean
# portmaster -a #自动升级所有软件
# portmaster screen #升级单个软件
```

如果不想回答问题解决依赖，可使用类似 BATCH=yes 的选项 `-a -G --no-confirm`：

```sh
# portmaster -a -G --no-confirm
```

#### 查看依赖关系

```sh
root@ykla:/usr/ports/ports-mgmt/portmaster # portmaster sysutils/htop  --show-work

===>>> Port directory: /usr/ports/sysutils/htop

===>>> Starting check for all dependencies
===>>> Gathering dependency list for sysutils/htop from ports

===>>> Installed devel/autoconf
===>>> Installed devel/automake
===>>> NOT INSTALLED		devel/libtool
===>>> NOT INSTALLED		devel/pkgconf
===>>> NOT INSTALLED		lang/python311
===>>> Installed ports-mgmt/pkg
```

### ② portupgrade

```sh
# cd /usr/ports/ports-mgmt/portupgrade && make install clean
# portupgrade -ai #自动升级所有软件，i 会挨个确认
# portupgrade -R screen #升级单个软件
# portupgrade -a --batch		#不要问，只做，等同于  BATCH=yes
```

#### 参考资料

- [portmaster -- manage your ports without external databases or languages](https://man.freebsd.org/cgi/man.cgi?portmaster(8))
- [portupgrade,  portinstall -- tools to upgrade installed packages	or in- stall new ones via ports	or packages](https://man.freebsd.org/cgi/man.cgi?portupgrade(1))
  

## FreeBSD USE


- 如何全局屏蔽 mysql

```sh
# echo "OPTION_UNSET+= MYSQL" >> /etc/make.conf
```

完整的列表见 <https://cgit.freebsd.org/ports/tree/Mk/bsd.default-versions.mk>

## FreeBSD ports 多线程编译

将以下内容写入 `/etc/make.conf`，没有就 `touch` 新建一个。

```ini
FORCE_MAKE_JOBS=yes
MAKE_JOBS_NUMBER=4
```

Linux 如 Gentoo 上一般是直接 `-jx` 或者 `jx+1`, `x` 为核心数。

`4` 是处理器核心数（还是线程数？）。

可以通过命令查询：

```sh
root@ykla:/home/ykla # sysctl kern.smp.cpus
kern.smp.cpus: 16
```

或者：

```sh
root@ykla:/home/ykla # sysctl hw.ncpu 
hw.ncpu: 16
```

输出值即为 `MAKE_JOBS_NUMBER` 值。

英特尔的处理器搜索 `CPU 型号+ARK` 转跳英特尔官网可查询线程数。

- 个别情况下可以设置别名加速编译：（非永久设置，FreeBSD 14 无须设置默认即生效）

```sh
# alias ninja='ninja -j4'
```

### 参考资料

- [Easy way to get cpu features](https://forums.freebsd.org/threads/easy-way-to-get-cpu-features.10553/)，获取 CPU 线程数量的命令来自此处。

## 设置内存为 `tmp`

```sh
# ee /etc/fstab
```

写入：

```sh
tmpfs /tmp tmpfs rw 0 0
```

`reboot` 重启即可。

### 参考资料

- [tmpfs --in-memory file system](https://man.freebsd.org/cgi/man.cgi?tmpfs(5))


## ccache

>**警告**
>
>使用 ccache 可能会导致编译失败！只在重复编译时起效果，首次编译不仅不会加速还会慢上一些。是一种以空间换时间的行为。


### ccache3

使用 pkg 安装：

```sh
root@ykla:~ # pkg install ccache
```

- 使用 Ports 安装：

```
# cd /usr/ports/devel/ccache/ 
# make install clean
```

- 查看软链接情况：

```sh
root@ykla: # ls -al  /usr/local/libexec/ccache
total 56
drwxr-xr-x   3 root wheel 15 Sep 20 02:02 .
drwxr-xr-x  18 root wheel 49 Sep 20 01:39 ..
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 CC -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 c++ -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 cc -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 clang -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 clang++ -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 clang++15 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 02:02 clang++18 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 clang15 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 02:02 clang18 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 cpp13 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 g++13 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21 Sep 20 00:29 gcc13 -> /usr/local/bin/ccache
drwxr-xr-x   2 root wheel 15 Sep 20 02:02 world
```

---

- 修改 `/etc/make.conf`，加入下面一行：

```sh
WITH_CCACHE_BUILD=yes
```

- 设置编译缓存最大为 10GB：

```sh
root@ykla:/usr/ports/devel/ccache4 # ccache -M 10G  
Set cache size limit to 10.0 GB
root@ykla:/usr/ports/www/chromium # ccache -s
cache directory                     /root/.ccache
primary config                      /root/.ccache/ccache.conf
secondary config      (readonly)    /usr/local/etc/ccache.conf
cache hit (direct)                     0
cache hit (preprocessed)               0
cache miss                             0
cache hit rate                      0.00 %
cleanups performed                     0
files in cache                         0
cache size                           0.0 kB
max cache size                      10.0 GB
```

- 在 Ports 编译一段时间后：

```sh
root@ykla:~ # ccache -s
cache directory                     /root/.ccache
primary config                      /root/.ccache/ccache.conf
secondary config      (readonly)    /usr/local/etc/ccache.conf
stats updated                       Fri Sep 20 02:05:35 2024
cache hit (direct)                    20
cache hit (preprocessed)              17
cache miss                           918
cache hit rate                      3.87 %
called for link                      121
called for preprocessing              26
compile failed                       115
preprocessor error                    66
bad compiler arguments                15
autoconf compile/link                523
no input file                         71
cleanups performed                     0
files in cache                      2305
cache size                           0.0 kB
max cache size                      10.0 GB
```

### ccache4

目前最新版本是 ccache4：

使用 pkg 安装：

```sh
# pkg install ccache4
```

或使用 Ports 安装：

```sh
# cd /usr/ports/devel/ccache4/
# make install clean
```

- 查看软链接情况：

```sh
root@ykla:~ # ls -al  /usr/local/libexec/ccache    total 55
drwxr-xr-x   3 root wheel 13  9月 20 02:29 .
drwxr-xr-x  20 root wheel 54  9月 20 02:29 ..
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 c++ -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 cc -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 CC -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 clang -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 clang++ -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 clang++15 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 clang15 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 cpp13 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 g++13 -> /usr/local/bin/ccache
lrwxr-xr-x   1 root wheel 21  9月 20 02:29 gcc13 -> /usr/local/bin/ccache
drwxr-xr-x   2 root wheel 13  9月 20 02:29 world
```

---

- 修改 `/etc/make.conf`，加入下面一行：

```sh
WITH_CCACHE_BUILD=yes
```

- 设置编译缓存最大为 20GB：

```sh
root@ykla: # ccache -M 20G  
Set cache size limit to 20.0 GB
```

- 在 Ports 编译一段时间后，查看编译缓存：

```sh
root@ykla:/ # ccache -s
Cacheable calls:   558 /  579 (96.37%)
  Hits:            110 /  558 (19.71%)
    Direct:        110 /  110 (100.0%)
    Preprocessed:    0 /  110 ( 0.00%)
  Misses:          448 /  558 (80.29%)
Uncacheable calls:  21 /  579 ( 3.63%)
Local storage:
  Cache size (GB): 0.0 / 20.0 ( 0.11%)
  Hits:            110 /  558 (19.71%)
  Misses:          448 /  558 (80.29%)
```

查看当前配置文件：

```sh
root@ykla:~ # ccache -p 
(default) absolute_paths_in_stderr = false
(default) base_dir =
(default) cache_dir = /root/.cache/ccache
……省略一部分……
```

### 参考文献

- [ccache-howto-freebsd.txt.in](https://github.com/freebsd/freebsd-ports/blob/main/devel/ccache/files/ccache-howto-freebsd.txt.in)
- [ccache -a fast C/C++ compiler cache](https://man.freebsd.org/cgi/man.cgi?query=ccache&sektion=1&n=1)

## 多线程下载

### axel

安装：

```sh  
# pkg install axel
```

或者

```sh
# cd /usr/ports/ftp/axel/
# make install clean
```

新建或者编辑 `/etc/make.conf` 文件，写入以下几行：

```sh
FETCH_CMD=axel
FETCH_BEFORE_ARGS= -n 10 -a
FETCH_AFTER_ARGS=
DISABLE_SIZE=yes
```

### wget2
  
```sh
# cd /usr/ports/www/wget2/ && make install clean
```

新建或者编辑 `/etc/make.conf` 文件，写入以下几行：

```sh
FETCH_CMD=wget2
FETCH_BEFORE_ARGS= -c -t 3 -o 10
FETCH_AFTER_ARGS=
DISABLE_SIZE=yes
```

- `-c` 断点续传；
- `-t 3` 重试次数 3；
- `-o 10` 启用 10 个线程进行下载。

>**技巧**
>
>`10` 这个参数可能过于保守。但是要注意很多服务器不支持较多线程同时下载。同时会给服务器带来较大压力。

### 参考文献

- [ports --contributed applications](https://man.freebsd.org/cgi/man.cgi?query=ports&sektion=7)，`FETCH_CMD` 的出处，同时也是参数 `BATCH` 的出处。

