---
title: ' Vultr  配置 SSR 后连不上解决'
date: 2018-06-01 00:01:33
tags: 服务器配置
---

1. 打开 SSR 的端口

   ```
   ufw allow 端口号
   ```

2. 编辑 /etc/default/ufw 文件

   ```
   DEFAULT_INPUT_POLICY="DROP"
   DEFAULT_OUTPUT_POLICY="DROP"
   DEFAULT_FORWARD_POLICY="DROP"

   修改为：
   DEFAULT_INPUT_POLICY="ACCEPT"
   DEFAULT_OUTPUT_POLICY="ACCEPT"
   DEFAULT_FORWARD_POLICY="ACCEPT"
   ```

3. 重启 ufw

   ```
   ufw disable
   ufw enable
   ```

   这样就可以了，去试一下吧，如果再连不上，那我也不知道为什么了，~~~