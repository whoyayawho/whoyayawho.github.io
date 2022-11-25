---
title: "[Jetson] 쿨링팬 구동 설정"

sidebar:
    nav: "ubuntu"
---

<br/>


# 1. 쿨링팬 구동

Jetson의 쿨링팬을 항상 돌아가도록 하려면 아래 명령어를 실행한다. 

기본적으로 최대 속도로 구동이 되는데 파일을 열어 `FAN_SPEED` 값을 0~255으로 수정하여 팬 속도를 조절한다.

```bash
$ sudo /usr/bin/jetson_clocks --fan
```

> 재부팅하면 초기화 된다.
{: .notice--info}

<br/>


# 2. 부팅 시에 `jetson_clocks` 자동 실행

## (1) 스크립트 파일 생성

`/usr/bin/run_jetson_fan.sh` 파일을 생성한다.

파일 내용은 아래와 같이 작성한다.

```bash
#!/bin/bash

sudo /usr/bin/jetson_clocks --fan

exit 0
```

## (2) 권한 설정

```bash
$ sudo chmod u+x /usr/bin/run_jetson_fan.sh
```

## (3) 서비스 파일 생성 

`/etc/systemd/system/run_jetson_fan.service` 파일을 생성한다.

파일 내용은 아래와 같이 작성한다.

```bash
[Unit]
Description=Run Jetson Fan
Requires=multi-user.target
After=multi-user.target

[Service]
Type=forking
Restart=on-failure
RestartSec=1s
ExecStart=/usr/bin/run_jetson_fan.sh

[Install]
WantedBy=multi-user.target
```

## (4) 서비스 등록

```bash
$ systemctl enable run_jetson_fan.service
```

<br/>