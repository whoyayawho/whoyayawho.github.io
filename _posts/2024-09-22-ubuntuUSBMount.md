---
title: "[Ubuntu] USB 외장하드, SSD 등 마운트(Mount) 안 되는 문제 해결"

sidebar:
    nav: "ubuntu"

toc: true
---

<br/>


우분투에서 usb 외장하드나 SSD를 사용하려는데 마운트가 안 되는 경우가 있다. 

이럴 때, 아래와 같이 수동으로 마운트를 직접 해주면 해결되는 경우가 있다. 

<br/>


# 1. USB 외장하드 또는 SSD 확인 

아래 명령어를 실행하면 현재 연결되어 있는 디스크를 확인 할 수 있는데 USB 외장하드나 SSD도 확인이 가능하다. 

```bash
$ sudo fdisk -l
```

위의 명령어를 통해 마운트 하고자 하는 대상 디스크의 위치를 찾아야 한다. 

보통 현재 연결된 USB 디스크는 `/dev/sda1`와 같은 형태로 맨 아래에 표시된다. 

<br/>


# 2. 마운트(Mount)

먼저, 디스크를 마운트 할 폴더를 만든다. 

그 후에 mount 명령어를 통해 해당 폴더에 대상 디스크를 마운트 한다. 

```bash
$ sudo mkdir ~/ext_disk
$ sudo mount ${대상 디스크} ~/ext_disk
$ sudo mount /dev/sda1 ~/ext_disk         # 예시
```

<br/>


# 3. 언마운트(Umount)

USB 디스크 사용이 끝나고 언마운트 하기 위해서는 아래 명령어를 실행한다. 

```bash
$ sudo umount ~/ext_disk
```


<br/>
