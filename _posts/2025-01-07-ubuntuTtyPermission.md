---
title: "[Ubuntu] tty 권한 설정 및 항상 유지(/dev/tty*)"

sidebar:
  nav: "ubuntu"
---

<br/>

# 1. 개요

우분투를 사용해서 개발을 하다 보면 (특히, USB 시리얼통신 할 때) `/dev/tty*`의 권한을 설정할 일이 많다.

한 번 권한 설정을 해도 재부팅을 하면 다시 권한을 설정해줘야 한다.

매번 권한 설정하기가 귀찮거나, 부팅 시에 프로그램을 자동으로 실행해야 하는 경우에 아래와 같이 항상 권한을 갖도록 설정한다.

<br/>

# 2. 모든 tty 권한 일괄 설정

아래 명령어를 통해 `dialout` 그룹에 사용자를 추가하면 모든 tty 권한을 일괄 설정할 수 있다.

```bash
sudo usermod -aG dialout $USER
```

<br/>

# 3. 특정 USB 장치에 대해서만 권한 설정

다른 tty에 대한 권한은 그대로 유지하고, 특정 USB 장치에 대해서만 권한을 설정할 수도 있다.

## (1) 특정 USB 장치 정보 확인

아래 명령어를 실행해서 원하는 특정 USB 장치의 `idVendor`, `idProduct` 값을 확인한다.

`ID {idVendor}:{idProduct}` 형식으로 표시된다.

```bash
lsusb
```

## (2) 특정 USB 장치에 대해서만 권한 설정

`/etc/udev/rules.d/99-usb-serial.rules` 파일을 생성해서 아래 내용을 작성한다.

```
SUBSYSTEM=="tty", ATTRS{idVendor}=="{idVendor}", ATTRS{idProduct}=="{idProduct}", MODE="0666", GROUP="dialout"
```

`"{idVendor}"`와 `"{idProduct}"`는 위에서 확인한 값을 넣어준다.

## (3) 권한 설정 적용

아래 명령어를 통해 수정 내용을 적용한다.

```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

<br/>
