.. :Author: ZQ
   :Contact: fdevilpublic@163.com
   :Revision: 1.0.0
   :Created Date: 2021-01-26
   :Modified Date:
   :Status: First draft
   :Copyright: This document has been placed in the public domain.
   
==============================================================
Python+Sphinx+reStructuredText+github+ReadTheDocs写技术文档
==============================================================
:Date: 2020-07-26

.. contents:: 目录
   :depth: 3

前言
=====

这是第一次写博文，起源于一次Linux系统的学习。学习过程中想把笔记记下来，防止忘记，意外在网上发现
``sphinx+reStructuredText+github+readthedocs`` 写技术文档的各类资料博客，立刻被其强大的功能吸引，
在后来的一段时间里，翻阅了无数的中文、英文（英文不行，全靠谷歌）资料，从头到尾验证了从 
:guilabel:`Python`、:guilabel:`pip`、:guilabel:`Sphinx`、:guilabel:`reStructuredText(rst)`、
:guilabel:`github`、:guilabel:`ReadTheDocs` 的全过程。在这里把所学的知识、所遇到的困难、
所解决的问题记录下来。博文借鉴于各处，如有侵权，请联系本人删除。

简介
======

什么是Sphinx?
---------------

**Sphinx 是Python下Docutils项目中的是一种文档工具，使用 reStructuredText 作为标记语言。使用Sphinx需要安装Python环境。**

Sphinx可以令人轻松的撰写出清晰且优美的文档, 由 Georg Brandl 在BSD 许可证下开发。新版的Python文档 就是由Sphinx生成的，并且它已成为Python项目首选的文档工具,同时它对 C/C++ 项目也有很好的支持; 并计划对其它开发语言添加特殊支持. 本站当然也是使用 Sphinx 生成的，它采用reStructuredText! Sphinx还在继续开发. 下面列出了其良好特性,这些特性在Python官方文档中均有体现:

- 输出格式：HTML（包括Windows HTML帮助），LaTex（PDF), ePub, Texinfo, manual pages（man 文档）, 纯文本。
- 广泛的交叉引用：语义标记和函数，类，引用，术语和类似信息的自动链接。
- 层次结构：轻松定义文档树，自动链接到同级/父级/下级文章。
- 自动索引：通用索引，以及用于特定语言的模块索引。
- 代码处理： 使用Pygments 自动高亮显示。
- 扩展： 自动测试代码片段，包含Python模块中的文档字符串（API文档）等。

什么是Markdown、reStructuredText?
----------------------------------

**reStructuredText** 也是轻量级标记语言。扩展名为 ``.rst`` 的纯文本文件，含义为"重新构建的文本"，简称为：RST或reST；是Python编程语言的Docutils项目的一部分，该项目类似于Java的JavaDoc或Perl的POD项目。Docutils 能够从Python程序中提取注释和信息，格式化成程序文档。

- 易于阅读的，所见即所得。
- 对于内联程序文档，快速创建简单的网页以及独立文档很有用。
- 是对StructuredText和Setext轻量级标记系统的修订和重新解释。

**Markdown** 是一种轻量级标记语言，拓展名为 ``.md`` 的纯文本文件。比reST更简单，它允许人们使用易读易写、所见即所得的纯文本格式编写文档。在 2004 由约翰·格鲁伯（John Gruber）创建。Markdown就是个text-to-HTML的工具。目前简书、知乎、github、csdn等都支持并采用markdown编辑博文。[#makedown]_

.. tip:: reST的功能要比 Markdown 多很多。最重要的不同在于 Markdown 只输出html，而reST可以转换为html、ptf、Epub等其他格式。简单的说Markdown用来写文章，reST用来写书。
 


什么是Git、github、ReadTheDocs?
-------------------------------

Git是一个分布式版本控制系统（Version Control System，VCS）。SVN, CVS这类早期的集中式版本控制系统，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。

github是一个非常适合程序员交流的网站，是最大的同性交友平台。是纯代码托管网站。很多国际上的技术个人、企业都在github上有自己的开源代码，只要申请个人账号就可以随意的看到这些大牛写的程序。同时国内的很多互联网公司如百度，阿里等，也在github上公布有开源的代码。国内类似github有**码云Gitee** 。


安装Python
===========

安装Sphinx
===========

reStructuredText语法
====================

github托管文档
==============

git的使用
-----------

ReadTheDocs部署文档
===================

ReadTheDocs自动配置文档
-----------------------

ReadTheDocs手动配置文档
-----------------------

引用文献
========

.. [#什么是rst] https://www.jianshu.com/p/0dc1eb6feea6

.. [#makedown] https://www.runoob.com/markdown/md-tutorial.html
.. [#什么是rst1] file:///D:/%E8%BD%AF%E4%BB%B6/python3.8.3/sphinx+reStructuredText%E5%88%B6%E4%BD%9C%E6%96%87%E6%A1%A3%20-%20LinuxPanda%20-%20%E5%8D%9A%E5%AE%A2%E5%9B%AD.html
.. [#什么是rst2] https://www.jianshu.com/p/0dc1eb6feea6
.. [#什么是rst3] https://www.jianshu.com/p/0dc1eb6feea6
.. [#什么是rst4] https://www.jianshu.com/p/0dc1eb6feea6
.. [#什么是rst5] https://www.jianshu.com/p/0dc1eb6feea6