# vim 安装与使用记录

## 1. 安装配置VIM (摘取) 
  - 摘取
  - [centos如何安装vim](https://www.php.cn/centos/445383.html)

### 1. 检查是否已安装

  查看一下你本机已经存在的包，确认一下你的VIM是否已经安装，输入：

  ```shell
    rpm -qa|grep vim
  ```

  如果已安装，会显示：

  > vim-minimal-7.4.629-6.el7.x86_64
  > 
  > vim-filesystem-7.4.629-6.el7.x86_64
  > 
  > vim-enhanced-7.4.629-6.el7.x86_64
  > 
  > vim-common-7.4.629-6.el7.x86_64
  > 
  > vim-X11-7.4.629-6.el7.x86_64

### 2. 安装

  如果缺少了其中某个，比如说： vim-enhanced这个包少了，则执行：

  ```shell
    yum -y install vim-enhanced
  ```

  它会自动下载安装。如果上面三个包一个都没有显示，则直接输入命令：

  ```shell
    yum -y install vim*
  ```

  执行命令后会自动安装，完毕后就可以使用vim编辑器了。

### 3. 配置

  安装完成后开始配置vim

  ```shell
    vim /etc/vimrc
  ```

  打开文件后，按 i 进入编辑模式，然后找一个位置添加如下代码

  > set nu          " 设置显示行号
  > 
  > set showmode    " 设置在命令行界面最下面显示当前模式等
  >  
  > set ruler       " 在右下角显示光标所在的行数等信息
  > 
  > set autoindent  " 设置每次单击Enter键后，光标移动到下一行时与上一行的起始字符对齐
  > 
  > syntax on       " 即设置语法检测，当编辑C或者Shell脚本时，关键字会用特殊颜色显示

  添加好了之后，按Esc，然后输入

  ```shell
    :wq
  ```

  退出并保存即可。
  
## 2. VIM常用命令悉知
  - 摘取
  - [Vim命令合集](https://www.cnblogs.com/softwaretesting/archive/2011/07/12/2104435.html)

### 1. 命令历史

  以:和/开头的命令都有历史纪录，可以首先键入:或/然后按上下箭头来选择某个历史命令。
  
### 2. 启动vim

vim 直接启动vim

vim filename 打开vim并创建名为filename的文件

示例：
```shell
  vim config.conf
```
如果存在config.conf文件 则直接打开，如果没有 则会创建config.conf文件 在操作保存时会进行实际物理存储

### 3. 文件命令

1. 打开单个文件
```shell
  vim file
```

2. 同时打开多个文件
```shell
  vim file1 file2 file3 ...
```

3. 在vim窗口中打开一个新文件
```shell
  :open file
```

4. 在新窗口中打开文件
```shell
  :split file
```

5. 切换到下一个文件
```shell
  :bn
```

6. 切换到上一个文件
```shell
  :bp
```

7. 查看当前打开的文件列表，当前正在编辑的文件会用[]括起来。
```shell
  :args
```


