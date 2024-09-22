---
title: "[Ubuntu] 우분투 기본 부팅 순서, timeout 변경"

sidebar:
    nav: "ubuntu"

toc: false
---

<br/>


우분투를 듀얼 부팅으로 사용할 때, 자동 부팅 되는 OS를 윈도우 또는 우분투 중에 원하는 대로 설정하고 싶은 경우가 있다.

이럴 때, `/etc/default/grub` 파일을 열어서 기본 부팅 OS와 timeout을 수정할 수 있다. 

```bash
$ sudo vim /etc/default/grub
```

파일 수정 후에는 아래 명령어를 실행해야 수정된 내용이 적용된다. 

```bash
$ sudo update-grub
```

<br/>
