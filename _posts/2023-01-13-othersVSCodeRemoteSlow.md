---
title: "[Others] VS Code Remote Server 다운로드 문제 해결 방법 (접속이 안 되면)"

sidebar:
    nav: "dev"
---

<br>


# 1. 개요

Visual Studio Code에서 굉장히 유용하게 사용하는 기능 중에 하나가 `Remote` 기능이다.

VS Code에서 WSL, Docker, SSH 등 접속을 할 때 Remote 기능을 사용하여 접속하면 굉장히 편하다.

로컬에서 VS Code를 사용하는 것과 같은 경험을 WSL, Docker, SSH 등을 통해서 똑같이 할 수 있다.

파일 브라우징, 터미널 작업이 편한 것도 있지만 원격으로 파일 다운로드, 업로드가 정말정말정말 편하다.

원래 WSL, Docker, SSH 통해서 파일 업로드 또는 다운로드 하려면 명령어 치는게 정말 귀찮다.

하지만 VS Code Remote로 접속하면 그냥 로컬 파일을 드래그하면 업로드가 되고 오른쪽 버튼 눌러 다운로드를 하면 파일을 가져올 수 있다. 

그래서 정말 정말 정말 필수 기능 중 하나인데 가끔 Remote 접속을 하려는데 한참을 기다려도 접속이 안 되는 경우가 있다.

이유는 버그 때문인지 (아시아에서 MS 서버에 접속할 때 발생하는 문제라서 다른 지역으로 바꿔서 접속하면 문제 없어진다는 이야기도 있다.) Remote Server를 접속 대상에 설치해야 하는데 이게 굉장히 오래 걸리는 경우가 있다. 

또는 인터넷 환경이 아닌데 접속하려는 경우가 있을 수 있다. 

이런 경우에는 Remote Server 파일을 수동으로 다운로드 받아, 수동으로 접속 대상에 올려서 설치해야 한다. 

<br>


# 2. Remote Server 다운로드

Remote Server 설치 파일을 수동으로 다운로드 하기 위해서는 아래 주소로 접속하면 된다.

```bash
https://update.code.visualstudio.com/commit:${COMMIT_ID}/server-linux-x64/stable
https://update.code.visualstudio.com/commit:${COMMIT_ID}/server-linux-arm64/stable
```

플랫폼에 따라 x64, arm64에 맞춰 다운로드 한다.

이때 `${COMMIT_ID}`를 다운로드 하고자 하는 Remote Server Commit id에 맞춰 수정을 해줘야 한다.

이 값을 확인하기 위해서는 VS Code에서 remote 접속 시도할 때 log를 확인하면 된다.

log에 보면 어떤 commit id의 remote server를 설치하려고 한다는 메시지를 확인할 수 있다. 

<br>


# 3. Remote Server 설치 파일 복사 이동

설치 파일을 다운로드 받았다면 이 파일을 접속하고자 하는 원격 대상의 아래 경로로 복사 이동한다.

```bash
~/.vscode-server/bin/$COMMIT_ID
```

<br>


# 4. 설치 파일 압축 해제

복사한 경로의 폴더에서 아래 명령어로 복사한 파일의 압축을 해제한다.

```bash
$ tar -xvzf vscode-server-linux-x64.tar.gz --strip-components 1
```

<br>