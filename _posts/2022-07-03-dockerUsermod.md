---
title: "[Docker] Visual Studio Code에서 Docker가 보이지 않음 (Docker 사용자 그룹 추가)"

sidebar:
    nav: "ubuntu"
---

<br/>


Visual Studio Code를 사용하면 Extension을 활용하여 Docker를 편하게 사용할 수 있다.

하지만 Docker가 설치되어 있지 않다던가 권한 문제가 있다는 등의 이유로 Docker의 Image, Container가 보이지 않는 경우가 있다.


# 1. Docker 사용자 그룹 추가 

Docker가 잘 설치되어 있는데도 문제가 있다는 경우에는 아래 명령어를 사용하여 Docker 사용자 그룹을 추가하면 문제가 해결된다.

```bash
$ sudo groupadd docker
$ sudo usermod -aG docker $USER 
```

<br/>


