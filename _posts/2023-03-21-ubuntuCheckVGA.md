---
title: "[Ubuntu] 장착된 그래픽카드 확인"

sidebar:
    nav: "ubuntu"

toc: false
---

<br>


그래픽카드 드라이버가 설치되어 있다면 `nvidia-smi` 같은 명령어를 통해 그래픽카드를 확인할 수 있다.

그러나 드라이버가 설치되어 있지 않은 상태에서 장착된 그래픽카드를 확인하기 위해서는 아래 명령어를 실행하면 된다.

```bash
$ lspci | grep -i VGA
```

<br>

