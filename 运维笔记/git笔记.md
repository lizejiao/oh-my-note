# git笔记

## 为配置代理

相关文章：[解决git无法clone提示443以及配置git代理方法](https://blog.csdn.net/a1527238987/article/details/80237076)

```shell
git config --global http.proxy "127.0.0.1:1087"
```

config 配置有system级别 global（用户级别） 和local（当前仓库）三个 设置先从system-》global-》local  底层配置会覆盖顶层配置 分别使用--system/global/local 可以定位到配置文件

- **查看系统config**

```shell
git config --system --list
```

- **查看当前用户（global）配置**

```shell
git config --global --list
```

- **查看当前仓库配置信息**

```shell
git config --local --list
```

