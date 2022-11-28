---
title: "[Python] 파이썬 없이 파이썬3만 설치되어 있는 경우 오류 해결 (/usr/bin/env: 'python': No such file or directory)"

sidebar:
    nav: "dev"
---

<br/>


`Python3`만 설치되어 있는 경우에 python을 실행하다보면 `/usr/bin/env: 'python': No such file or directory` 같은 오류가 발생하는 경우가 있다.

이럴 때는 아래와 같이 두 가지 방법 중 하나를 실행하면 해결된다.

# 1. `python-is-python3` 설치

python을 python3로 연결해주는 패키지를 설치한다. 

```bash
$ sudo apt install python-is-python3
```

<br/>


# 2. `ln`을 이용한 연결

버전에 따라 `python-is-python3` 패키지가 설치가 안 될 수 있다.

그런 경우에는 아래와 같이 `ln` 명령어를 이용하여 python을 python3로 연결해준다.

```bash
$ sudo ln -s /usr/bin/python3 /usr/local/bin/python
```

<br/>