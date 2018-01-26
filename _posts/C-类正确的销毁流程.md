---
title: 'C#类正确的销毁流程'
date: 2017-11-20 12:34:49
tags: 游戏开发
---

```c#
using System;
using System.Collections.Generic;

public class Test : IDisposable {
 private List<int> numbers = new List<int>();

    ~Test() {
     Dispose(false);
 }

    public void Dispose() {
     Dispose(true);
     GC.SuppressFinalize(this);
 }
	
    private void Dispose(bool _disposing) {
     // _disposing 为true时，自己销毁分配的内存，列表，字典，数组，其他类实例，等等
     if (_disposing) {
            if(numbers != null) {
             numbers.Clear();
         }
         numbers = null;
     }
 }
}
```

