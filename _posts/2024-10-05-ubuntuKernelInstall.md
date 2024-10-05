---
title: "[Ubuntu] 와이파이 안 되는 문제 해결 (우분투 커널 버전 올리기)"

sidebar:
    nav: "ubuntu"

toc: true
---

<br/>

# 1. 개요

새로 노트북을 구매해서 우분투를 설치하다 보면 와이파이가 안 되는 경우가 자주 있다. 

그런 경우는 우분투에서 자동으로 설치하는 드라이버가 노트북의 와이파이 모듈을 지원하지 않는 경우이다.

와이파이 드라이버만 따로 구해서 설치해주는 것도 해결 방법이지만, 더 높은 버전의 우분투 커널을 설치해주는 것이 더 간단하다. 

<br/>


# 2. Mainline

`Mainline`을 설치하여 이용하면 우분투 커널을 여러 버전 설치 및 관리를 간편하게 할 수 있다. 

## (1) 설치

아래 명령어를 순차적으로 실행하여 Mainline을 설치한다. 

```bash
$ sudo add-apt-repository ppa:cappelikan/ppa
$ sudo apt update && sudo apt upgrade -y
$ sudo apt install -y mainline
```

## (2) 삭제

설치했던 Mainline을 삭제하기 위해서는 아래 명령어를 순차적으로 실행한다. 

```bash
$ sudo add-apt-repository --remove ppa:cappelikan/ppa
$ sudo apt remove mainline
```

<br/>


# 3. 커널 설치 및 실행

Mainline을 실행하면 아래 화면과 같이 창이 뜬다. 

![]({{ site.url }}/assets/images/241005/figure1.png){: width="80%" .align-center}

화면에서 원하는 커널 버전을 선택한 후에 Install 버튼을 눌러 커널을 설치한다.

설치한 커널을 삭제할 때는 삭제할 커널을 선택한 후에 Uninstall 버튼을 눌러 삭제한다. 

커널 버전에 따라 문제가 발생하기도 하는데 문제가 발생하면 다른 버전을 다시 시도해보면 된다. 

> 커널을 여러 버전 설치한 후에 재부팅하면 가장 높은 버전의 커널이 자동으로 선택된다. 
> 설치한 여러 버전의 커널 중에서 원하는 특정 버전을 실행하고 싶다면 부팅할 때 `Advanced options for Ubuntu` 옵션을 선택하여 커널 버전을 선택할 수 있다. 
{: .notice--info}

<br/>