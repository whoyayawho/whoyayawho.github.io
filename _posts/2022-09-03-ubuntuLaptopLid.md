---
title: "[Ubuntu] 노트북 덮었을 때 절전모드 진입 끄기"

sidebar:
    nav: "ubuntu"
---

<br/>

# 1. `logind.conf` 파일 수정

`/etc/systemd/logind.conf` 파일에서 아래 부분을 찾아 수정

```bash
#HandleLidSwitch=suspend
```

위 부분을 아래와 같이 수정

```bash
HandleLidSwitch=ignore
```

수정 후에 아래 명령 실행

```bash
systemctl restart systemd-logind
```

<br>

