## 1. 赋予用户挂载目录权限
 
- 将当期登录用户加入到vboxsf组
```shell
sudo usermod -aG vboxsf $(whoami)
```

- 重启
```shell
reboot
```
  
## 2. 修改hosts文件

- hosts文件路径
```shell
cd /etc
```

- 修改hosts
```shell
vim /etc/hosts
```

- 重启网络
```shell
/etc/init.d/network restart
```

