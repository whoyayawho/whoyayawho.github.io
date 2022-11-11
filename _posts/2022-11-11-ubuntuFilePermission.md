---
title: "[Ubuntu] 파일 소유 및 권한 수정 (chown & chmod)"

sidebar:
    nav: "ubuntu"
---

<br/>

# 1. 파일 소유 변경

아래 명령어를 통해 하위 파일 및 폴더의 소유를 현재 유저(`$USER`)로 변경한다.

```bash
sudo chown -R $USER:$USER ./*
```

<br/>


# 2. 파일 권한 변경

아래 명령어를 통해 하위 파일 및 폴더의 권한을 775로 변경한다.

```bash
sudo chmod -R 775 ./*
```

<br/>