---
title: "[MFC] 리소스 오류 (error RC2104: undefined keyword or key name: SS_REALSIZECONTROL)"

sidebar:
    nav: "windows"

toc: false
---

<br/>

MFC에서 리소스 파일을 열려고 할 때 가끔 아래 오류가 포함된 경고창이 뜨면서 열리지 않는 경우가 있다.

```javascript
error RC2104: undefined keyword or key name: SS_REALSIZECONTROL
```

이런 문제가 발생할 경우, 리소스 코드를 열어서 아래와 같은 부분을 찾는다.

```cpp
#ifndef APSTUDIO_INVOKED
#include "targetver.h"
#endif
#include "afxres.h"
#include "verrsrc.h"
```

그리고 `#include "targetver.h"` 바로 아래 줄에 아래 코드를 입력한다.

```cpp
#else
#define WINVER 0x501
```

최종적으로 아래와 같이 수정하여 저장하고 다시 리소스 파일을 열어본다.

```cpp
#ifndef APSTUDIO_INVOKED
#include "targetver.h"
#else
#define WINVER 0x501
#endif
#include "afxres.h"
#include "verrsrc.h"
```


<br/>