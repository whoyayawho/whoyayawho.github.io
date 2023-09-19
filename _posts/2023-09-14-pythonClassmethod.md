---
title: "[Python] 인스턴스 메소드, 클래스 메소드, 정적 메소드 (@classmethod, @staticmethod)"

sidebar:
    nav: "dev"

toc: true
---

<br/>

# 1. 개요

파이썬(python)에서 메소드(method)는 인스턴스 메소드(instance method), 클래스 메소드(class method), 정적 메소드(static method)가 있다. 

이 중에서 인스턴스 메소드는 일반적으로 python에서 처음 배우는 클래스를 만들고 메소드를 만들어 사용하는 것을 말한다고 보면 된다.

따라서 이번 글에서는 클래스 메소드와 정적 메소드에 대해 설명하고, 세 가지 메소드의 차이를 설명하고자 한다. 

```python
class TestClass:
    name = "TestClass"
    __priv_name = "Private TestClass"

    def __init__(self) -> None:
        print("__init__")
        self.var_1 = "var_1"
        self.__var_2 = "var_2"

    # instance method
    def test_instance(self) -> None:
        print("\n  [Instance method]")
        print(self.name)
        print(self.__priv_name)
        print(self.var_1)
        print(self.__var_2)

    # static method
    @staticmethod
    def test_static() -> None:
        print("\n  [Static method]")
        # print(self.name)  # 오류 발생
        # print(self.__priv_name)  # 오류 발생
        # print(self.var_1)  # 오류 발생
        # print(self.__var_2)  # 오류 발생

    # class method
    @classmethod
    def test_class(cls) -> None:
        print("\n  [Class method]")
        print(cls.name)
        print(cls.__priv_name)
        # print(cls.var_1)  # 오류 발생
        # print(cls.__var_2)  # 오류 발생


test = TestClass()
test.test_instance()
print(test.var_1)
# print(test.__var_2)  # 오류 발생
# print(test.__priv_name)  # 오류 발생

TestClass.test_static()

TestClass.test_class()

print("===")
print(TestClass.name)
# print(TestClass.__priv_name)  # 오류 발생
```

```
=== 코드 수행 결과 ===
__init__

  [Instance method]
TestClass
Private TestClass
var_1
var_2
var_1

  [Static method]

  [Class method]
TestClass
Private TestClass
===
TestClass
```

<br/>


# 2. Private 변수 및 메소드

완벽히는 아니지만 class 내부에서 생성한 변수나 메소드를 외부에서 접근하지 못하도록 할 수 있다. 

변수나 메소드 앞에 "__"을 붙여서 이름을 만드는 것이다. 

이렇게 생성한 변수나 메소드는 (아예 방법이 없는건 아니지만) 일반적인 방법으로는 접근이 안 된다. 

아래 코드와 같은 방법으로 변수에 접근하면 `AttributeError: 'TestClass' object has no attribute '__var_2'`와 같은 오류가 발생한다. 

```python
test = TestClass()
print(test.__var_2)  # 오류 발생
print(test.__priv_name)  # 오류 발생
print(TestClass.__priv_name)  # 오류 발생
```

<br/>


# 3. 정적 메소드 (static method)

## (1) 생성

정적 메소드를 생성할 때 아래와 같이 `@staticmethod` 데코레이터를 사용한다. 

```python
class TestClass:
    @staticmethod
    def test_static() -> None:
        print("\n  [Static method]")
```

## (2) 사용

인스턴스 메소드를 사용하기 위해서는 아래 코드와 같이 먼저 인스턴스를 만든 다음에 인스턴스 변수를 이용하여 메소드를 사용한다.
```python 
test = TestClass()  # 인스턴스 생성
test.test_instance()  # 생성된 인스턴스 변수를 이용하여 메소드 실행
```

하지만 정적 메소드는 인스턴스를 만들지 않아도 아래 코드와 같이 바로 사용이 가능하다. 

```python
TestClass.test_static()  # 인스턴스 생성 없이 바로 정적 메소드 사용 가능 
```
```
=== 코드 수행 결과 ===
  [Static method]
```

클래스 메소드도 인스턴스를 만들지 않아도 사용이 가능하다는 점은 정적 메소드와 동일하다. 

하지만 정적 메소드는 클래스 메소드와 달리 클래스 변수에 접근하지 못하는 차이가 있다. 

정적 메소드는 클래스 안에 선언된다 뿐이지 별개의 함수를 사용하는 것과 같다. 


<br/>


# 4. 클래스 메소드 (class method)

## (1) 생성

클래스 메소드를 생성할 때 아래와 같이 `@classmethod` 데코레이터를 사용한다. 

```python
class TestClass:
    name = "TestClass"  # 클래스 변수 선언
    __priv_name = "Private TestClass"  # 클래스 변수 선언

    @classmethod
    def test_class(cls) -> None:
        print("\n  [Class method]")
        print(cls.name)  # 클래스 변수 접근 가능
        print(cls.__priv_name)  # 클래스 변수 접근 가능
```

이때, 인스턴스 메소드를 생성할 때 `self`를 사용하는 것과 유사하게 `cls`를 사용한다. 

인스턴스 메소드에서 `self`를 이용하여 인스턴스 변수와 메소드에 접근 가능한 것처럼 `cls`를 이용하여 클래스 변수(`name`, `__priv_name`)에 접근이 가능하다. 

> 인스턴스 메소드에서 `self`를 이용하면 인스턴스 변수와 메소드 뿐만 아니라 클래스 변수와 메소드도 접근 가능하다.
{: .notice--info}

> `cls` 대신에 `self`로 작성하여 만들어도 `cls`와 동일하게 작동한다. 
> 하지만 인스턴스 메소드의 `self`와는 다른 것이기 때문에 구분을 위해 `cls`를 사용한다. 
{: .notice--info}

## (2) 사용

클래스 메소드도 아래 코드와 같이 인스턴스를 생성하지 않고 변수와 메소드를 사용할 수 있다. 

```python
TestClass.test_static()
TestClass.test_class()
print(TestClass.name)
```

인스턴스 변수나 메소드에는 접근하지 못하고 클래스 변수와 메소드에만 접근이 가능하다. 


<br/>

