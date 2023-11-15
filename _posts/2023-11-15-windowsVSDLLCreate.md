---
title: "[Windows] Visual Studio에서 DLL 만들기"

sidebar:
    nav: "windows"

toc: true
---

<br/>



# 1. 개요

프로그램을 만들어 배포하다 보면 DLL 형태로 배포하는 것이 필요한 경우가 있다. 

DLL로 배포하면 장점은 소스코드를 공유하지 않아도 되고, 수정 배포할 때도 DLL 파일만 새로운 파일로 전달하면 되기 때문에 편리하다. 

그런데 조심해야 하는 것은 DLL을 생성하는 컴파일러에 따라 DLL의 형식이 조금씩 다르다.  

그래서 Visual Studio에서 만든 DLL을 다른 컴파일러에서 사용하려고 하면 안 되는 경우가 있다. 

사용 안 되는 DLL을 사용할 수 있게 바꾸는 방법도 있긴 한 것 같은데 그 방법이 간단한 것도 아니고 일부분만 되는 경우도 있는 것 같으니 사용할 컴파일러에서 DLL을 만드는 것이 가장 좋을 것 같다. 

<br/>


# 2. DLL 만들기

## (1) DLL 생성 프로젝트 만들기

프로젝트 템플릿에서 "DLL(동적 연결 라이브러리)"을 찾아 프로젝트를 만든다. 

여기서는 솔루션 이름은 "test_dll", 프로젝트 이름은 "dll_create"으로 생성하였다. 

![]({{ site.url }}/assets/images/231115/1_create_project.png){: .align-center} 

프로젝트를 만들면 기본적으로 `pch.h`, `pch.cpp`, `framework.h`, `dllmain.cpp` 파일이 생성된다. 

![]({{ site.url }}/assets/images/231115/2_dll_create.png){: .align-center} 

> "DLL 생성 프로젝트"의 속성은 자동으로 DLL 생성에 맞도록 생성되기 때문에 특별히 변경해야 하는 설정은 없다.  
> 입맛에 맞는 개발 환경이 되도록 설정하면 된다. (예를 들어, 출력 파일이 저장되는 폴더 경로 수정 등)  
> `pch.h` 관련 오류가 발생할 수도 있는데 "미리 컴파일된 헤더"를 사용하기 위한 설정을 진행하거나 "프로젝트 속성 --> 구성 속성 --> C/C++ --> 미리 컴파일된 헤더"에서 "미리 컴파일된 헤더 사용 안 함"으로 설정하면 된다.  
{: .notice--info}


## (2) 헤더파일, 소스코드 작성 

DLL로 만들 간단한 헤더파일과 소스코드를 작성한다. 

프로젝트에서 오른쪽 버튼을 눌러 추가를 선택하여 헤더파일(`dll_create.h`)과 소스코드(`dll_create.cpp`)를 각각 생성한다. 

`TESTDLL` 이름의 클래스를 만드는 코드이다.

클래스를 생성하면 콘솔에 메시지를 출력하여 생성이 잘 되었는지 확인하도록 하였다. 

```cpp
// dll_creat.h

#ifndef DLL_CREATE_H
#define DLL_CREATE_H

///////////////////////////////
/* Macros for DLL generation */
///////////////////////////////
#ifdef DLLCREATE_EXPORTS
#if defined(_MSC_VER)
#define DLL_EXPORTS __declspec(dllexport)
#endif
#else
#if defined(_MSC_VER)
#define DLL_EXPORTS __declspec(dllimport)
#endif
#endif

#if defined(_MSC_VER)
#pragma warning ( disable : 4251 )
#endif

///////////
/* class */
///////////
class DLL_EXPORTS TESTDLL
{
public:
	TESTDLL();
	~TESTDLL();
}; // class TESTDLL

#endif // DLL_CREATE_H
```

```cpp
// dll_creat.cpp

#include "dll_create.h"

#include <iostream>


//////////////////////
/* TESTDLL::TESTDLL */
//////////////////////
TESTDLL::TESTDLL()
{
	std::cout << __FUNCTION__ << " is created." << std::endl;
}

TESTDLL::~TESTDLL()
{
}
```

이렇게 만든 코드를 컴파일 하면 결과 폴더에 `dll_create.dll`, `dll_create.lib`이 생성된다. 

만들어진 DLL을 사용하여 다른 프로젝트에서 프로그램을 만들고 컴파일을 진행하려면 `dll_create.h`, `dll_create.dll`, `dll_create.lib` 파일 세 가지가 모두 필요하다. 


## (3) 코드 설명 

소스코드는 특별한 부분이 없으며 헤더파일만 설명을 하고자 한다.

```cpp
#ifdef DLLCREATE_EXPORTS
#if defined(_MSC_VER)
#define DLL_EXPORTS __declspec(dllexport)
#endif
#else
#if defined(_MSC_VER)
#define DLL_EXPORTS __declspec(dllimport)
#endif
#endif
```

먼저, 위와 같이 DLL을 생성하는 것과 관련된 매크로를 보면 `DLLCREATE_EXPORTS`가 define 되어 있는지 여부에 따라 `DLL_EXPORTS` define 부분이 다르다. 

`DLLCREATE_EXPORTS`은 프로젝트의 속성을 보면 이미 프로젝트 생성 시에 전처리기로 설정되어 있다. 

프로젝트 이름 뒤에 `_EXPORTS`가 붙어 만들어진 것을 알 수 있다. 

![]({{ site.url }}/assets/images/231115/3_dllcreate_exports.png){: .align-center} 

따라서 "DLL 생성 프로젝트"를 컴파일 하면 `DLLCREATE_EXPORTS`가 define 되어 있고, 다른 프로젝트에서 헤더파일을 가져다 컴파일하면 define 되어 있지 않게 되는 것이다. 

`__declspec(dllexport)` 또는 `__declspec(dllimport)`은 함수나 클래스 앞에 붙여 사용하는데 각각 해당 함수/클래스를 export 하여 DLL로 만들거나 함수/클래스를 DLL으로부터 import 하여 사용하는 의미이다. 

define된 `DLL_EXPORTS`은 export 할 함수나 클래스 앞에 아래와 같이 사용한다. 

```cpp
class DLL_EXPORTS TESTDLL
{
public:
	TESTDLL();
	~TESTDLL();
}; // class TESTDLL
```

이를 통해, `TESTDLL` 클래스를 `DLLCREATE_EXPORTS` 전처리기 여부에 따라 DLL export 또는 import 하여 사용할 수 있다. 

추가로 이렇게 코드를 작성해서 컴파일을 하면 경고가 뜨게 되는데 아래와 같이 설정하면 경고를 없앨 수 있다. 

```cpp
#if defined(_MSC_VER)
#pragma warning ( disable : 4251 )
#endif
```


<br/>


# 3. DLL 사용하기

## (1) DLL 사용 프로젝트 만들기

앞서 만든 DLL을 사용하기 위해 솔루션에 프로젝트를 하나 더 추가한다. 

Visual Studio를 배울 때 가장 먼저 하는 "Hello World!"를 콘솔에 출력하는 템플릿을 사용한다. 

"추가 --> 새 프로젝트"에서 콘솔 앱을 선택하여 프로젝트를 만든다. 

이번 프로젝트 이름은 `dll_use`으로 만들었으며, `dll_use.cpp` 파일이 자동 생성된다. 


## (2) 솔루션 설정 

### a. 시작 프로젝트

솔루션에 프로젝트가 2개 이상이 되었을 때, 추가로 설정해야 하는 것이 있다. 

프로젝트 결과물을 확인하기 위해 시작(Run, `Ctrl+F5`)을 하면 "시작 프로젝트"에 설정된 프로젝트가 실행된다. 

이때, 기본으로 설정된 프로젝트가 DLL 프로젝트이기 때문에 오류가 발생하므로 콘솔 앱 등과 같은 프로젝트로 변경해줘야 한다. 

솔루션에서 오른쪽 버튼을 클릭하여 "시작 프로젝트 구성..."을 선택한다. 

![]({{ site.url }}/assets/images/231115/4_solution_setting.png){: .align-center} 

"시작 프로젝트"에서 "현재 선택 영역"을 선택하거나 "한 개의 시작 프로젝트"에서 "dll_use"를 선택한다. 


### b. 프로젝트 종속성

`dll_use` 프로젝트는 DLL이 없으면 컴파일 오류가 발생하게 된다. 

따라서 `dll_create` 프로젝트 컴파일이 먼저 완료된 후에 `dll_use` 프로젝트 컴파일이 진행되어야 한다. 

이를 위해, "프로젝트 종속성"에서 `dll_use` 프로젝트에 `dll_create` 프로젝트 종속을 추가한다. 

![]({{ site.url }}/assets/images/231115/5_solution_setting2.png){: .align-center} 


## (3) 프로젝트 설정 

DLL을 사용하기 위해 프로젝트에서 설정해야 하는 것은 크게 세 가지가 있다. 

### a. 추가 포함 디렉터리 

사용할 헤더파일이 있는 폴더의 경로를 설정한다. 

"프로젝트 속성 --> 구성 속성 --> C/C++ --> 일반"에서 "추가 포함 디렉터리"에 헤더파일이 있는 폴더의 경로를 입력한다. 

![]({{ site.url }}/assets/images/231115/6_include_path.png){: .align-center} 

### b. 추가 라이브러리 디렉터리 

사용할 dll, lib 파일들이 있는 폴더의 경로를 설정한다. 

"프로젝트 속성 --> 구성 속성 --> 링커 --> 일반"에서 "추가 라이브러리 디렉터리"에 dll, lib 파일이 있는 폴더의 경로를 입력한다. 

![]({{ site.url }}/assets/images/231115/7_lib_path.png){: .align-center} 

### c. 추가 종속성 

사용할 lib 파일을 설정한다. 

"프로젝트 속성 --> 구성 속성 --> 링커 --> 입력"에서 "추가 종속성"에 사용할 lib 파일(`dll_create.lib`)을 입력한다. 

![]({{ site.url }}/assets/images/231115/8_add_lib.png){: .align-center} 

<br/>


## (4) 소스코드 작성 

`dll_use.cpp` 파일에 아래와 같이 코드를 작성한다. 

```cpp
// dll_use.cpp

#include <iostream>

#include "dll_create.h"

int main()
{
	TESTDLL* test_dll = new TESTDLL();
	std::cout << "Hello World!\n";
}
```

헤더파일을 추가하고 `TESTDLL` 클래스의 인스턴스를 만드는 간단한 코드이다. 

컴파일하고 실행하면 클래스의 인스턴스가 정상적으로 생성되어 아래와 같이 콘솔에 출력된다. 

![]({{ site.url }}/assets/images/231115/9_results.png){: .align-center} 


<br/>


# 4. DLL 배포하기

DLL을 이용하여 새로운 프로그램을 만들어 컴파일 하기 위해서는 `*.h`, `*.dll`, `*.lib` 파일 세 가지가 모두 필요하다. 

하지만 DLL을 이용하여 새롭게 만든 프로그램을 실행만 하는 경우에는 `*.dll` 파일만 있으면 된다. 


<br/>
