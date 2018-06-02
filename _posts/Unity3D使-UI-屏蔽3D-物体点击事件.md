---
title: Unity3D使 UI 屏蔽3D 物体点击事件
date: 2018-06-02 09:21:23
tags: 游戏开发
---

 Uinty3D 的 UnityEngine.EventSystems.EventSystem.current.IsPointerOverGameObject(); 似乎有 BUG，在电脑平台一切正常，但是在移动平台，无法正确检测到是否点在了 UI 上，下面是摘自网络的一个解决方案

```c#
private void OnMouseDown() {
    if (IsPointerOverGameObject()) {
        Debug.Log("Clicked UI");
        return;
    }

    Debug.Log("Click GameObject " + gameObject.name);
}

	
public static bool IsPointerOverGameObject() {
    PointerEventData eventData = new PointerEventData(UnityEngine.EventSystems.EventSystem.current);
    eventData.pressPosition = Input.mousePosition;
    eventData.position = Input.mousePosition;

    List<RaycastResult> list = new List<RaycastResult>();
    UnityEngine.EventSystems.EventSystem.current.RaycastAll(eventData, list);
    return list.Count > 0;
}
```

