## 安装完系统后 挂载文件系统

### 1 安装增强功能出现kernel headers not found for target kernel 错误的解决办法

1. 更新kernel

  yum update kernel -y

2. 安装缺失的包

  yum install kernel-headers kernel-devel gcc make -y

3. 重启系统
  
4. 正常安装增强功能

  **增强工具iso文件 路径不可存在空格**
 
  1. 拷贝 安装目录下的VBoxGuestAdditions.iso 到 某盘的根目录 如D盘
 
  2. VMware中该虚拟机的设置 -- > 存储 -->光盘中选择该ios 文件 
 
  3. 在虚拟机中执行命令
 
    - 挂载
    ```shell
      mount /dev/cdroom /mnt/iso 
    ```
  
    - 执行安装
    ```shell
      cd /mnt/iso
      sh VBoxLinuxAdditions.run 
    ```
    