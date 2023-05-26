# jdk 安装与使用记录

## 1. 安装配置jdk


### 1. 检查是否已安装

1. 检测是否拥有java语言环境
```shell
java -version
```

![没安装的情况](jdk的安装及使用_files/1.jpg)

表示没有安装过jdk


2. 检查jdk自带的安装包
```shell
rpm -qa | grep java
```

3. 如果有就卸载，卸载的包名通过检查命令获取，包名要全部输入


### 2. 安装

1. yum检查jdk版本
```shell
yum -y list java*
```

2. 安装(jdk1.8)
```shell
yum install -y java-1.8.0-openjdk
```

3. 安装后检查
```shell
java -version
```

![安装了的情况](jdk的安装及使用_files/2.jpg)

