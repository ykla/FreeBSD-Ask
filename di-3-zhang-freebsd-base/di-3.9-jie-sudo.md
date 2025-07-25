# 3.9 sudo 和 doas


![权限示意图](../.gitbook/assets/qie-su.png)

## doas

实际上对于大部分人来说只需要 `sudo su` 这一行命令，其他都是多余的。

OpenBSD 认为 sudo 软件配置复杂，代码质量差，漏洞太多，故自行开发了 [doas](https://man.openbsd.org/doas)。自然，FreeBSD 也可以用。

### 安装 doas

- 使用 pkg 安装：

```sh
# pkg install doas
```

- 或者使用 Ports 安装：

```sh
# cd /usr/ports/security/doas/
# make install clean
```

### 查看 doas 安装后信息

```sh
root@ykla:~ # pkg info -D doas
doas-6.3p12:
On install:
To use doas,

/usr/local/etc/doas.conf

must be created. Refer to doas.conf(5) for further details and/or follow
/usr/local/etc/doas.conf.sample as an example.
# 要使用 doas，必须创建配置文件 /usr/local/etc/doas.conf。
# 可参考 doas.conf(5) 的联机文档，或查看 /usr/local/etc/doas.conf.sample 示例配置。

Note: In order to be able to run most desktop (GUI) applications, the user
needs to have the keepenv keyword specified. If keepenv is not specified then
key elements, like the user's $HOME variable, will be reset and cause the GUI
application to crash.
# 注意：如果需要运行图形界面（GUI）程序，配置中必须添加 keepenv 关键词。
# 否则像 $HOME 这样的环境变量将会被清空，导致 GUI 程序崩溃。

Users who only need to run command line applications can usually get away
without keepenv.
# 如果只需要运行命令行程序，通常不需要 keepenv。

When in doubt, try to avoid using keepenv as it is less secure to have
environment variables passed to privileged users.
# 如果不确定是否需要，建议尽量避免使用 keepenv，因为它可能降低系统安全性，
# 会将原用户的环境变量传递给拥有权限的目标用户。

On upgrade from doas<6.1:
With the 6.1 release the transfer of most environment variables (e.g. USER,
HOME and PATH) from the original user to the target user has changed.
# 从 doas 6.1 版本起，环境变量（如 USER、HOME、PATH）传递方式已发生变化。

Please refer to doas.conf(5) for further details.

# 请查看 doas.conf(5) 联机文档以了解更多详情。
```

### 配置 doas

由上可知，示例样板在 `/usr/local/etc/doas.conf.sample`。

而我们需要把配置文件放在 `/usr/local/etc/doas.conf`，该文件默认不存在，需要我们自行创建。

- `/usr/local/etc/doas.conf.sample` 内容如下，相比 sudo 来说，非常简单易懂：

让我们简单注释一下：

```
# Sample file for doas
# Please see doas.conf manual page for information on setting
# up a doas.conf file.

# Permit members of the wheel group to perform actions as root.
permit :wheel # 允许 wheel 组成员 doas

# Same without having to enter the password
permit nopass :wheel # 允许 wheel 组成员 doas，但免密码

# Permit user alice to run commands as a root user.
permit alice as root # 允许用户 alice doas

# Permit user bob to run programs as root, maintaining
# environment variables. Useful for GUI applications.
permit keepenv bob as root  # 允许用户 bob doas，并继承用户 bob 的环境变量，GUI 程序需要，但会降低安全性（参见查看安装后信息）

# Permit user cindy to run only the pkg package manager as root
# to perform package updates and upgrades.
permit cindy as root cmd pkg args update  # 仅允许用户 cindy 执行 pkg update
permit cindy as root cmd pkg args upgrade # 仅允许用户 cindy 执行 pkg upgrade

# Allow david to run id command as root without logging it
permit nolog david as root cmd id # 允许 David 以 root 身份运行 `id` 命令且不记录日志

```


对于一般人只需要创建文件 `/usr/local/etc/doas.conf`，写入

```sh
permit :wheel
```

即可满足日常需求（你的用户须加入 `wheel` 组）。

## sudo

### 安装 sudo

- 使用 pkg 安装：

```sh
# pkg install sudo
```

- 或者使用 Ports 安装：


```sh
# cd /usr/ports/security/sudo/ 
# make install clean
```

### sudo 免密码

在 `/usr/local/etc/sudoers.d/` 下新建两个文件 `username`（需要免密码的用户）和 `wheel`：

- 文件 `username` 内容如下：

```sh
%admin ALL=(ALL) ALL
```

- 文件 `wheel` 内容如下：

多加一行，使用 `sudo` 时不需要输入密码：

```sh
%wheel ALL=(ALL) NOPASSWD:ALL
```

### 故障排除与未竟事宜

- `xxx Is Not in the Sudoers File. This Incident Will Be Reported`

应当在 sudoers 中加入一句话来解决这个问题：


编辑 `/usr/local/etc/sudoers`，找到 `root ALL=(ALL:ALL) ALL` 这行，一般是在第 94 行。在这行下面加一句：

```sh
你的普通用户名 ALL=(ALL:ALL) ALL
```

然后保存退出即可。
