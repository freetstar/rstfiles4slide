Linux ToolChain
=================

-----------------------------------------------------------------------

Tools
======
* 编译器
* 连接器
* 汇编器
* 调试器

-----------------------------------------------------------------------

1 Linux 开发过程
====================

-----------------------------------------------------------------------


1.1 Source Code
==================

|


常见的 :strong:`源代码` 都是压缩好的包：

.. sourcecode:: bash

    foobar.tar.gz   foobar.tar.bz2 
    
.. 原来是这样添加空行的哈

|


|

围观下 :strong:`Codeblock` 的源码包结构:

.. sourcecode:: python

   $tar jxvf  codeblocks-10.05-release.tar.bz2
   $ls
    acinclude.m4  ChangeLog            COMPILERS     debian       missing
    aclocal.m4    codeblocks.pc.in     config.guess  depcomp      NEWS
    AUTHORS       codeblocks.plist     config.sub    install-sh   README
    bootstrap     codeblocks.plist.in  configure     ltmain.sh    revision.m4
    BUGS          codeblocks.spec      configure.in  Makefile.am  src
    BUILD         codeblocks.spec.in   COPYING       Makefile.in  TODO


-----------------------------------------------------------------------

1.2 GNU Autoconf
=======================

:strong:`Tool` :configure

:strong:`目的` ：配置本地编译环境（硬件环境和软件环境）

:strong:`运行` `configure` 来检查:

1）系统是否安装必要的编译环境

2）系统是否安装源码编译时需要的库以及库的版本是否正确

:strong:`运行` ：

.. sourcecode:: python

    $./configure
    checking for gcc... gcc
    ... ...
    configure:creating Makefile

:strong:`帮助` ：

.. sourcecode:: python

    $./configure --help
    `configure' configures codeblocks 10.05-release to adapt to many kinds of systems.

    Usage: ./configure [OPTION]... [VAR=VALUE]...
    ... ...

|

-----------------------------------------------------------------------

1.3 GNU make
===================

:strong:`Tool` :make

:strong:`目的` ：编译源代码

:strong:`过程` `make` :

1） 读取Makefile文件

2） 根据Makefile确定调用命令的顺序并编译指定源代码

:strong:`运行`:

.. sourcecode:: Python

    make

有时，Makefile由其他自动工具产生的，但是通常都由configure产生

-----------------------------------------------------------------------

2 GNU工具链的组成
=====================

-----------------------------------------------------------------------

2.1 GNU 编译器集
==================

* GNU编译器集可以支持很多语言

.. sourcecode:: python
    
    c/c++/Ada/Fortran/Objective c/Java ... ...

* 自由软件
* GCC/G++ 易用性


.. 本文着重以GCC做为C编译器和C源代码为例子

:strong:`本质` ： GCC是实际上仅仅是一个C编译器，仅将代码输出为汇编代码 
                  不包含汇编器或连接器，不做多余的事情(KISS)


-----------------------------------------------------------------------

2.1.1编译单个源文件
===================

GCC的前端gcc驱动程序，会执行GNU汇编器和连接器来执行汇编和链接

.. sourcecode:: python
  
   $vim hello.c
   #include <stdio.h>
   #include <stdlib.h>

   int 
   main(int argc,char ** argv)
   {
        printf("Hello,World!\n");
        exit(0);
   }

编译运行

.. sourcecode:: python

    $gcc -o hello hello.c
    $./hello
    Hello,World!

注：默认的可执行文件名为a.out ,使用-o 指定可执行文件名

-----------------------------------------------------------------------

2.1.2编译多个源文件
=====================

gcc不仅可以编译一个源文件，其还可以适当地调用GNU连接器，可以将不同的目标文件链接成可执行程序

写一个简单的消息打印函数：

.. sourcecode:: python
    
    $vim message.c
    #include <stdio.h>
    
    void
    goobye_world(void)
    {
        printf('Goodbye,World!\n');
    }

尝试编译会出错

.. sourcecode:: python

    $gcc -o goodbye message.c
    ... ...
    /usr/lib/gcc/i686-pc-linux-gnu/4.6.1/../../../crt1.o: In function `_start':
    (.text+0x18): undefined reference to `main'
    collect2: ld returned 1 exit status

转换为目标代码.o文件即可，方法：

.. sourcecode:: python
   
   $gcc -c message.c  /*使用-c选项来支持库代码*/

-----------------------------------------------------------------------

2.1.2编译多个源文件(续)
=======================

编写main.c调用goodbye_world

.. sourcecode:: python
    
   $vim main.c
   #include <stdlib.h>
    
   void googbye_world(void);

   int 
   main(int argc,char ** argv)
   {
        goodbye_world();
        exit(0);
   }
    
GCC编译此程序

.. sourcecode:: python

    $gcc -c main.c  /*产生main.o目标文件*/
    $ls
    main.c message.c main.o message.o 
    $gcc -o goodbye main.o message.o /*产生goodbye可执行文件*/
    $./goodbye
    Goodbye,World!

其实可以简化为一条命令

.. sourcecode:: python

    gcc -o goodbye message.c main.c

-----------------------------------------------------------------------

2.1.3 使用外部函数库
============================

几乎每一个linux应用程序都依赖于GNU C函数库GLIBC提供的库。此库包含了如I/O库，print函数，exit函数。在使用GCC执行编译时，GCC :strong:`默认情况` 下在链接阶段将假设GLIBC被包括进程序中，所以需要在源代码中做函数声明。
  
下面的源代码 testmath.c

.. sourcecode:: c

    #include <stdio.h>
    #include <stdlib.h>
    #include <math.h>

    int 
    main(int argc,char ** argv)
    {
        double angle = 30.0;
        printf("sin(%e) = %e\n",angle.sin(angle));

        return 0;
    }

编译：

.. sourcecode:: python

   $gcc -o trig -lm testmath  #在编译时添加lm选项，表示链接系统中的数学库


-----------------------------------------------------------------------

2.1.4 linux系统函数库
=========================

Linux系统中函数库有2种类型： :strong:`共享（shared）`  :strong:`静态(static)` 

* 静态库

  程序用到的函数库在编译时，会被直接包含进到最终的二进制程序中, 也就是说每个二进制程序都包含了其必须的库。

* 共享库

  共享库是唯一的，程序在需要时链接此共享库。程序本身不包含此库。

  :strong:`优点` :
       * 减少了程序本身的大小和对内存的占用（程序只需要链接一个库即可）
       * 当共享函数库出现安全问题，一处修改，到处安全
       * 被许多程序同时调用的共享函数库很可能驻留内存时间很长，而不是放在磁盘的交换分区 

-----------------------------------------------------------------------

2.1.4.1 创建共享函数库
==========================

:strong:`例子`

.. sourcecode:: python
    
    $gcc -fPIC -c message.c 
    /* PIC选项告诉GCC不要包含对函数和变量具体内存位置的引用，
      产生的message.o用来建立共享函数库  */
    $gcc -shared -o libmessage.so message.o
    /*-shared 表示共享，-o表示生成的共享函数库文件名*/
    $gcc -o goodbye -lmessage -L. main.o
    /* -lmessage表示通知GCC驱动程序在链接阶段引用共享函数库libmessage.so 
       -L. 表示共享库位于当前目录*/

通常linux会自动在程序需要时寻找必要的共享函数库:
  :strong:`ldd` 命令用来在标准系统函数库路径中显示程序的所需函数库的版本

.. sourcecode:: bash

    $ldd /usr/bin/awk 
        linux-gate.so.1 =>  (0xb77db000)
        libdl.so.2 => /lib/libdl.so.2 (0xb77af000)
        libm.so.6 => /lib/libm.so.6 (0xb7783000)
        libc.so.6 => /lib/libc.so.6 (0xb75e1000)
        /lib/ld-linux.so.2 (0xb77dc000)

3 :strong:`ldd` tips:

1) /etc/ld.so.conf 此文件可以指定一些共享库的寻找位置

2) LD_LIBRARY_PATH 此变量用来指定ldd寻找的共享库路径 \
   //you can hack it :export LD_LIBRARY_PATH=LD_LIBRARY_PATH:`pwd`

3) ldconfig :在安装好系统之前不存在的库后，需要运行此命令更新共享库的信息
  
-----------------------------------------------------------------------

2.1.5 GCC常用选项
=====================

=============         ===============================================================
 -c                   告诉GCC只执行编译和汇编而不链接
-------------         ---------------------------------------------------------------
 -s                   在执行玩编译之后就停止并输出汇编语言代码
-------------         ---------------------------------------------------------------
 -ansi                禁止使用与C90规范不兼容的某些GCC特征
-------------         ---------------------------------------------------------------
 -std                 -std=c89使用C89 ANSI C语言规范
-------------         ---------------------------------------------------------------
 -fnobuiltin          禁止使用GCC内置的如memcpy，printf函数
-------------         ---------------------------------------------------------------
 -Wall                启动了绝大多数警告选项，并将产生冗长的输出
-------------         ---------------------------------------------------------------
 -g                   用来增加调试信息 //常与-Wall一起使用
-------------         ---------------------------------------------------------------
 -O{0,1,2,3}          0不进行优化，1,2,3级优化等级逐渐增高  
-------------         ---------------------------------------------------------------
 -Os                  对可执行文件的大小进行优化
-------------         ---------------------------------------------------------------
 -march               要求GCC针对特定的cpu模型生成代码，其中将包含特定模型的指令 
-------------         ---------------------------------------------------------------
-msoft-float          要求GCC不使用硬件浮点运算指令，常用于嵌入式设备编译软件 
-------------         ---------------------------------------------------------------
man gcc               查看更多的文档帮助
=============         ===============================================================


-----------------------------------------------------------------------

2.2 GNU二进制工具集
====================

-----------------------------------------------------------------------

2.2.1 GNU汇编器as
==================

作用：把已编译的C代码（以汇编语言形式）转换为能够在特定目标处理器上执行的目标代码

例子：

.. sourcecode:: python
    
    $gcc -S hello.c
     /*用-S表示产生汇编代码文件hello.s*/
    $cat hello.s
    ... ...
    call puts
    ... ...
    /*call puts表示对外部函数库的调用，这部分涉及到GNU连接器*/
    $as -o hello.o hello.s
    /*汇编源代码hello.s,产生目标代码文件*/

GNU汇编器as支持许多不同种类的微处理器，当然包括Intel IA32（俗称x86） 

-----------------------------------------------------------------------

2.2.2 GNU连接器ld
==================

源代码=>编译=>汇编代码=>汇编=>目标代码=>连接器=>可执行文件

|

可执行文件必须是要被目标Linux系统理解的标准容器格式。目前是ELF（Executable and Linking
Format）可执行和链接格式。它既是目标代码和应用程序的文件格式的选择,也是GNU Id的选择

|

ELF 包含了许多段落，其中包含了程序自身的代码段和数据段以及各种和应用程序本身相关的元数据。


:strong:`连接器的操作`


遵循连接器脚本（/usr/lib/ldscripts文件夹下）的预编写命令来处理目标代码文件,并产生需要的输出


-----------------------------------------------------------------------

2.2.3 GNU objcopy和objdump
===========================

:strong:`objdump` 作用：查看可执行文件的内容

.. sourcecode:: python
    
    $objdump -x -d -s hello
    /* -x 显示二进制文件hello的所有头
       -d 试图反汇编任一可执行段落的内容
       -s 将程序的源代码与其对应的反汇编代码混合显示
       可能要求编译时加-g并没有进行任何GCC指令调度优化*/
    
    hello:     file format elf32-i386 //32位的elf格式，i386目标文件
    hello
    architecture: i386, flags 0x00000112:
    ... ...

:strong:`objcopy` 作用:从一个文件拷贝目标代码到另一个文件，并在过程中做各种转换

-----------------------------------------------------------------------

2.3 GNU Make
================

:strong:`作用` ：遵循一系列的规则以确定对一个大型项目中每个单独源文件必须执行的动作，是一个依赖性跟踪工具。简单来说就是编译规则

.. sourcecode:: python
    
    #Makefile example

    CFLAGS := -Wall -pedantic-errors

    all:hello goodbye trig

    clean:
            -rm -rf  \*.o  \*.so  hello goodbye trig
    hello: 

    goodbye: main.o message.o
    
    trig:
        $(cc) $(CFLAGS) -lm -o trig trig.c

解释：

- 默认动作all试图通过针对每个示例程序的规则来编译这三个程序

- ello没有定义任何依赖关系，则将hello.c编译为可执行文件hello

- goodbye:需要main.o message.o两个依赖文件，意味着这两个文件首先要被处理

- trig: 相当于cc -Wall -pedantic-errors -lm -o trig trig.c



-----------------------------------------------------------------------

2.4 GNU调试器gdb
===================

:strong:`注意` :程序在编译时必须添加-g调试标记

用法:

.. sourcecode:: python
    
    $gdb hello
    /*调试hello可执行文件*/
    (gdb)list
    /*列出部分代码*/
    (gdb)break main
    /*在main函数处添加断点*/
    (gdb)run
    /*开始运行程序*/
    (gdb)next
    /*单步执行*/
    (gdb)print 变量
    /*查看变量的值*/
    (gdb)continue
    /*程序一致运行至一个断点或者至程序结束*/
    (gdb)help
    /*获取帮助*/

GDB另外一个非常重要的作用是调试core dump

其包含了程序崩溃时包含程序当时状态的文件，用来确定崩溃的具体情况，可以理解为飞机的黑匣子

-----------------------------------------------------------------------

2.5总结
======================

* GNU make:编译和构建源代码的自动化工具
* GNU Compiler Collection(GCC):一系列编程语言编译器
* GNU Binutils: 连接器，汇编器和其他工具
* GNU Bison : 语法解析生成器
* GNU m4: m4 宏处理器
* GNU Debugger(GDB): 代码调试器
* GNU build system(autotools):
  Autoconf Autoheader Automake Libtool


-----------------------------------------------------------------------

2.6 
=======================

文中有不正确的地方请指出
lgxwqq[#]gmail.com

参考:

1 Linux高级程序设计

2 GNU Toolchain

http://en.wikipedia.org/wiki/GNU_toolchain

--------------------------------------------------------------

End
========
