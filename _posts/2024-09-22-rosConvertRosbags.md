---
title: "[ROS] rosbag 파일 변환 (ROS1 <-> ROS2)"

sidebar:
    nav: "dev"

toc: true
---

<br/>


ROS1에서 저장한 rosbag 파일을 ROS2에서 사용하거나, ROS2에서 저장한 rosbag 파일을 ROS1에서 사용하기 위해서는 서로 변환이 필요하다. 

<br/>

# 1. `rosbags` 설치 

`rosbags`패키지를 설치하여 사용하면 ROS1 <-> ROS2 rosbag 파일 변환이 간단하다. 

파이썬 패키지이기 때문에 pip로 설치한다. (파이썬 설치 필요)

```bash
$ pip install rosbags
```

<br/>


# 2. ROS1의 rosbag 파일을 ROS2 형식으로 변환 

아래 명령어를 통해 ROS1의 rosbag 파일을 ROS2 형식으로 변환할 수 있다. 

```bash
$ rosbags-convert foo.bag                       # Convert "foo.bag", result will be "foo/"
$ rosbags-convert foo.bag --dst /path/to/bar    # Convert "foo.bag", save the result as "bar"
$ rosbags-convert foo.bag --exclude_topics ${제외할 토픽}
$ rosbags-convert foo.bag --include_topics ${포함할 토픽}
$ rosbags-convert foo.bag --exclude_msgtypes ${제외할 메시지 타입}
$ rosbags-convert foo.bag --include_msgtypes ${포함할 메시지 타입}
```

<br/>


# 3. ROS2의 rosbag 파일을 ROS1 형식으로 변환 

아래 명령어를 통해 ROS2의 rosbag 파일을 ROS1 형식으로 변환할 수 있다. 

```bash
$ rosbags-convert bar                           # Convert "bar", result will be "bar.bag"
$ rosbags-convert bar --dst /path/to/foo.bag    # Convert "bar", save the result as "foo.bag"
$ rosbags-convert bar --exclude_topics ${제외할 토픽}
$ rosbags-convert bar --include_topics ${포함할 토픽}
$ rosbags-convert bar --exclude_msgtypes ${제외할 메시지 타입}
$ rosbags-convert bar --include_msgtypes ${포함할 메시지 타입}
```

<br/>
