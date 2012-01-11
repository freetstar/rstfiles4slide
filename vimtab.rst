vim中的tab和space
=================

常见的tab设置们
````````````````

一一解说

1. expandtab|et    [off|on] 
    
   默认值为off.当为on时，在插入模式下,按[TAB]键时会以一定数量的[SPACE]键代替。若希望插入真正的
   TAB的话，按CTRL-V<Tab>。同时，若autoindent=on，使用[<]和[>]键来缩进,插入的也是一定数量
   [SPACE]键。

2. shiftwidth|sw   [数字]
   
   默认值为8.每次缩进插入的[SPACE]数量.当'cindent',[>>],[<<],[<],[>]时使用

3. tabstop|ts   [数字]

   默认值为8.文件中的[TAB]键被 :strong:`当做` [SPACE]键的数目。

4. smarttab|sta   [off|on]

   默认值为off。off时[TAB]键将依据"tabstop"或"softtabstop"插入[SPACE].而"shiftwidth"仅用在
   左右平移文本时。
   on时,在插入行前按下[TAB]键时将根据'shiftwidth'插入相应的空白符。"tabstop"或'softtabstop'
   此时就用在别处.[BS]键则会删除行首对应‘shiftwidth’数的空白字符

5. softtabstop|sts   [数字]

   默认值为0.在文档编辑操作时，像[BS]键和[TAB]键被:strong:`当做` "softtabstop"个[SPACE]键使用.
   此给人感觉虽然是[TAB]键被插入了,但实际上是[SPACE]和[TAB]的混合体。[x]键仍然是一个个字符产生作用。

好吧，我怎么知道代码里到底是[SPACE]还是[TAB]
``````````````````````````````````````````````

- list模式可将不可以打印的字符以^代替，如[TAB]和[SPACE]等空白字符，同时每行末添加$
  
    set list

- 使用listchars来改变list模式下显示的字符
  listchars关于[TAB]的设置默认模板为tab:xy,其中x只显示一次，y则占有剩余的空间
    
    set listchars=tab:>-,eol:$,同时tab默认占4个空格时，tab就显示为>---，每行末尾显示为$

效果如图:

.. image:: listchar.jpg
    :align: center
  
为了方便，可以添加这个到你的vimrc中，

::

    " 用来打开list功能，显示不可见字符
    nmap <leader>l :set list!<CR>
    " 设置为>-格式,用$结尾
    set listchars=tab:>-,eol:$

我是肿么干的
```````````````````

采用vim推荐的方案之一

::

	2. Set 'tabstop' and 'shiftwidth' to whatever you prefer and use
	   'expandtab'.  This way you will always insert spaces.  The
	   formatting will never be messed up when 'tabstop' is changed.

具体设置

::

    set tabstop=4
    set shiftwidth=4
    set expandtab
    set softtabstop=4
    set smarttab

这种方案下，所有[TAB]键均以softtabstop个[SPACE]键代替，也就是基本上么有[TAB]键会在文档里出现了,
都采用[SPACE]键替代了。

当然，如果不愿意每一种代码都采用这样的配置方式，还可以在~/.vim/ftplugin/下新建python.vim，添入

::

    setlocal tabstop=4
    setlocal shiftwidth=4
    setlocal expandtab
    setlocal softtabstop=4
    setlocal smarttab


要是遇到和你喜好不一样的同学怎么办
```````````````````````````````````

很多时候大家写代码时对[TAB]和[SPACE]的习惯不一样，有的同学喜欢4个空格代替一个tab，有的同学喜欢到处是
tab，这种情况下，可能有时候遇到像c这种以{}来管理语句块的还好，但是一遇到python这种以缩进来处理语句块
的语言，空格和tab的使用，tab用多少空格来替代不同习惯的影响就很大了

看这个优酷下载的项目时，git://github.com/freetstar/youku-lixian.git，clone下来，gvim youku.py
很简单的做一个print 调试，发现一直提示我语法错误，最终发现原来作者用的占8位的[TAB]做缩进的,那我直接[o]
开启新的一行时，很自然地我的新行是以我自己的设置，即空格做缩进的，自然要报错误

看看python对代码格式的要求吧： http://www.python.org/dev/peps/pep-0008/

::

    Use 4 spaces per indentation level.

    For really old code that you don't want to mess up, you can continue to
    use 8-space tabs.
     
    Never mix tabs and spaces.

    The most popular way of indenting Python is with spaces only.  The
    second-most popular way is with tabs only.  Code indented with a mixture
    of tabs and spaces should be converted to using spaces exclusively

**:(遇到python缩进不一直的情况怎么办!**

解决办法:输入 :strong:`":retab"`

格式：

::

    [range]ret[ab][!] [new_tabstop]

用法：

::

    配合expandtab设置，将所有[TAB]键用tabstop个的[SPACE]来替代，如果没有指定tabstop值或者等于0，
    则使用目前的vim配置中tabstop值

**做个好人，告诉vim咱想怎么做**

在代码中指定想要的vim设置，如"/* vim: tabstop=8:softtabstop=8:shiftwidth=8:noexpandtab*/"

这样一来，下次无论是谁用vim改动代码时，vim都会自动读取代码中关于vim的配置！


晕了没，其实我也很。。。。。。。。。。。。
``````````````````````````````````````````````

- 这个还是比较形象的，讲vim中tab和space故事的一段视频，
    http://media.vimcasts.org/videos/2/tabs_and_spaces.ogv

- 复杂的解释
    http://blog.chinaunix.net/space.php?uid=16444831&do=blog&id=2742643

- vimwiki的介绍
    http://vim.wikia.com/wiki/Converting_tabs_to_spaces

- 一个关于vim不错的网站，用视频来解释im_.

.. _vim: http://vimcasts.org/

参考文档:

http://tedlogan.com/techblog3.html

http://www.imkeke.net/vim-2/vim-tab-config.html
