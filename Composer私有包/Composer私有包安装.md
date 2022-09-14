# Composer私有包安装

## 1. 制作gitlab私有包




## 2. 在项目中使用私有包

1. 需要被授权可获取该包

2. 在项目工程中的composer.json中加入该私有包

```json
{
    ...
    "require": {
        "hptown-extension/api-response": "^1.0"
    },
    ...
    "repositories": {
        ...
        "hptown-extension/api-response": {
            "type": "vcs",
            "url": "ssh://git@gitlab.dev.hptown.cn:19022/SoftwareDevelopmen/ServerEndGroup/api-response.git"
        }
    }
}

```

- require 中指定 包名 以及版本 可 指定分支 可依据tag版本规则 获取

- repositorires 中 添加需要添加的私有包及私有包的git地址

- 使用composer update 即可更新

- 需要 以 ssh 使用 git