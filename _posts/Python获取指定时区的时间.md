---
title: Python获取指定时区的时间
date: 2018-01-26 18:02:06
tags: Python
---

```python
import pytz
from datetime import datetime
import time

def GetShanghaiTime(self):
    tz = pytz.timezone('Asia/Shanghai')
    ts = int(time.time())
    dt = datetime.fromtimestamp(ts,tz)
    return datetime(dt.year,dt.month,dt.day,dt.hour,dt.minute,dt.second,dt.microsecond)
```

> 如果 pytz 找不到，请先使用 pip3 install pytz 安装

