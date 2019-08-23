# 文件和目录常用命令

## 目录操作

* 查看目录 : ls，ll

  ./ 当前目录 ../ 父级目录 / 根目录

* 切换目录 : cd

* 创建目录 : mkdir dirname

* 删除目录 : rm -rf dirname

* 拷贝目录 : cp -r  dirsource dirtarget

* 移动目录 : mv -r dirsource dirtarget

## 文件操作

* 查看文件内容 

  cat filename (查看文件内容、创建文件、文件合并、追加文件内容 等功能)

  more filename (分屏显示文件内容，每次只显示一页内容)

  * 空格键	显示手册页的下一屏
  	 Enter 键	一次滚动手册页的一行
  	 b	回滚一屏
  	 f	前滚一屏
  	 q	退出
  	 /word	搜索 word 字符串

* **创建文件** : touch filename 

* 删除文件 : rm -f  filename 

* 拷贝目录 : cp  filesource filetarget

* 移动目录 : mv filesource filetarget

* 文本搜索 : grep

  * -n	显示匹配行及行号
  	 -v	显示不包含匹配文本的所有行（相当于求反）
  	 -i	忽略大小写

* 常用的两种模式查找\

  * ^a	行首，搜寻以 a 开头的行
  	 ke$	行尾，搜寻以 ke 结束的行

## 其他

* echo 会在终端中显示参数指定的文字

* **重定向 > 和 >>**

  * \> 表示输出，会覆盖文件原有的内容
  * \>> 表示追加，会将内容追加到已有文件的末尾

* **管道 |**

  一个命令的输出 可以通过管道 做为 另一个命令的输入

  常用的管道命令有：
  more：分屏显示内容
  grep：在命令执行结果的基础上查询指定的文本

# 远程管理常用命令

* 关机/重启

  * shutdown 选项 时间 : 关机

    选项	含义
    -r	重新启动

  * **halt** 关机

* 查看或配置网卡信息

  * ifconfig
  * ping

* 远程登录

  * ssh 用户名@ip

* 复制文件

  *  scp

# 用户权限

* 基本概念

  序号	权限		英文		缩写		数字代号
  01		读			read		r			4
  02		写			write		w			2
  03		执行		excute		x			1

* 组
  为了方便用户管理，提出了 组 的概念
  在实际应用中，可以预先针对 组 设置好权限，
  然后 将不同的用户添加到对应的组中，从而不用依次为每一个用户设置权限

* **切换用户  su username**

* 退出 exit

* **修改文件权限**

  ​	序号	命令		作用
  	01	        chown	         修改拥有者
  	02	        chgrp	         修改组
  	03	        chmod	         修改权限

  ex. chmod 修改 用户／组 对 文件／目录 的权限

  ​	chmod -rwx 文件名|目录名

  * 递归修改文件|目录的组

     chgrp -R 组名 文件名|目录名

  * 递归修改文件权限

    chmod -R 755 文件名|目录名

    ![](.\picture\权限.jpg)

    ![](http://ww1.sinaimg.cn/large/007KrspHly1g69lxqc2jsj30bc03wt8v.jpg)

* sudo 

  sudo 命令用来以其他身份来执行命令，预设的身份为 root.

  使用 sudo 时，必须先输入密码，之后有 5 分钟的有效期限.

* 组管理

  * 添加组 : groupadd 组名	
  * 删除组 : groupdel 组名
  	 确认组信息 : cat /etc/group	
  * 递归修改文件/目录的所属组 : chgrp -R 组名 文件/目录名

* 用户管理

  * **添加新用户** : useradd -m -g 组 新建用户名

    -m 自动建立home目录

    -g 指定用户所在的组

  * **设置用户密码** : passwd 用户名

  * 删除用户 : userdel -r 用户名

    -r 选项会自动删除用户家目录

  * 确认用户信息 cat /etc/passwd | grep 用户名

    新建用户后，用户信息会保存在 /etc/passwd 文件中

  * **查看用户信息**

  	 who		查看当前所有登录的用户列表
    whoami		查看当前登录用户的账户名

  * which 命令 ：查看执行命令所在位置

    ex. which ls

# 系统信息

* 时间和日期

  * date	查看系统时间
  * cal / calendar 查看日历，-y 选项可以查看一年的日历

* 磁盘和目录空间

  * df ：disk free 显示磁盘剩余空间

    df -h

  * du：disk usage 显示目录下的文件大小

    du -h [目录名]

* **进程信息**：

  * 找出占用端口进程的pid

    lsof -i:port


  * ps : process status 查看进程的详细状况

    * **ps aux**

      选项	含义
      a	显示终端上的所有进程，包括其他用户的进程
      u	显示进程的详细状态
      x	显示没有控制终端的进程

  * **top** : 动态显示运行中的进程并且排序

  * **kill**

    * kill [-9] 进程代号

      终止指定代号的进程，-9 表示强行终止

# 其他命令

* 查找文件 ：find

  ex. find [路径] -name "*.py"

  查找指定路径下扩展名是 .py 的文件，包括子目录

  如果省略路径，表示在当前文件夹下查找

* 软链接 通俗的方式讲类似于 Windows 下的快捷方式

  ln -s 被链接的源文件 链接文件

  注意: 

  * 没有 -s 选项建立的是一个 硬链接文件
  * 源文件要使用绝对路径，不能使用相对路径

  ln -snf 被链接的源文件 链接文件   --更改软连接

* 打包和压缩

  不同操作系统中，常用的打包压缩方式是不同的。

  * Windows 常用 rar
  * Mac 常用 zip
  * Linux 常用 tar.gz

  **打包 ／ 解包**（含压缩）

  * **打包文件**

    tar czf 压缩文件名 要压缩的文件夹

    ex. tar czf test.tar.gz ./opt/

  * **解包文件**（-C参数 表示更换目录的意思 ）

    tar -zxf 待解压文件 -C 解压到的文件夹

    ex. tar -zxf test.tar.gz -C /opt/module/

  * tar 选项说明
    选项	含义
    c	生成档案文件，创建打包文件
    x	解开档案文件
    v	列出归档解档的详细过程，显示进度
    f       指定文件名，f 后面一定是 .tar 文件，必须放选项最后

    z       调用 gzip, 实现压缩和解压缩的功能

* 软件安装

  apt 是 Advanced Packaging Tool，是 Linux 下的一款安装包管理工具

  * 安装软件 apt-get install 软件包
  * 卸载软件 apt-get remove 软件名
  * 更新已安装的包 apt-get upgrade 

  配置软件源

  * 在软件和更新中，选项ubuntu软件

    设置下载自：http://mirrors.aliyun.com/ubuntu

# vi 编辑

很多 Linux 发行版中，直接把 vi 做成 vim 的软连接

* 查询软连接命令（知道）

  $ which vi

* 打开和新建文件

  vi filename

  * 如果文件已经存在，会直接打开该文件
  * 如果文件不存在，会新建一个文件

* 光标上下左右

  h  j  k  l
  左下右上

* Vim编辑器三种模式

  * 命令模式：控制光标移动，可对文本进行复制、粘贴、删除和查找等工作。

  * 输入模式：正常的文本录入。

  * 末行模式：保存或退出文档，以及设置编辑环境。

    ![img](file:///E:/ProjectFile/GitRepos/StudyNotesRepo/NoteRepo/picture/vim%E6%A8%A1%E5%BC%8F%E5%88%87%E6%8D%A2.jpg?lastModify=1566531557)

    ![](http://ww1.sinaimg.cn/large/007KrspHly1g69lyhk9t9j30dr05kabx.jpg)

  * 命令模式中最常用的一些命令

    * dd	删除（剪切）光标所在整行
    	 5dd	删除（剪切）从光标处开始的5行
    	 yy	复制光标所在整行
    	 5yy	复制从光标处开始的5行
    	 u	撤销上一步的操作
    	 **p**	将之前删除（dd）或复制（yy）过的数据粘贴到光标后面
    * shirft+g  跳转到最后一行

  * 末行模式常用的一些命令

    * :q!	强制退出（放弃对文档的修改内容）
    	 :wq!	强制保存退出
    	 :set nu	显示行号
    	 :set nonu	不显示行号
    	 :s/one/two	将当前光标所在行的第一个one替换成two
    	 :s/one/two/g	将当前光标所在行的所有one替换成two
    	 :%s/one/two/g	将全文中的所有one替换成two
    	 ?字符串	在文本中从下至上搜索该字符串
    	 /字符串	在文本中从上至下搜索该字符串









