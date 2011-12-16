HTML5
======

--------------

Logo
======

.. image:: ./img/html5-logo.png

--------------

Usage
======

.. image:: ./img/HTML5.jpg

--------------

WHY 
===========

--------------

W3C-world wide web consortium
==============================

* HTML4.0 :
    MIME:text/html 结构松散，标签不严谨


* XHTML1.0 :
    MIME:application/xhtml+xml标签,语法严格


* XHTML1.1 :
   MIME:application/xhtml+xml,全部,xml
   所以很多用户开始以text/html做声明，XHTML写文件


* XHTML2.0 :Never finished 



--------------

.. image:: ./img/fuck_w3c.jpg
   :width: 600
   :height: 400

--------------

The Future of The Web
======================

* Backward compatibility, clear migration path

* Well-defined error handling 

* Users should not be exposed to authoring errors

* Practical use

* Scripting is here to stay

* Device-specific profiling should be avoided

* Open process 

--------------

WHATWG
===========

.. image:: ./img/apple.jpg
    :width: 150    
    :height: 150
    :align: left

.. image:: ./img/Opera.png
    :width: 150    
    :height: 150
    :align: right

.. image:: ./img/firefox.jpg
    :width: 150    
    :height: 150
    :align: center

:strong:`Features`:

*   Web Forms 2.0
*   Web Applications 1.0

--------------

Here it is!!!
===================

* 1991 HTML

* 1997 HTML4

* 1999 HTML4.01

* XHTML1.0+CSS 假XML

* XHTML1.1 XML

* 06/2004 WHATWG 诞生

* 08/2006 W3C和WHATWG合作 将Web Applications 1.0改名为HTML 5

* 2005 AJAX

* 08/2009 W3C关闭XHTML2工作组 

* 2009 HTML5

* 2010/4 Apple block Flash

.. ,有空格

--------------

HTML + CSS3 + Javascript 
=================================


--------------

Canvas
=======

作用：Canvas使用JS在网页上绘图，画布为矩形，多种绘制方法

:strong:`绘制实色图形`

.. sourcecode:: python
    
    <canvas id="myCanvas1" width="200" height="100"></canvas>
    <script type="text/javascript">
        var c=document.getElementById("myCanvas1");
        var cxt=c.getContext("2d");
        cxt.fillStyle="#FF0000"
        cxt.fillRect(0,0,150,75)
    </script>

:strong:`放置图片`

.. sourcecode:: python
    
    <canvas id="myCanvas2" width="200" height="100"></canvas>

    <script type="text/javascript">
        var c=document.getElementById("myCanvas");
        var cxt=c.getContext("2d");
        var img=new Image()
        img.src="flower.png"
        cxt.drawImage(img,0,0);
    </script>

--------------

Video
=======

作用：视频，摆脱第三方插件如Flash

3种视频格式：

* Ogg: Theora 视频编码和 Vorbis 音频编码
* MPEG4: H.264 视频编码和 AAC 音频编码
* WebM: VP8 视频编码和 Vorbis 音频编码

例子

.. sourcecode:: python

    <video src="./movie/big_buck_bunny.webm" controls="controls" >
    </video>

.. raw:: html

    <video src="http://cj-jackson.com/wp-content/uploads/2010/07/big_buck_bunny.webm" width="400" height="200" controls="controls" >
    </video>
    

--------------

Audio
======
作用：音频

3种音频格式：

* MP3
* Ogg
* WAV

例子

.. sourcecode:: python

    <audio src="./movie/audacity_tremolo.ogg" controls="controls">
    </audio>

.. raw:: html

    <audio src="http://cj-jackson.com/wp-content/uploads/2010/07/Ozzy_Osbourne-Scream-Let_It_Die.ogg" controls="controls">
    </audio>
    

--------------

Storage
=========

localStorage
~~~~~~~~~~~~~~ 
特点：没有时间限制

.. sourcecode:: python

    <script type="text/javascript">
        localStorage.lastname="Smith";
        document.write(localStorage.lastname);
    </script>

sessionStorage
~~~~~~~~~~~~~~~

特点：真对一个session进行数据存储，窗口关闭后数据删除

.. sourcecode:: python
    
    <script type="text/javascript">
        sessionStorage.lastname="Smith";
        document.write(sessionStorage.lastname);
    </script>

--------------

Form Input
===========

新增的类型

* email
* url
* number
* range
* Date pickers(date, month, week, time, datetime, datetime-local)
* search
* color

:strong:`email`

.. sourcecode:: python

    E-mail:<input type="email" name="user_email"/>


--------------

Form&&Input Attribute
=====================

+----------------+-------------------+
|   Forms        |    Input          |
+================+===================+
|* autocomplete  |   * autocomplete  |
+                +                   +
|* novalidate    |   * autofocus     |
+                +                   +
|                |   * form          |
+                +                   +
|                |   * form overrides|
+                +                   +
|                |   * height        |
+                +                   +
|                |   * list          |
+                +                   +
|                |   * min,max,step  |
+                +                   +
|                |   * multiple      |
+                +                   +
|                |   * pattern(regexp|
+                +                   +
|                |   * placeholder   |
+                +                   +
|                |   * required      |
+----------------+-------------------+


-----------------

Geolocation
===========
作用:识别地理位置,进一步可以分享

例子

.. sourcecode:: python
    
    <script type="text/javascript">
    function loadDemo() {
        if(navigator.geolocation) {//检测浏览器是否支持Geolocation
            navigator.geolocation.getCurrentPosition(updateLocation);
        }
    }
    function updateLocation(position) {
        var latitude = position.coords.latitude;
        var longitude = position.coords.longitude;
        if (!latitude || !longitude) {           
            return;
        }
        document.getElementById("latitude").innerHTML = latitude;
        document.getElementById("longitude").innerHTML = longitude;
    }
    </script>

--------------

Drag-in 
================

拖拽文件

.. sourcecode:: python

    document.querySelector('#dropzone').addEventListener('drop', function(e) {
      var reader = new FileReader();
      reader.onload = function(evt) {
        document.querySelector('img').src = evt.target.result;
      };

      reader.readAsDataURL(e.dataTransfer.files[0]);
    }, false);


--------------

Semantic content
==================

.. image:: ./img/semantic.jpg

--------------


<!DOCTYPE html>
===============


--------------

CSS3 Borders
=============

Rounded Corners
~~~~~~~~~~~~~~~

.. sourcecode:: python

    div
    {
        border:2px solid;
        border-radius:25px;
        -moz-border-radius:25px;
    } 

Box Shadow
~~~~~~~~~~

.. sourcecode:: python
    
    div
    {
        box-shadow: 10px 10px 5px #888888;
    } 

Border image
~~~~~~~~~~~~

.. sourcecode:: python

    div
    {
        border-image:url(border.png) 30 30 round;
        -moz-border-image:url(border.png) 30 30 round; 
        -webkit-border-image:url(border.png) 30 30 round; 
        -o-border-image:url(border.png) 30 30 round;
    } 


--------------

Text Effects
==================

Text Shadow
~~~~~~~~~~~

.. sourcecode:: python

    h1
    {
        text-shadow: 5px 5px 5px #FF0000;
    } 

Word Wrapping
~~~~~~~~~~~~~~

.. sourcecode:: python

    p{word-warp:break-word;}

--------------

2D Transforms
~~~~~~~~~~~~~

* :strong:`translate`
* :strong:`rotate`
* :strong:`scale`
* :strong:`skew`
* :strong:`matrix`

:strong:`translate`

.. sourcecode:: python

    div
    {
        transform: translate(50px,100px);
        -ms-transform: translate(50px,100px); 
        -webkit-transform: translate(50px,100px);
        -o-transform: translate(50px,100px); 
        -moz-transform: translate(50px,100px);
    } 

--------------



Animations
~~~~~~~~~~

:strong:`模拟动画`

.. sourcecode:: python

    div
    {
        animation-name: myfirst;
        animation-duration: 5s;
        animation-timing-function: linear;
        animation-delay: 2s;
        animation-iteration-count: infinite;
        animation-direction: alternate;
        animation-play-state: running;
        -moz-animation-name: myfirst;
        -moz-animation-duration: 5s;
        -moz-animation-timing-function: linear;
        -moz-animation-delay: 2s;
        -moz-animation-iteration-count: infinite;
        -moz-animation-direction: alternate;
        -moz-animation-play-state: running;
        -webkit-animation-name: myfirst;
        -webkit-animation-duration: 5s;
        -webkit-animation-timing-function: linear;
        -webkit-animation-delay: 2s;
        -webkit-animation-iteration-count: infinite;
        -webkit-animation-direction: alternate;
        -webkit-animation-play-state: running;
    } 

--------------

Wonders
========

* Planet_
* CSScat_
* Google_guitar_
* Pac_
* Canvas-grad_
* BallPoll_
* liquid-particles_
* 3D_
* Firefox_

.. _Planet: https://developer.mozilla.org/zh-CN/demos/detail/the-planetarium/launch
.. _CSScat: https://developer.mozilla.org/en-US/demos/detail/css-nyan-cat/launch
.. _Google_guitar: http://googleguitar.org/
.. _Firefox: https://developer.mozilla.org/media/uploads/demos/p/a/paulrouget/html5-dashboard/demo_package/index.html
.. _Pac: http://macek.github.com/google_pacman/
.. _Canvas-grad: http://html5demos.com/canvas-grad/
.. _BallPoll:  http://mrdoob.com/projects/chromeexperiments/ball_pool/
.. _liquid-particles: http://spielzeugz.de/html5/liquid-particles.html
.. _3D: http://andrew-hoyer.com/experiments/cloth/

--------------

HTML5 Slide
===========

:strong:`reStructured`
:superscript:`Text` WYTIWYG

:strong:`目的`

(1) 建立一套标准语法来使用纯文本内容来表达内容的结构
(2) 将这类文档转换为有效的结构化数据模式

:strong:`优点`

* 易于阅读，纯文本标记语法和解析系统
* 易于使用,优秀扩展性
* 足够强大的语法来产生结构化文档
* 可处理各种自然语言
* MultiOutput:HTML,XML,LaTex,PDF,s5,man,odt,xml.xetex
* Python官方文档

:strong:`landslide`

Github https://github.com/adamzap/landslide

--------------

Useful links
============

* html5slides_  A Google HTML5 slide template

.. _html5slides: https://code.google.com/p/html5slides/

* HTML5ROCKS_ 

.. _HTML5ROCKS: https://www.html5rocks.com/en

* HTML5DashBoard_ 
  
.. _HTML5DashBoard: https://mozillademos.org/demos/dashboard/demo.html

* `Dive Into HTML5`_ 

.. _`Dive Into HTML5`: http://diveintohtml5.info/

* HTML5test_ test your browser's support for html5

.. _HTML5test: http://html5test.com

* W3Cschool_

.. _W3Cschool: http://www.w3schools.com/html5/default.asp


* Tutorial_

.. _Tutorial: http://www.hongkiat.com/blog/building-html5-css-webpages/

* `Another Tutorial`_

.. _`Another Tutorial`: http://www.dzinepress.com/2011/04/the-ultimate-html5-tutorials-and-useful-techniques/

* `开源中最好的Web开发的资源`_

.. _`开源中最好的Web开发的资源`: http://coolshell.cn/articles/4795.html



--------------

Thank you!
==========
