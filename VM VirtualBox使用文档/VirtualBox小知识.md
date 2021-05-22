## 1. 赋予用户挂载目录权限
 
- 将当期登录用户加入到vboxsf组
```shell
sudo usermod -aG vboxsf $(whoami)
```

示例： 需要将 用户 www 添加到 vboxsf组中
```shell
  sudo usermod -aG vboxsf www
```

**重启才会生效**

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

## 3. 网络请求403

- 需要重新配置一下挂载的文件目录及子文件的权限 需要开启vboxsf组所有权限（前提是www用户在vboxsf组中）
