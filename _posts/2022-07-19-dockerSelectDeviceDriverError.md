---
title: "[Docker] 오류 \"could not select device driver\" (nvidia-container-toolkit 설치)"

sidebar:
    nav: "dev"

toc: false
---

<br/>

Docker 컨테이너를 실행하려고 하면 아래와 같은 오류가 나오면서 실행이 안 되는 경우가 있다.

```bash
docker: Error response from daemon: could not select device driver "" with capabilities: [[gpu]].
ERRO[0050] error waiting for container: context canceled
```

이런 문제가 발생하면 `nvidia-container-toolkit`을 설치하면 해결된다.

```bash
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
$ sudo systemctl restart docker
```


<br/>