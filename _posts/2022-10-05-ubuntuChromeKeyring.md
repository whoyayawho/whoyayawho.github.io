---
title: "[Ubuntu] 크롬(Chrome) Unlock Login keyring 팝업 및 Keyring 삭제"

sidebar:
    nav: "ubuntu"
---

<br/>

# 1. Unlock Login keyring 팝업 해제

우분투 자동로그인을 해두면 크롬 브라우저를 실행할 때 매번 keyring을 묻는 팝업이 뜬다.

Keyring을 묻는 팝업이 안 뜨도록 하기 위해 찾아보았지만 결론은 **자동로그인을 해제**하는 것으로 해결하기로 했다.

<br>


# 2. Keyring 삭제

기존에 Keyring을 한 번 등록해두면 자동로그인을 해제해도 계속 Keyring을 묻는 팝업이 뜬다.

그런 경우에 아래 명령어를 통해 Keyring을 삭제한다.

```bash
$ sudo rm -r ~/.local/share/keyrings/*
```

<br>

