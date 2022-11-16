---
title: "[Ubuntu] 쉘스크립트 자동 실행 등록 및 더블 클릭 실행 (feat. Docker, ROS)"

sidebar:
    nav: "ubuntu"
---

<br/>


# 1. 부팅 시에 자동 실행 (systemd 서비스 등록)

systemd 서비스 등록을 하면 부팅 중 로그인 하기 전에 원하는 스크립트를 자동실행하도록 할 수 있다.

> 로그인 전에 실행하기 때문에 로그인 후에 필요한 기능(GUI 이용하는 프로그램 등)은 동작하지 않는다.
{: .notice--warning}

## (1) systemd 서비스 등록

### a. `.service` 파일 작성

아래 명령어를 실행하여 `custom_script_run.service` 파일을 새로 만들어 작성한다.

파일명은 원하는대로 작성한다.

```bash
$ sudo vim /etc/systemd/system/custom_script_run.service
```

파일의 내용은 아래와 같이 작성한다.

부팅 중에 자동으로 `/usr/bin/custom_docker_run.sh` 스크립트를 실행하는 내용이다.

```bash
[Unit]
Description=Docker Run
Requires=docker.service
After=docker.service

[Service]
Type=forking
User=${user name}
Restart=on-failure
RestartSec=1s
ExecStart=/usr/bin/custom_docker_run.sh

[Install]
WantedBy=multi-user.target
```

> `${user name}`은 로그인 계정 이름으로 설정한다.
{: .notice--info}


### b. 서비스 등록

아래 명령어를 실행하면 서비스가 등록되어 부팅 중에 실행된다.

```bash
$ systemctl enable custom_script_run.service
```



## (2) 자동 실행 할 스크립트 작성 (docker 실행하는 스크립트 예시)

### a. 스크립트 작성

부팅 중에 자동 실행하고자 하는 `custom_docker_run.sh` 파일을 만들어 작성한다.

```bash
$ sudo vim /usr/bin/custom_docker_run.sh
```

아래와 같이 내용 작성을 하면 사전에 만들어둔 `ros_melodic` 이름의 도커 컨테이너를 실행하고, 컨테이너 내부에서 `/root/ros_ws/src/run.sh` 스크립트를 실행한다.

```bash
#!/bin/bash

docker start ros_melodic;

sleep 1;

docker exec ros_melodic sh /root/ros_ws/src/run.sh;

exit 0;
```

### b. 권한 설정

내용 작성 후에는 아래와 같이 권한 설정을 해준다.

```bash
$ sudo chmod 775 /usr/bin/custom_docker_run.sh
```

## (3) 컨테이너 내부에서 실행할 스크립트 예시 (ROS 패키지 실행 예시)

위 과정을 통해 부팅 중에 컨테이너 내부의 `/root/ros_ws/src/run.sh` 스크립트를 자동 실행하도록 만들었다.

컨테이너 안에서 아래 명령어를 통해 `/root/ros_ws/src/run.sh` 스크립트를 생성하고 작성한다.

```bash
$ vim /root/ros_ws/src/run.sh
```

`tmux`를 통해 ROS 패키지를 실행하는 스크립트 예시는 아래와 같이 작성한다.

```bash
#!/bin/bash

source /opt/ros/melodic/setup.bash;
source /root/ros_ws/devel/setup.bash;

tmux new-session -d -s whoyayawho;
tmux new-window -t whoyayawho:1;
tmux new-window -t whoyayawho:2;
tmux new-window -t whoyayawho:3;

tmux send -t whoyayawho:1 "cd /root/ros_ws/src/package1/launch; roslaunch --wait ./package1.launch" C-m
tmux send -t whoyayawho:2 "cd /root/ros_ws/src/package2/launch; roslaunch --wait ./package2.launch" C-m
tmux send -t whoyayawho:3 "cd /root/ros_ws/src/package3/launch; roslaunch --wait ./package3.launch" C-m
tmux send -t whoyayawho:0 "cd; roscore" C-m

exit 0
```

<br/>


# 2. 로그인 시에 쉘스크립트 자동 실행 (시작프로그램 등록)

- 우분투 프로그램 중에 `Startup Applications` 프로그램 실행
- `add` 클릭
- `command` 탭에서 명령어 작성
```bash
gnome-terminal -- bash -c "/path/to/script/temp.sh; exec bash"
```

<br/>


# 3. 쉘스크립트 파일 더블클릭하여 실행

- 쉘스크립트 더블클릭 시에 실행
```bash
gsettings set org.gnome.nautilus.preferences executable-text-activation 'launch'
```

- 쉘스크립트 더블클릭 시에 실행 묻기
```bash
gsettings set org.gnome.nautilus.preferences executable-text-activation 'ask'
```

- 쉘스크립트 더블클릭 시에 코드 열기
```bash
gsettings set org.gnome.nautilus.preferences executable-text-activation 'display'
```

<br/>