---
title: "[Ubuntu] 여러 버전의 파이썬 관리 (pyenv)"

sidebar:
  nav: "ubuntu"

toc: true
---

<br/>

# 1. 개요

우분투에서 프로젝트를 진행하다보면 파이썬 버전이 다르게 필요한 경우가 있다.

이럴 때, 여러 버전의 파이썬을 관리하기 위해 pyenv를 사용한다.

<br/>

# 2. `pyenv` 설치

## (1) 필수 패키지 설치

```bash
$ sudo apt update
$ sudo apt install build-essential curl
```

## (2) pyenv 설치

```bash
$ curl https://pyenv.run | bash
```

## (3) `~/.bashrc` 파일 수정

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

<br/>

# 3. 사용법

## (1) 원하는 파이썬 버전 설치

```bash
$ pyenv install 3.11.9
```

## (2) 설치되어 있는 파이썬 버전들 확인

```bash
$ pyenv versions
```

## (3) 사용할 파이썬 버전 설정

```bash
$ pyenv global 3.11.9
```

## (4) 설치된 파이썬 버전 삭제

```bash
$ pyenv uninstall 3.11.9
```

<br/>
