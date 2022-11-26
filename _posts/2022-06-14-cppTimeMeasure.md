---
title: "[C++] 코드 실행 시간 측정"

sidebar:
    nav: "dev"
---

<br/>


우분투에서 C++로 프로그래밍할 때, 코드 실행 시간을 측정하기 위해 아래 함수를 사용한다.


# 1. 시간 측정

```cpp
#include <chrono>

using namespace std::chrono_literals;


std::chrono::steady_clock::time_point last_detected_time = std::chrono::steady_clock::now();
// 시간 측정하고자 하는 코드
std::chrono::duration<double> diff_time = std::chrono::steady_clock::now() - last_detected_time;
std::cout << diff_time.count() << std::endl;
```




<br/>


