---
title: "[Jetson] Jetson 상태 확인 (tegrastats, jtop)"

sidebar:
    nav: "ubuntu"

toc: true
---

<br/>



# 1. 개요

Jetson을 사용하다 보면 Ubuntu에서처럼 CPU 사용량, GPU 사용량 등과 같이 상태 확인이 필요한 경우가 있다.

이때, Ubuntu에서 사용하던 상태 확인 방법이 먹히지 않는데 그럴 때 tegrastats 명령어를 실행하여 확인 가능하다.

<br/>


# 2. tegrastats 사용법

tegrastats는 Jetson에 기본적으로 설치되어 있으니 아래 명령어로 실행하면 된다.

```bash
sudo tegrastats
```

> `--interval <int>` The interval at which tegrastats is to write output to the log, in milliseconds. The default interval is 1000 msec.  
> `--verbose`            Print verbose messages.  
> `--stop`               Stop any running instances of tegrastats.  
> `--logfile <out_file>` Dump the output of tegrastats to out_file.
{: .notice--info}

<br/>


# 3. jtop

Ubuntu의 htop과 유사하게 그랙픽적으로 확인하고 싶다면 jtop을 사용하면 된다. 

## (1) 설치

아래 명령어를 실행하여 설치한다.

```bash
sudo pip3 install -U jetson-stats
```

<br/>


## (2) 실행

아래 명령어로 실행하여 확인이 가능하다. 

```bash
jtop
```

<br/>