---
title: "[Ubuntu] .AppImage 파일 실행 및 설치 (프로그램 목록에 표시)"

sidebar:
  nav: "ubuntu"

toc: true
---

<br/>

# 1. 개요

우분투에서 프로그램을 다운로드 받으면 dep 파일로 받는 경우도 있지만 AppImage 파일로 받는 경우가 있다.

dep 파일은 apt 명령어로 설치를 하면 되지만, AppImage는 설치 파일이 아닌 실행 파일이기 때문에 다른 방법으로 실행해야 한다.

그리고 AppImage 파일 자체가 실행 파일이기 때문에 다른 설치 프로그램처럼 사용하려면 추가적인 작업을 해야 한다.

<br/>

# 2. 실행

.AppImage 프로그램 실행은 권한 설정하고 그대로 실행하면 된다.

```bash
$ sudo chmod 775 {AppImage 파일 이름}.AppImage
$ ./{AppImage 파일 이름}.AppImage
```

> 실행하는데 libfuse.so.2 에러가 발생하면 설치를 해준다.
>
> ```bash
> $ sudo apt install libfuse2
> ```
>
> {: .notice--info}

<br/>

# 3. 프로그램 목록에 추가

AppImage 파일은 실행 파일이기 때문에 프로그램 목록에서 확인할 수 없다.

프로그램 목록에 추가를 하기 위해 아래 명령어를 순차적으로 실행한다.

## (1) opt 폴더에 이동

```bash
$ sudo mv {AppImage 파일 이름}.AppImage /opt/{AppImage 파일 이름}.appimage
```

## (2) 아이콘 파일 opt 폴더로 이동

아이콘으로 만들 파일을 opt 폴더로 이동한다.

```bash
$ sudo mv {AppImage 파일 이름}.png /opt/{AppImage 파일 이름}.png
```

## (3) Desktop entry 파일 생성

`/usr/share/applications/{AppImage 파일 이름}.desktop` 파일을 생성하여 아래 내용을 작성한다.

```bash
[Desktop Entry]
Name={AppImage 파일 이름}
Exec=/opt/{AppImage 파일 이름}.appimage
Icon=/opt/{AppImage 파일 이름}.png
Type=Application
Categories=Development;
```

<br/>
