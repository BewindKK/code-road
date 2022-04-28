# 基础

## 什么是Linux?

- Linus编写的开源操作系统的内核
- 广义的操作系统

服务端要做的事情不一样，不需要华丽的界面

## 环境

云主机

虚拟机：就算有危险操作也不影响

## Linux版本

https://www.kernel.org/

内核版本分为三个部分

主版本号、次版本号、末版本号

次版本号是奇数为开发版，偶数为稳定版



**发行版**

RedHat Enterprise Linux：软件经过专业人员测试，比较稳定，收费

Fedora：没有经过专业测试

CentOS：稳定免费

有桌面系统

Debian

Ubuntu

## Linux虚拟机安装



## Linux常见目录结构

- /

  根目录

- 

- **/bin**：
  bin 是 Binaries (二进制文件) 的缩写, 这个目录存放着最经常使用的命令。

- **/boot：**
  这里存放的是启动 Linux 时使用的一些核心文件，包括一些连接文件以及镜像文件。

- **/dev ：**
  dev 是 Device(设备) 的缩写, 该目录下存放的是 Linux 的外部设备，在 Linux 中访问设备的方式和访问文件的方式是相同的。

- **/etc：**
  etc 是 Etcetera(等等) 的缩写,这个目录用来存放所有的系统管理所需要的**配置文件和子目录**。

- **/home**：
  **用户的主目录**，在 Linux 中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的，如上图中的 alice、bob 和 eve。

- **/lib**：
  lib 是 Library(库) 的缩写这个目录里存放着系统最基本的动态连接共享库，其作用类似于 Windows 里的 DLL 文件。几乎所有的应用程序都需要用到这些共享库。

- **/lost+found**：
  这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

- **/media**：
  linux 系统会自动识别一些设备，例如U盘、光驱等等，当识别后，Linux 会把识别的设备挂载到这个目录下。

- **/mnt**：
  系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在 /mnt/ 上，然后进入该目录就可以查看光驱里的内容了。

- **/opt**：
  opt 是 optional(可选) 的缩写，这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

- **/proc**：
  proc 是 Processes(进程) 的缩写，/proc 是一种伪文件系统（也即虚拟文件系统），存储的是当前内核运行状态的一系列特殊文件，这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
  这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

  ```
  echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
  ```

- **/root**：
  该目录为系统管理员，也称作**超级权限者的用户主目录**。

- **/sbin**：
  s 就是 Super User 的意思，是 Superuser Binaries (超级用户的二进制文件) 的缩写，这里存放的是**系统管理员使用的系统管理程序。**

- **/selinux**：
   这个目录是 Redhat/CentOS 所特有的目录，Selinux 是一个安全机制，类似于 windows 的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。

- **/srv**：
   该目录存放一些服务启动之后需要提取的数据。

- **/sys**：

  这是 Linux2.6 内核的一个很大的变化。该目录下安装了 2.6 内核中新出现的一个文件系统 sysfs 。

  sysfs 文件系统集成了下面3种文件系统的信息：针对进程信息的 proc 文件系统、针对设备的 devfs 文件系统以及针对伪终端的 devpts 文件系统。

  该文件系统是内核设备树的一个直观反映。

  当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

- **/tmp**：
  tmp 是 temporary(临时) 的缩写这个目录是用来存放一些临时文件的。

- **/usr**：
   usr 是 unix shared resources(共享资源) 的缩写，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于 windows 下的 program files 目录。

- **/usr/bin：**
  系统用户使用的应用程序。

- **/usr/sbin：**
  超级用户使用的比较高级的管理程序和系统守护程序。

- **/usr/src：**
  内核源代码默认的放置目录。

- **/var**：
  var 是 variable(变量) 的缩写，这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。

- **/run**：
  是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。

# Linux命令

```shell
# 通用
Ctrl+r	#搜索之前出现的命令
上箭头		# 向上翻查
命令 | more #分页显示，按空格翻页


# 万能的帮助命令

# man命令 是 manual 的缩写
eg:
man ls
# man 也是一条命令，分为 9 章，可以使用 man 命令获得 man 的帮助;分开章节是因为命令有重名的现象
# 上述命令省略了"1"
man 7 man

# 按Q键退出命令行终端

# help 帮助
# shell（命令解释器）自带的命令称为内部命令，其他的是外部命令
# 内部命令使用 help 帮助
help cd
# 外部命令使用help帮助
ls --help
# 利用type命令去区分内部命令和外部命令

# info 帮助
# info 帮助比 help 更详细，作为 help 的补充
info ls

# 使用网络资源，搜索引擎，官方文档


# 对文件操作
# 显示当前目录名称
pwd

# 更改当前操作目录
cd /path/to/...  绝对路径
cd ./path/to/... 相对路径	'.'当前目录
cd ../path/to/... 相对路径	两个点上一级目录

# 使用Tab自动补全文件名

# 查看当前目录下的文件
ls [选项，选项...] 参数...
	常用参数
	-l 长格式显示文件
	-a 显示隐藏文件
	-r 逆序显示
	-t 按照时间顺序显示
	-R 递归显示
# ls后面可以带多个文件目录
ls /root /

# 详解ls
ls -l .(当前无参数时可以把"."省略)
# 第一个字符为"-"代表普通文件，后边9个文件代表文件的权限 第一个root代表是谁创建了这个文件 数字代表当前文件的大小 时间代表最后修改时间
lrwxrwxrwx.  1 root root     7 Jul 11  2019 bin -> usr/bin
dr-xr-xr-x.  5 root root  4096 Jul 11  2019 boot
drwxr-xr-x  19 root root  2980 Apr 22 16:47 dev
drwxr-xr-x. 77 root root  4096 Apr 22 16:44 etc

# 显示隐藏文件夹 以'.'开头即为隐藏文件夹
ls -a

# 按照文件名逆序显示
ls -l -r

# 按照时间进行逆向显示
ls -l -r -t
ls -lrt # 执行效果相同
ls -lh #文件大小以M显示

# 查看固定目录权限
ls -ld /test


# 创建和删除目录
# 建立目录
mkdir /a #在根目录下建立名称为a的文件夹
mkdir a  # 在当前目录下建立
mkdir a b x # 在当前目录下建立多个文件夹
mkdir a/b/c # 创建多级目录
mkdir -p /a/b/c/d/e/f # 创建多级目录
ls -R /a #递归查看多级目录

# 删除文件夹
rmdir /a #只能删除空白的目录
rm -r # 删除非空目录
rm -r -f # 删除不会进行提示-----------此命令为危险操作---------------------------
rm -rf


# 复制和移动目录
cp [要复制的原文件目录] [目标文件目录]
cp -r /root/a /tmp # 要复制目录
cp -v /filea /tmp # 显示复制过程
cp -p /filea /tmp # 复制的时候保留原有时间
cp -a /filea /tmp #权限，创建人，时间都保留
#创建空白文件
touch /filea
# 移动
mv /filea /tmp
# 改名
mv /filea /fileb
# 移动+改名
mv /tmp/fileb /filec
# 对当前目录下所有文件进行操作-----通配符
cp file* / #将当前目录下文件名前缀为file下的所有文件进行复制 '*'也可以代表多个字符
ls file*  # 使用ls也可以使用通配符
cp file? # "?"代表单个字符


# 文本查看命令
cat # 文本内容显示到终端，可以跟多个文件名称
head # 查看文件开头
head -5 /tmp/demo # 指定显示文件行数
tail # 查看文件结尾 常用参数-f 文件内容更新后，显示信息同步更新
tail -5 /tmp/demo # 指定显示文件行数
wc # 统计文件内容信息，显示行数
more /tmp/demo #分行显示


# 打包压缩和解压缩
# 最早的Linux备份介质是磁带,使用的命令是tar
# 可以打包后的磁带文件进行压缩储存，压缩的命令是gzip(更快压缩)和bzip2(更高压缩比例)
# 经常使用的扩展名是.tar.gz .tar.bz2 .tgz
# 打包
tar 打包命令
	# 常用参数
	c 打包
	x 解包
	f 指定操作类型为文件
tar cf /tmp/etc-back.tar /etc #对etc这个目录进行打包
tar czf /tmp/etc-back.tar.gz /etc # 打包并进行压缩
tar cjf /tmp/etc-back.tar.bz2 /etc #打包并进行压缩
tar xf /tmp/etc-back.tar -C /root #对/tmp/etc-back.tar进行解包，放到/root中


# 用户和权限管理

useradd #新建用户root用户
id [用户名] #验证某个用户是否存在
userdel #删除用户，不会删除家目录
userdel -r [用户名] #会删除家目录
passwd  #修改用户密码 +用户名-->修改指定用户密码 +-->修改当前用户密码
usermod #修改用户属性 通过man usermod进入帮助
chage   #修改用户属性 修改用户密码过期时间

# 组管理命令
groupadd #新建用户组
groupdel #删除用户组
usermod -g group1 user1 #修改用户组
useradd -g group1 user2 #在创建的时候指定组

# 切换用户权限 普通用户切换需要输入密码
su - user #- 会把运行环境一起变为user的环境
su #切换用户
su - USERNAME #使用 login shell 方式切换用户
sudo #以其他用户身份执行命令，只能执行授权的命令
visudo #设置需要使用 sudo 的用户（组）


# 用户和用户组配置文件介绍

# 用户配置文件
/root  #root用户的家目录
/home/USERNAME #普通用户默认家目录位置
/etc/passwd #用户配置文件
/etc/shadow #用户密码相关配置文件
/etc/group #用户组配置文件

#/etc/passwd #用户配置文件
admin:x:1000:1000::/home/admin:/bin/bash	#x：是否需要密码登录；1000：userid ；1000：groupid ；注释
# /etc/shadow #用户密码相关配置文件
root:$6$lboAicVjKAkJKq$THcjYvRzE #用户名:加密后的密码


# 文件权限的表示方法

- rw- r-x r- - 1 userame groupname mtime filename #'-':类型，前三个字符代表当前用户有的权限，中间三个代表当前用户组有的权限，最后三个字符代表其他人对此文件的权限
# 文件类型 不是利用拓展名在区分文件
- #普通⽂件
d #⽬录⽂件
b #块特殊⽂件，指代设备
c #字符特殊⽂件 shell终端
l #符号链接 相当于win快捷方式
p #命名管道
s #套接字⽂件

# ⽂件权限的表示⽅法
# 字符权限表示⽅法
r #读
w #写
x #执⾏
# 数字权限的表示⽅法
r = 4
w = 2
x = 1
#创建新⽂件有默认权限，根据 umask 值计算，属主和属组根据当前进程的⽤户来设定

# ⽬录权限的表示⽅法
x #进⼊⽬录
rx #显示⽬录内的⽂件名
wx #修改⽬录内的⽂件名

# 修改权限命令

chmod #修改⽂件、⽬录权限
	chmod u+x /tmp/testfile
	chmod 755 /tmp/testfile
	u	#对属主进行更改，前三个
	g	#属组权限，中间三个
	o	#其他人权限 最后三个
	+	# 增加权限
	-	# 减少权限
	=	# 设置权限
	777	# 有最高权限
	400	# 只有读取权限
	644	# 默认权限，自己读写，其他人只读
	000	# 所有权限都没有
chown 更改属主、属组
chown user1:group1 afile #同时对属主和属组进行修改
chgrp 可以单独更改属组，不常⽤

# 特殊权限	建议保持默认权限
SUID #⽤于⼆进制可执⾏⽂件，执⾏命令时取得⽂件属主权限	如 /usr/bin/passwd
SGID #⽤于⽬录，在该⽬录下创建新的⽂件和⽬录，权限⾃动更改为该⽬录的属组	文件共享
SBIT #⽤于⽬录，该⽬录下新建的⽂件和⽬录，仅 root 和⾃⼰可以删除	如 /tmp


# 网络管理

# 网络查看工具
#net-tools CentOS之前
ifconfig
route
netstat
# iproute
ip
ss

# ⽹络状态查看命令
ifconfig
	# 后边可以接一个单独的网卡进行查看
	eth0 第⼀块⽹卡（⽹络接⼝）
	你的第⼀个⽹络接⼝可能叫做下⾯的名字
		eno1 板载⽹卡
		ens33 PCI-E⽹卡
		enp0s3 ⽆法获取物理信息的 PCI-E ⽹卡
		CentOS 7 使⽤了⼀致性⽹络设备命名，以上都不匹配则使⽤ eth0
	inet XXXX # 网卡ip地址
	netmask		# 子网掩码
	ether		# 网卡mac地址
	
	lo	#网卡，本地环回，本地测试
	virbr0 #linux上用来做虚拟化的网卡，虚拟网关
	
	# 对网卡进行批量操作
	vim /etc/default/grub	增加 biosdevname=0 net.ifnames=0  #重启生效
# 在家用当中可以知道实际运用了哪几个网卡，在服务器运用中因网卡名称不用无法进行批量化操作

# ⽹络接⼝命名修改
# ⽹卡命名规则受 biosdevname 和 net.ifnames 两个参数影响
# 编辑 /etc/default/grub ⽂件，增加 biosdevname=0 net.ifnames=0  
# 更新 grub
grub2-mkconfig -o /boot/grub2/grub.cfg
# 重启
reboot
biosdevname 	net.ifnames 	⽹卡名
	0				1			ens33
	1				0			em1
	0				0			eth0

# 查看网络情况
mii-tool eth0 #查看⽹卡物理连接情况
# 查看网关命令
route -n #使⽤ -n 参数不解析主机名

# 修改网络配置
# ⽹络配置命令
ifconfig <接⼝> <IP地址> [netmask ⼦⽹掩码 ]
ifconfig eth0 10.10.12.112
ifup <接⼝>
ifdown <接⼝>

# ⽹关配置命令
#添加⽹关
	route add default gw <⽹关ip>
	route add -host <指定ip> gw <⽹关ip>
	route add -net <指定⽹段>(eg:198.168.0.0) netmask <⼦⽹掩码> gw <⽹关ip>
	
# ⽹络命令集合：ip 命令
ip addr ls
	ifconfig
ip link set dev eth0 up
	ifup eth0
ip addr add 10.0.0.1/24 dev eth1
	ifconfig eth1 10.0.0.1 netmask 255.255.255.0
ip route add 10.0.0/24 via 192.168.0.1
	route add -net 10.0.0.0 netmask 255.255.255.0 gw 192.168.0.1
	
# ⽹络故障排除命令
ping #检测当前主机与目标主机是否畅通
ping www.baidu.com
traceroute #跟踪在那里丢包	-w(等待)	1(等待1秒)
traceroute -w 1 www.baidu.com
mtr	#详细网络信息：丢包率...
nslookup #解析域名对应的ip
telnet	# 查看端口的连接状态
tcpdump # 跟细致分析数据包，抓包工具
netstat #查看Linux中网络系统状态信息
ss #比 netstat 好用的socket统计信息，iproute2 包附带的另一个工具，允许你查询 socket 的有关统计信息

# ⽹络服务管理程序分为两种，分别为SysV和systemd
service network start|stop|restart
chkconfig -list network
systemctl list-unit-files NetworkManager.service
systemctl start|stop|restart NetworkManger
systemctl enable|disable NetworkManger

# ⽹络配置⽂件
ifcfg-eth0
/etc/hosts

hostname
hostnamectl
	hostnamectl set-hostname centos7.test
	注意修改/etc/hosts⽂件
	

# 软件安装

# 软件包管理器
#包管理器是⽅便软件安装、卸载，解决软件依赖关系的重要⼯具
	#CentOS、RedHat 使⽤ yum 包管理器，软件安装包格式为 rpm
	#Debian、Ubuntu 使⽤ apt 包管理器，软件安装包格式为 deb

#rpm 包
#rpm 包格式
vim-common-7.4.10-5.el7.x86_64.rpm
软件名称 软件版本 系统版本 平台
# rpm 命令
# rpm 命令常⽤参数
	-q #查询软件包
	-i #安装软件包
	-e #卸载软件包

ls /dev/sr0 -l	#显示对应设备
mount /dev/sr0 /mnt	#挂载设备

# yum 包管理器
#CentOS yum 源
http://mirror.centos.org/centos/7/
#国内镜像
https://opsx.alibaba.com/mirror
# yum 配置⽂件
/etc/yum.repos.d/CentOS-Base.repo
wget -O /etc/yum.repos.d/CentOS-Base.repo #覆盖原有配置文件
# yum命令常⽤选项
install #安装软件包
remove #卸载软件包
list| grouplist #查看软件包
update #升级软件包


#ji


```

# Vim文本编辑器

## Vim四种模式

Vim对Vi做了很多增强

正常模式(Normal-mode)

插入模式(Insert-mode)

命令模式(Command-mode)

可视模式(Visual-mode)：高级操作

**1、正常模式(Normal-mode)**



## Vim命令

```shell
# 正常模式

h(向左移动) j k l(x) # 移动光标
# 进入其他模式转换命令
i I a A o O  #进入插入模式 大写O会在光标所在行的上一行进入插入模式，小写o光标所在下一行
v V ctrl+v  #进入可视化模式
： #进入命令模式 q退出
esc  #从其他模式回到正常模式
# 基本操作
yy #按行复制
[num] yy # 复制多行
y$ # 复制光标到行结尾的字符
dd #按行剪切
[num] yy # 复制多行
d$ # 剪切光标到行结尾的字符
p  #粘贴
u #撤销
ctrl+r #把撤销的命令重做
x #删除单个字符
r #替换字符，在光标所在位置按r键在输入新的字符
:set nu #显示当前行号
[num] shift+g # 移动到指定行
g #移动到第一行
G #移动到最后一行
^  #光标来到开头
$  #光标来到结尾


# 命令模式

: #正常模式->命令模式
:w /demo.txt #保存demo文件到根目录下
:wq	#保存并退出
:w #保存
:q! #不对文件进行保存
:! ifconfig #临时输入命令查看ip地址
:! which [命令名] #寻找命令所在的位置
/x # 查找x
n #在查找到的结果中向下移动
shift+n #在查找到的结果中向上移动
:s/old/new # 替换针对光标所在的一行进行替换
:%s/old/new/g #对整个文件进行替换,global全局操作
:3,5s/old/new #第三行到第五行之间进行替换，g为可选命令

# 对Vim进行操作
:set nu #显示行号
:set nonu #不显示行号
vim /etc/vimrc #修改Vim配置文件
一直显示行号 # 在上述配置文件加上 set nu


# 插入模式 i进入


# 可视模式 
v  #正常模式->可视模式 字符可视模式，字符走过的地方颜色背景会变化
shift+V  #可视行模式
ctrl+v  #块可视
shift+i [直接输入即可] ->再连续按两次esc 即可将选中的都进行操作# 在每一行前都加 123，可视模式选中后
#批量删除
```

