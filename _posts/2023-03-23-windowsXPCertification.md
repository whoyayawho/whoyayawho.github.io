---
title: "[Windows] XP 정품 인증 문제 해결"

sidebar:
    nav: "windows"

toc: true
---

<br/>


# 1. 개요

Windows XP가 워낙 오래되서 모든 지원이 끊겼다.

그런데 아직도 가끔 XP를 사용해야 하는 장비들이 있다. (왜 아직도 XP를 쓰나요? 이제 윈도우 버전 업데이트를 합시다!!)

그래서 발생하는 문제는 windows XP 정품 시디와 시디키가 있어도 정품 인증이 안 된다는 것이다. (인증 방법이 MS 서버 인증이나 전화 인증인데 모두 지원이 안 된다.)

그럼 부팅할 때 정품 인증하라고 하면서 윈도우 바탕화면을 볼 수가 없다.

마이크로소프트에 전화해서 물어봐도 결국 해결 방법은 없었다. (이제 XP 관련 부서가 없어서 전화 연결도 못 해준다고 한다.)

이런 경우에 정품 인증 없이 사용할 수 있는 기한을 초기화 하는 방법이 가능하다.

한 달 마다 연장을 해줘야 하는데 1년에 한 두어번 쓰는 정도라서 이런 방법을 이용한다.

만약 자주 써야 한다면 크랙을 이용하는게 나을 것 같다. (다른 방법이 없다.)

<br/>


# 2. 인증 기한 초기화 방법

## (1) Safe Mode로 부팅

컴퓨터 전원을 켜고 F8 등의 버튼(PC 마다 다를 수 있다.)을 통해 부팅 옵션을 안전 모드(Safe Mode) 부팅으로 변경한다.

## (2) 명령 프롬프트(Command Prompt)에서 아래 명령어 실행

명령 프롬프트를 찾아 실행한 후에 아래 명령어를 입력하고 재부팅한다.

```bash
rundll32.exe syssetup,SetupOobeBnk
```

<br/>