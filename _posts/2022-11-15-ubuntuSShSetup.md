---
title: "[Ubuntu] 원격 접속을 위한 SSH 설정"

sidebar:
    nav: "ubuntu"
---

<br/>

# 1. 필요 패키지 설치

```bash
$ sudo apt install ssh openssh-server
```

<br/>


# 2. `sshd_config` 파일 수정

아래 명령어를 실행하여 `sshd_config` 파일 수정

```bash
$ sudo vim /etc/ssh/sshd_config
```

## (1)  `PermitRootLogin` 부분을 주석 해제하고 아래와 같이 yes 설정

```
PermitRootLogin yes
```

## (2)  `Port 22` 부분을 주석 해제하고 아래와 같이 원하는 포트 번호로 설정

```
Port 1234
```

<br/>