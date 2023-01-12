---
title: "[Python] requirements.txt 만들기 & 사용하기"

sidebar:
    nav: "dev"
---

<br/>


# 1. 개요

파이썬에서는 `pip` 명령어로 필요한 패키지를 설치한다.

`pip list` 명령을 실행하면 설치된 패키지를 확인할 수 있다.

다른 환경에서 프로젝트를 실행하려면 다시 이러한 패키지를 설치해야 한다.

하나씩 설치하려면 힘들겠지만 `requirements.txt` 파일을 이용하면 이러한 작업을 쉽게 할 수 있다. 

<br/>


# 2. `requirements.txt` 만들기

아래 명령어를 실행하면 현재 설치되어 있는 패키지 목록이 작성된 `requirements.txt` 파일이 만들어진다.

```bash
$ pip freeze > requirements.txt
```

<br/>


# 3. `requirements.txt` 이용해 패키지 설치하기

아래 명령어를 실행하면 목록에 있는 패키지들이 설치된다.

```bash
$ pip install -r requirements.txt
```

<br/>