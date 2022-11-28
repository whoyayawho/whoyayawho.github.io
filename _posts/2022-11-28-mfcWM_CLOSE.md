---
title: "[MFC] MFC 종료 함수"

sidebar:
    nav: "windows"
---

<br/>


아래 함수를 실행하여 MFC 프로그램을 종료할 수 있다.

```cpp
AfxGetMainWnd()->PostMessage(WM_CLOSE);
```

<br/>