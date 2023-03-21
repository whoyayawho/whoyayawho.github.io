---
title: "[ROS] .so 파일 추가"

sidebar:
    nav: "dev"

toc: false
---

<br/>


미리 컴파일된 라이브러리 `.so` 파일을 추가하여 컴파일 하기 위해 `CMakeLists.txt` 파일에 아래와 같이 추가한다.

파일명과 경로를 적절히 수정해서 작성한다.

`${ARCHITECTURE}`에는 현재 구동 시스템의 아키텍쳐가 들어간다.


```java
execute_process( COMMAND uname -m COMMAND tr -d '\n' OUTPUT_VARIABLE ARCHITECTURE )
set( LIBRARY_PATH "${PROJECT_SOURCE_DIR}/lib/${ARCHITECTURE}" )
set( PATH_PLANNING_LIB "${LIBRARY_PATH}/libpath_planning.so")

:
:

target_link_libraries(${PROJECT_NAME}_node
  ${PATH_PLANNING_LIB}
)
```


<br/>


