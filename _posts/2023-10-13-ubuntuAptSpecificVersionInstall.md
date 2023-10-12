---
title: "[Ubuntu] apt로 특정 버전 설치"

sidebar:
    nav: "ubuntu"

toc: true
---

<br/>



# 1. 특정 버전 설치

`apt`로 프로그램을 설치할 때 특정 버전을 설치할 때는 아래와 같이 명령어를 사용한다.

```bash
sudo apt install ${패키지 이름}=${설치할 버전}
```

<br/>


# 2. 설치 가능한 버전 확인

아래 명령어를 실행하면 설치 가능한 패키지의 버전을 확인할 수 있다.

```bash
sudo apt list -a ${패키지 이름}
```

<br/>
