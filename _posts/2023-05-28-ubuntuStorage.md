---
title: "[Ubuntu] 디스크, 폴더, 파일의 용량 크기 확인"

sidebar:
    nav: "ubuntu"

toc: true
---

<br/>

우분투(Ubuntu)에서 디스크의 현재 사용량과 남은 용량을 확인하거나 폴더 또는 파일의 크기를 확인하기 위해서는 아래와 같은 명령어를 사용한다. 


# 1. 디스크 별 용량 확인 

```bash
df -h
```

<br/>


# 2. 특정 디렉토리 용량 확인

```bash
du -hs folder_name
```

<br/>


# 3. 현재 폴더에 있는 폴더 및 파일 용량 확인

```bash
du -hs *
```

<br/>