---
title: "[MFC] 문자열(string) 형변환"

sidebar:
    nav: "windows"

toc: true
---

<br/>

# 1. 개요

Visual Studio에서 개발을 하다보면 특히 MFC의 경우에 문자열 형변환을 해야 할 일이 자주 있다. 

매번 잊어버리고 찾는 것이 번거로워 정리하기로 한다. 

<br/>


# 2. 문자열 형변환

## (1) `char*` --> `std::string`

```cpp
char str_from[10] = "hello";
std::string str_to(str_from);
// 또는
std::string str_to = str_from;
```

## (2) `std::string` --> `const char*`

```cpp
std::string str_from = "hello";
const char* str_to = str_from.c_str();
```

## (3) `std::string` --> `char*`

```cpp
std::string str_from = "hello";
std::vector<char> str_from2(str_from.begin(), str_from.end());
str_from2.push_back('\0');
char* str_to = &*str_from2.begin();
```

## (4) `char*` --> `CString`

```cpp
char str_from[10] = "hello";
CString str_to = str_from;
```

## (5) `std::string` --> `CString`

```cpp
std::string str_from = "hello";
CString str_to(str_from.c_str());
```

## (6) `CString` --> `std::string`

```cpp
CString str_from(_T("hello"));
std::string str_to = std::string(CT2CA(str_from));
```

## (7) `std::stringstream` --> `std::string`

```cpp
std::stringstream str_from;
str_from << "hello" << std::endl;
std::string str_to = str_from.str();
```


<br/>

