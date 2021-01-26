.. linux-study-notes.rst documentation master file, created by
   zq on 2021.1.7.

=======================
Linux学习笔记
=======================

.. 插入目录
.. contents:: 目录
   :depth: 3

Linux的目录结构
=======================

基本介绍
------------

#. linux的文件系统是采用集层式的树状目录结构，最上层是根目录“/“。
#. 在linux中，一切皆文件。

具体的目录结构
----------------

* /bin [常用] (/usr/bin、/usr/local/bin)是Binary的缩写，存放着最经常使用的指令。
* /etc [常用] 所有系统管理所需要的配置文件和子目录。
* /usr [常用] 非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于Windows下的program files目录。
* /usr/local 这是另一个给主机额外安装软件所安装的目录，一般是通过编译源码方式安装的程序。
* /lib 系统开机所欲需要的最基本的动态链接共享库，其作用类似于Windows的DLL文件，几乎所有的应用程序都需要用到这些共享库。
* /sbin [常用] (/usr/sbin、/usr/local/sbin)s就是Super User，存放的是系统管理员使用的系统管理指令。
* /root [常用] 超级权限者的用户主目录
* /boot [常用] 存放启动Linux时使用的核心文件，包括一些链接文件以及镜像文件。
* /proc 该目录是虚拟的目录，是系统内存的映射，访问目下的文件获取系统信息。
* /srv service缩写，存放一些服务启动之后需要提取的数据。
* /sys 这是linux2.6内核的一个很大的变化，该目录下安装了2.6内核中新出现的一个文件系统sysfs。
* /tmp 存放一些临时文件的。
* /dev 类似于Windows的设备管理器,把所有的硬件用文件的形式存储。
* /media [常用] Linux会自动识别一些设备，例如U盘、光驱等，当识别后，linux会把识别的其它设备挂载到这个目录下。
* /mnt [常用] 系统提供该目录是为了让用户临时挂载别的文件系统；我们可以将外部的存储挂载到/mnt下，别人的设备关挂载到这个目录下。
* /opt 给主机额外安装软件所拜访的目录 。
* /var 这个目录中存放着在不断扩充着的东西，习惯将经常被修改的目录放在这个目录下，包括各种日志文件。
* /selinux [security-enhanced linux] SELinux是一种安全子系统，它能控制程序只能访问特定文件，有三种工作模式，可以自行设置。
* /lost+found 这个目录一般情况下是空的，当系统非法关机后，会存放一些文件。


vi和vim编辑器
=======================

* 按下i、I、o、O、a、A、r、R等任何一个字母进入编辑模式
* 复制当前行 yy,复制当前行向下5行 5yy,并粘贴（输入p）.
* 删除当前行 dd,删除当前行向下5行 5dd.
* 在文件中查找某个单词 /查找的单词,回车查找,输入n查找下一个.
* 设置和取消文件的行号, :set nu 和 :set nonu.
* 编辑/etc/profile文件,使用快捷键到该文档的最末行[G]和最首行[gg].
* 在一个文件中输入“Hello”,然后又撤销这个动作[u].
* 编辑/etc/profile文件,并将光标移动到20行,一般模式下输入20再按[shift+g].
* :wq 保存并退出   :q 退出  :wq! 强制保存并退出   :q!强制退出
* ESC 退出编辑模式


开机、重启和用户登录注销
==========================



* shutdown -h now   立刻关机
* shutdown -h 1     通知登录用户，1分钟后关机
* shutdown -r now   立刻重启
* halt              关机，作用和上面一样
* reboot            立刻重启
* sync              把内存的数据同步到磁盘
* 不管是重启系统还是关闭系统，首先要运行sync命令，把内存中的数据写到磁盘中。
* 目前shutdown/halt/reboot等命令均已经在关机前进行了sync。不过小心使得万年船。
* su - 用户名        命令来切换账户
* logout            注销账户，在图形界面运行无效，在运行级别3时有效。

用户管理
=======================

添加用户
---------

* useradd 用户名 // 创建用户，创建用户会同时按用户名创建用户组，删除用户时，会同时删除这个用户组，但是专门制定的用户组不会被删除，
* useradd -d /root/haha 用户名 // 指定家目录
* useradd -g 用户组 用户名 // 增加一个用户，直接将它指定到用户组

* userdel 用户名 // 删除用户，保留家目录
* userdel -r 用户名 // 删除用户，-r删除家目录

* groupadd 用户组 // 新增用户组
* groupdel 用户组 // 删除用户组

* passwd 用户名 // 修改用户密码
* pwd  查看当前所在目录
* id 用户名 // 查询用户的信息
* su - 用户名 // 切换用户，高权限到低权限用户不用输入密码
* su 用户名 // 不是很规范的切换用户方式，不加-，不显示上一次登录时间。
* whoami // 查看当前登录用户
* who am i // 查看第一次登录用户详细信息，切换用户后依然显示第一次登录的用户

* /etc/passwd文件
    - 用户(user)的配置文件，记录用户的各种信息
    - 每行的含义：用户名：口令：用户标识号UID：组标识号GID：注释性描述：主目录：登录Shell
    - 口令为x,真正的口令加密存放在/etc/shadow中
* /etc/shadow文件
    - 口令的配置文件
    - 每行的含义：用户名：加密口令：最后一次修改时间：最小时间间隔：最大时间间隔：警告时间：不活动时间：失效时间：标志
* /etc/group文件
    - 组(group)的配置文件，记录Linux包含的组的信息
    - 每行的含义：组名：口令：组标识号GID：组内用户名列表


实用指令
==============

指定运行级别
--------------

| 常用的运行级别是3和5，也可以指定运行级别。
| 指令：init[0123456]
| 也可以修改配置文件/etc/inittab

运行级别说明：
* 0：关机
* 1：单用户（找回丢失密码）
* 2：多用户状态没有网络服务
* 3：多用户状态有网络服务
* 4：系统未使用保留给用户
* 5：图形界面
* 6：系统重启

CentOS7后运行级别说明
------------------------

在centos7以前，级别配置信息在/etc/inittab文件中，
centos7开始，简化如下：

| multi-user.target:analogous to runlevel 3
| graphical.target:analogous to runlevel 5

* systemctl get-default // 查看当前运行级别
* systemctl set-default xx.target // 设置运行级别，重启生效

帮助指令
----------

* man [命令或配置文件] // 获得帮助信息
* help 命令 // 获得shell内置命令的帮助信息
* info

文件目录指令
--------------

* pwd // 显示当前工作目录的绝对路径
* ls [选项] [目录或文件] // 查看目录或文件信息
    - -a:显示当前目录所有的文件和目录，含隐藏的
    - -l:以列表的方式显示信息
    - ll:通 ls -l ，ls -l 指令的别名,在命令行用alias ll=ls -l  配置，也可以在配置文件在.bashrc添加


例行行工作与任务调度
=======================

Linux工作调度的种类：at,crontab

at:at是个可以处理仅执行一次就结束调度的命令，不过要执行at时，必须要求atd这个服务的支持，在某些新版的distributions中，atd可能默认没有启动，那么at命令就会失效，不过CentOS默认是启动的。

crontab:crontab所设置的任务将循环一直进行下去，除了使用crontab命令执行外，也可以编辑/etc/crontab文件来支持，让crontab生效则需要crond这个服务支持。

-e 编辑任务
-l 查询任务
-r 删除任务

crontab -e // 编辑任务调度，保存后退出，及生效，重启电脑依然生效，应该是写入了某文件之中



磁盘与目录
=======================


* lsblk 查看所有分区挂载情况
* lsblk -f 查看所有分区挂载情况 -f显示具体参数
* df -h 查看系统整体磁盘使用情况
* du -h /目录     // 查询指定目录的磁盘占用情况
    - -s 指定目录占用大小汇总
    - -h 带计量单位
    - -a 含文件
    - -c 列出明细的同时，增加汇总值
    - --max-depth=1 子目录深度
* ls -l /opt | grep "^-" | wc -l        // 统计/opt文件夹下文件的个数
* tree  //以目录显示   如果没有yum install tree安装，

网络配置
=======================

* /etc/sysconfig/network-scripts/ifcfg-eth0 网卡ip等配置文件，不同网卡最后的命名不一样
* service network restart              // 修改网络配置后，重启网络服务
* hostname      查看主机名

进程
=======================
ps

* -e 显示所有进程
* -f 全格式
* -a
* -u 
* -x

ps -ef 查看进程
ps -aux 常用经常查看命令


终止进程kill和killall

kill [选项] 进程号 // 通过进程号终止进程
killall 进程名称 // 通过进程名终止进程，也支持通配符，这在系统因负载过大而变得很慢时很有用。

[选项]
* -9 强制终止进程

案例

* 

pstree 查看进程数
-p 显示进程号
-u 显示进程用户

服务(service)管理
=======================

基本介绍
---------

服务(service)本质就是进程，但是是运行在后台的，通常都会监听某个端口，等待其他程序
的请求，比如(mysqld,sshd,防火墙等)，因此又称为守护进程，是Linux中非常重要的知识点。

service管理指令
------------------

* service 服务名 [start|stop|restart|reload|status]
* 在CentOS7.0后很多服务不再使用service，而是systemctl。
* service指令管理的服务在/etc/init.d目录下查看
* ls -l /etc/init.d // 查看service管理的服务
* setup // 命令查看所有服务，带*号的为随系统启动

systemctl 命令
---------------

* 基本语法:systemctl [start|stop|restart|status] 服务名
* systemctl指令管理的服务在/usr/lib/systemd/system目录下查看
* systemctl list-nuit-files [| grep 服务名] // 查看服务开机启动状态，grep进行过滤
* systemctl enable 服务名 // 设置服务开机启动，永久生效，在3/5级别生效
* systemctl disable 服务名 // 关闭服务开机启动，永久生效，在3/5级别生效
* systemctl is-enabled 服务名 // 查询某个服务是否是自启动





systemctl get-default // 查看当前运行级别

systemctl set-default graphical.target // 设置当前级别为图形化级别，也就是级别5


chkconfig 命令

* 通过命令可以给服务的各个运行级别设置自 启动|关闭
* chkconfig指令管理的服务在/etc/init.d查看
* 注意：在CentOS7.0后，很多服务使用systemctl管理
* chkconfig重新设置服务自启动和关闭，需要重新启动reboot生效。

chkconfig --list 查看服务
chkconfig 服务名 --list 查看某服务
chkconfig --level 5 服务名 on|off 设置某服务在5级别下自启动|自关闭

rpm包的管理
=======================

* rpm -qa  // 查询所有安装的rpm软件包
* rpm -q 软件包  // 查询是否安装某软件包
* rpm -qi 软件包名  // 查询某软件包详细信息
* rpm -qf 文件全路径 // 查询文件所属的软件包，也就是文件由那个软件所生成的
* rpm -qf /etc/passwd // 查/etc/passwd 由那个软件包生成
* rpm -e 软件包 // 删除软件包，如果该软件包被依赖，将提示
* rpm -e --nodeps 软件包 // 强制删除软件包

* rpm -ivh 软件包全路径名称   // 安装软件包 i=install安装 v=verbose提示 h=hash进度条

yum
=======================

yum是一个Shell前段软件包管理器，给予RPM包管理，能够从指定的服务器自动下载RPM包并且安装，
可以自动处理依赖性关系，并且一次安装所有依赖的软件包。

yum list | grep xx xx软件列表
yum install xxx 下载xxx安装，并安装所有的依赖包


* netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1 | sort -nr


* top // 查看内存
* iotop // 查看io读写
* df -lh // 查看磁盘存储
* netstat -tunlp // 查看端口占用
* lsof -i // 查端口占用
* ps -aux | grep xx进程 // 查看关心的xx进程

















Linux下常见文件介绍
=======================

| d /dev/dri 独立显卡驱动相关(unraid)。

| d /etc/init.d             服务service所在目录
| - /etc/passwd             用户相关信息
| - /etc/shadow             密码相关信息
| - /etc/group              用户组相关信息
| - /etc/crontab            任务调度与例行性工作相关
| - /etc/cron.deny          不允许使用cron调度指令的用户，一个用户一行
| - /etc/fstab              永久挂载磁盘、U盘等，添加完成后执行mound -a 即可生效
| - /etc/sysconfig/network-scripts/ifcfg-eth0   网卡ip等配置文件，不同网卡最后的命名不一样
| - /etc/hostname           主机名
| - /etc/inittab            运行级别相关信息
| - /etc/profile            设置环境变量
| - /etc/rsyslog.conf       日志相关 CentOS7
| - /etc/logrotate.conf     全局的日志轮替策略、规则，也可以单独给某个日志文件指定策略

| - /var/log/wtmp 用户登录数据记录,该文件是一个data file，能通过last命令读取，但是使用cat会读出乱码，属于一种特殊格式的文件(CentOS 5.x)。

| d /usr/lib/systemd/system systemctl指令管理的服务在/usr/lib/systemd/system目录下查看


Linux下常见服务介绍
=======================

* atb                       at任务调度与例行性工作服务
* crond                     crontab任务调度与例行性工作服务









Linux下常用命令
=======================

Linux ln 命令
-----------------------

.. code::

   ln [参数][源文件或目录][目标文件或目录]
   ln [源文件][目标文件或目录] // 硬链接，源文件只能是文件，目标可以是目录，即不更改文件名，不可以跨文件系统和硬盘。
   ln -s [源文件或目录][目标文件或目录] // 软链接，相当于windows下快捷方式，可以跨文件系统，跨硬盘。





























