---
title: "[Ubuntu] C++ 랜덤 값 생성"

sidebar:
    nav: "ubuntu"
---

<br/>

랜덤 값 생성을 위해서는 랜덤 시드 초기화(`srand`)를 하고 랜덤 값이 필요한 곳에서 랜덤 값을 생성(`rand`)하여 사용한다.

```cpp
#include <stdlib.h>
#include <time.h>

srand(time(NULL));
int random_value = rand()%255;
```

<br/>


