.. :Author: ZQ
   :Contact: fdevilpublic@163.com
   :Revision: 1.0.0
   :Created Date: 2021-01-27
   :Modified Date:
   :Status: First draft
   :Copyright: This document has been placed in the public domain.


======================
Linux常见命令及用法
======================
:Date: 2021-01-27

前言
======

本文记录了学习Linux过程中所遇到的常用命令及用法。

网络管理
==========

Linux netstat 命令
--------------------

Linux netstat 命令用于显示网络状态。利用 netstat 指令可让你得知整个 Linux 系统的网络情况。

语法
~~~~~~

.. code:: 

    netstat [-acCeFghilMnNoprstuvVwx][-A<网络类型>][--ip]
    
参数说明：
~~~~~~~~~~~

* -a或--all 显示所有连线中的Socket。
* -n或--numeric 直接使用IP地址，而不通过域名服务器
* -p或--programs 显示正在使用Socket的程序识别码和程序名称。
* -t或--tcp 显示TCP传输协议的连线状况。
* -u或--udp 显示UDP传输协议的连线状况。
* -l或--listening 显示监控中的服务器的Socket。

实例
~~~~~~

.. code::
    
    # netstat -a      // 查询详细的网络情况
    # netstat -i      // 查询网卡列表
    
    # netstat -tunlp    // 查看端口占用
    
    # netstat -nap |grep CLOSE_WAIT | grep 32771      // 查询32771端口处于CLOSE_WAIT状态的连接 -p获取进程号，
    如果进程显示为“-” ，则改用lsof -i:端口号  查询端口进程号后利用kill -9 进程号 杀死进程。
    
常见用法
==========

杀死CLOSE_WAIT状态连接
------------------------

#. netstat -nap \| grep CLOSE_WAIT \| grep 32771 // 查询32771端口处于CLOSE_WAIT状态的连接 -p获取进程号，
#. lsof -i:32771                // 查询占用端口32771，的进程号
#. kill -9 进程号               // 杀死进程

* top // 查看内存
* iotop // 查看io读写
* df -lh // 查看磁盘存储
* netstat -tunlp // 查看端口占用
* lsof -i:端口号 // 查端口占用
* ps -aux | grep xx进程 // 查看关心的xx进程