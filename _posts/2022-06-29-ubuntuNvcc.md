---
title: "[Ubuntu] NVCC로 CUDA 버전 확인하기"

sidebar:
    nav: "ubuntu"
---

<br/>


CUDA가 설치되어 있으면 NVCC 명령어로 CUDA 버전을 확인할 수 있다.


# 1. NVCC로 버전 확인

아래 명령어를 사용하여 CUDA 버전을 확인할 수 있다.

```bash
$ nvcc -V
```

<br/>


# 2. NVCC 명령어가 동작 안 할 때

CUDA가 잘 설치되어 있는데 NVCC 명령어가 동작을 안 하면 `~/.bashrc` 파일에 아래와 같이 추가한다.

`cuda-11.0` 뒤의 숫자는 CUDA 버전에 맞춰 수정한다.

```bash
export PATH="/usr/local/cuda-11.0/bin:$PATH"
export LD_LIBRARY_PATH="/usr/local/cuda-11.0/lib64:$LD_LIBRARY_PATH"
```

<br/>


