---
title: "[Python] 가상 환경 설정 (venv)"

sidebar:
    nav: "dev"
---

<br/>


파이썬을 사용하여 여러 프로젝트를 다루다보면 패키지들의 버전 문제가 거의 항상 발생한다.

이런 문제를 해결하기 위해 `venv`을 이용하면 프로젝트 마다 서로 다른 환경에서 개발이 가능하다.

<br/>


# 1. 가상 환경 만들기

만들고자 하는 임의의 `${환경이름}`을 넣어 명령을 실행하면 `${환경이름}` 폴더가 생성되고, 가상 환경 상에서 설치하는 패키지들은 이 폴더에 저장된다. 

`python` 명령어 대신 `py -${파이썬 버전}`을 사용하면 여러 파이썬 버전 중에서 특정 버전을 선택하여 가상 환경을 만들어 사용할 수 있다. 

```bash
$ python -m venv ${환경이름}
$ python -m venv _venv_         # 예시
$ py -3.10 -m venv _venv_       # 파이썬 특정 버전 (예시: python 3.10) 적용 시 
```

<br/>


# 2. 가상 환경 시작 (Activate)

가상 환경을 실행하기 위해서는 아래 명령어를 통해 activate 해야 한다.

## (1) Ubuntu

```bash
$ source ${환경이름}/bin/activate
```

## (2) Windows

```bash
$ ./${환경이름}/Scripts/activate
```

가상 환경을 activate 하면 터미널 앞에 `(${환경이름})` 글자가 붙는다. 

<br/>


# 3. 가상 환경 종료 (Deactivate)

가상 환경이 activate 된 상태에서 deactivate 명령을 실행하면 가상 환경이 종료된다. 

```bash
$ deactivate
```

<br/>