---
title: 'C#获取所有实现某一接口的类'
date: 2017-11-20 12:32:04
tags: 游戏开发
---

```c#
 var interfaceImplements = AppDomain.CurrentDomain.GetAssemblies()
        .SelectMany(item => item.GetTypes())
        .Where(item => item.GetInterfaces()
        .Contains(typeof(IModel)))
        .Select(type => (IModel)Activator.CreateInstance(type)).ToList();
```

