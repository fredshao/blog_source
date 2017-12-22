---
title: shadowsocksR安装
date: 2017-12-16 18:54:41
tags: 服务器配置
---

 

**以下操作请使用root用户**

```shell
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
```

```shell
chmod +x shadowsocksR.sh
```

```shell
./shadowsocksR.sh 2>&1 | tee shadowsocksR.log
```

**以上三个命令执行完后ShadowsocksR已经成功运行，可以使用了**

> **注意，如果你是在Google Cloud Platform上安装，那么还需要配置防火墙规则，根据自己设置的端口。如果想要偷懒，这里可以设置成443端口，443端口已经在Google Cloud Paltform的防火墙规则里了。**



**其他一些命令**

```shell
./shadowsocksR.sh uninstall		# 卸载 ShadowsocksR
```

```shell
/etc/init.d/shadowsocks start	# 启动
/etc/init.d/shadowsocks stop	# 停止
/etc/init.d/shadowsocks restart # 重启
/etc/init.d/shadowsocks status  # 状态

/etc/shadowsocks.json		# 配置文件路径
/var/log/shadowsocks.log	# 日志文件路径
/usr/local/shadowsocks		# 代码安装目录
```

