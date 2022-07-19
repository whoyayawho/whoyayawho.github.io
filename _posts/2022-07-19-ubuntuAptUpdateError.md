---
title: "[Ubuntu] apt update 실패 (DNS 설정)"

sidebar:
    nav: "ubuntu"
---

<br/>

`apt update` 명령어를 실행할 때 아래 내용이 포함되어 실패하는 경우가 있다.

```bash
Temporary failure resolving 'ports.ubuntu.com'
```

인터넷에 문제가 없는데 위와 같은 오류가 나온다면 DNS 문제일 수가 있다.

아래와 같이 두 가지 파일을 수정하여 다시 `apt update`를 시도해본다.

```bash
$ echo "dns-nameservers 8.8.8.8 8.8.4.4" >> /etc/network/interfaces
$ echo "nameserver 8.8.8.8" >> /etc/resolv.conf
$ echo "nameserver 8.8.4.4" >> /etc/resolv.conf
```


<br/>