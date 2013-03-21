 使用e4rat加速你的linux启动速度（ext4文件系统专用）

e4rat是什么，简单来说他可以使系统的启动速度加快，之前我的archlinux启动速度在40s多，现在降到了30m，有10m左右的改善

在archlinux下怎么玩：

1. **安装**
    
::

    sudo pacman -S e4rat

2. **配置**
  
  (2.1) 修改grub启动命令，让e4rat收集开机预读的文件列表
  
    在开机启动到grub时，按e进行编辑，修改kernel 那一行，在末尾添加init=/sbin/e4rat-collect,然后在2min内打开经常使用的程序
    这些程序会被e4rat记录下来，方便加速（当然不要开太多。。。）
    
    2分钟后看一下有木有/var/lib/e4rat目录是不是有startup.log这个文件，这个文件是e4rat收集的

  (2.2) 再次修改grub启动命令，让e4rat把以前收集的信息利用下  
  
    在开机启动grub时，按e进行编辑，修改kernel 那一行，末尾添加single,进入单用户模式,按提示输入root密码
    运行e4rat-realloc /var/lib/e4rat/startup.log

  (2.3) 修改/boot/grub/menu.list或者/boot/grub/grub.cfg，享受e4rat吧

    在文件中的kernel那一行末尾添加 init=/sbin/e4rat-perload

3. **注意点**

   (3.1) 只对ext4文件系统的有效，据说ext2,3升级到ext4的也不ok

   (3.2) 对固态硬盘无用，对CLI用户无效，对使用X的同学效果明显

   (3.3) 可以使用bootchart来查看系统的启动流程和时间

参考

    http://linuxtoy.org/archives/e4rat.html

    http://wiki.archlinux.org/index.php/E4rat
