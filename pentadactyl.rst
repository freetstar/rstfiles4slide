Pentadactyl
=================

Firefox XXOO vim ==> Pentadactyl 


----------------------------------

Modes
=====

* Normal ->default
* Command Line 
    * Ex -> starts with ":" ->standard mode for entering commands
    * Find ->寻找模式
    * Hints ->线索模式
* Insert  Mode(text区域)
* Visual Mode(可视化选择）
* Text Edit mode(编辑text区域）
* Operator Mode(移动光标)

----------------------------------

有用的Commandline
==================

<Up> 上一个历史记录

<Down> 下一个历史记录

----------------------------------

Scrolling
==========
* j/k
    scroll window down/up by one line, respectively
   
* h/l
    scroll window left/right

*  <C-f>/<C-b>
    scroll down/up by one page

*  <C-d>/<C-u>
    scroll down/up by 1/2 page

----------------------------------

Motion
=========

gf 显示源码和网页内容之见切换
gF 用editor打开网页源码(:set editor=gvim)
0 网页最左侧
$ 网页最右侧
% 跳转到百分比
gg 网页顶部
G  网页结尾

    

----------------------------------

History in tab
===============

H/L 当前TAB的历史中来回翻滚

<C-o>/<C-i> 当前TAB的历史中前后翻滚

:ju see the history,pass the history number as args

----------------------------------

Tabs
=====

gt/<C-n> 当前TAB的下一个

gT/<C-p> 当前TAB的上一个

g0/g$    所有TAB的第一个和最后一个

d        关闭当前TAB

r        刷新

R        不带Cache强制刷新

Normal.t = Command.tabopen

Normal.o = Command.open

----------------------------------

Hints!!!
===========

Mark the links in numbers,usr f/F to surf!!!

* f open link in current tab

* F open link in another tab

* <CR> 确认

**;** extened hints mode

----------------------------------

rcFile
========

.. sourcecode:: python

    if(vimrc===pentadactylrc){
        console.log("That's RIGHT");
        console.log("^_^");
    }

:mkp 
  one serious problem!it will override the exsit one!

----------------------------------

Exit
=====

* :xall  save session and exit
* :exit  just exit
* ZZ == :xall
* ZQ == :exit

----------------------------------

Where's Firefox
================

* :addo+[TAB] 
  所有的附加组件
* :dialog + [TAB]
   firefox的对话框
* :downl[oads]
* :emenu
  firefox所有菜单栏的入口
* :siderbar

----------------------------------

Restart
========

:reh[ash] [arg] ~ 重载所有Pentadactyl的附加组件，代码，插件，配置等等

:res[tart] [arg] ~ 强迫Firefox重启

----------------------------------

Status line
============

* URL
  当前打开的URL
* History and bookmark
* Tab index
  [N/M] M为TAB总数，N为位置
* Vertical Scroll
  垂直区域的百分比
* Securtiy

   
----------------------------------

Open
=======

:o [args]
   * local filename
   * search engine name
     :open google Linus Torvalds
   * just a string
     :open Linus Torvalds
   * URL
      :open www.freetstar.com

如果有多个参数，第一个在当前tab中打开,其他在新的TAB中打开

----------------------------------

TabOpen
========

* :tabopen[!] [args]
* t
* O 当前TAB打开当前URL==Refresh
* T 新开TAB打开当前URL
* s 打开搜索
* S 在新的TAB打开TAB
* w 在新的窗口中打开
* W 在新的窗口中打开当前标签页
* p 当前tab打开剪切板内的网址
* P 新开tab打开剪切板内的网址

----------------------------------

Navigating
===========

* ~  打开本地用户主目录
* gh 打开ff主页
* gH 在新的tab中打开ff主页
* [count]gu 打开url的第count级
* gU 打开url的顶级

----------------------------------

缩放
=====

* zi 放大
* zm 放大！
* zo 缩小
* zr 缩小！
* zz 恢复

* y 把当前buffer的url放到剪切板中
* Y 把选择的文本放在系统剪切板

----------------------------------

Search
=======

* /{pattern}<CR> 寻找pattern,向下搜索
* ?{pattern}<CR> 往回搜索
* n              找下一个
* N              找上一个
* '*'              向前搜索当前光标下的单词
* #              向后搜索当前光标下的单词
* :noh[lfind]    不高亮搜索

----------------------------------

Automatic Commands
==================

:au[tocmd][!] [events] [filters] [cmd]

    [cmd] js/Ex

    
e.g. :autocmd LocationChange '^https?://(www||mail)\.google\.com/' :normal! <C-z>


----------------------------------

Javascript
=============

:ec[ho] {expr}
   显示表达式的值，函数-》源码 DOM结点->XML，XML->页面，

:echoe[rr] {expr}   
    显示错误信息

:echom[sg] {expr}
    显示为正常信息

:exe[cute] {expr}
    执行命令，:exe "open" + content.location.host
    :exe prompt("just a test")

:javas[cript] {cmd}

.. HERE :javascript<<EOF
    for each (var tab in tabs.visibleTabs)
        tab.linkedBrowser.reload()
    EOF

:js! [context]

:javas[cript]! [context]
    打开javascript解释器,同上，得到一个循环。。有些像python

条件判断

:if {expr} 配对:elseif :else :endif

:en[dif] :if /elseif:/:else


----------------------------------




Bookmarks
==========

❤ -> status line 

a -> add a bookmark
    添加书签， -keyword 可以用在":open"中

A ->改变当前URL的书签状态

:bmarks[!] [filter] ->  列出来符合条件的书签

:delbm+[TAB]
  

----------------------------------

Tips
=====

禁止使用d关闭最后一个tab后关闭整个窗口
    :set! browser.tabs.closeWindowWithLastTab=false

:dialog searchengines 更改默认搜索引擎

:pass through gmail

.. sourcecode:: python

    set passkeys='mail\.google\.com':c/jkhnpouelxsfra#`[]z?\*nrtgidIU+-=<Tab><Return>'
  

----------------------------------

Over&&THANKYOU

