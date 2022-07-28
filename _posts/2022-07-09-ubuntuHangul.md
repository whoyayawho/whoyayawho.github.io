---
title: "[Ubuntu/Jetson] 한글 키보드, 한영키 설정"

sidebar:
    nav: "ubuntu"
---

<br/>

PC에 Ubuntu를 새로 설치하거나 Jetson 초기 상태에서 한글을 사용할 수 없는 경우에는 한글을 설치하고 셋팅해줘야 한다. 

PC Ubuntu와 Jetson의 한영 설정 방법이 조금 다르다.

사실 PC와 Jetson의 차이라기 보다는 Jetson의 Ubuntu 버전이 다르기 때문이다.

혹시 PC에서도 Ubuntu 버전에 따라 인터페이스가 Jetson과 같다면 ["2. Jetson 한영 설정"]({{ site.url }}/ubuntuHangul/#2-jetson-한영-설정)을 참고하면 된다.


# 1. Ubuntu 한영 설정 

## (1) 한국어팩 설치

`Settings` > `Region & Language` > `Manage Installed Languages` 순서로 이동한다.

![]({{ site.url }}/assets/images/220709/hangul1.jpg){: width="40%" .align-center} 

![]({{ site.url }}/assets/images/220709/hangul2.jpg){: width="100%" .align-center} 

`Manage Installed Language` 버튼을 처음 누르면 새로운 창이 뜨면서 보통 설치할지를 묻는다.

![]({{ site.url }}/assets/images/220709/hangul3.jpg){: width="100%" .align-center} 

`Install` 버튼을 눌러 설치하고 재부팅하면 (보통) 자동적으로 한국어가 설치된다. 

![]({{ site.url }}/assets/images/220709/hangul31.jpg){: width="100%" .align-center} 

설치 및 재부팅 후에는 `한국어`가 설치되어 있는지 확인한다.

만약 자동 설치에서 한국어가 설치되지 않았다면 `Install/Remove Languages...` 버튼을 눌러 `Korean`을 찾아 `Installed` 체크한 후에 `Apply` 버튼을 눌러 수동 설치한다.

## (2) ibus-setup 설정

터미널 창에서 ibus-setup 명령어를 실행한다.

```bash
$ ibus-setup
```

그럼 `IBus Preferences` 창이 뜨는데 `Input Method` > `Add` > `Korean` > `Hangul` > `Add` 과정을 수행하여 한글을 추가한다.

![]({{ site.url }}/assets/images/220709/hangul4.jpg){: width="80%" .align-center}

![]({{ site.url }}/assets/images/220709/hangul5.jpg){: width="80%" .align-center}


## (3) 한글 키보드 입력 설정

다시 `Settings` > `Region & Language`으로 이동한다. 

`+` 버튼을 눌러 `Korean` > `Korean (Hangul)` > `Add` 과정을 수행하여 한글을 추가한다. 

![]({{ site.url }}/assets/images/220709/hangul6.jpg){: width="100%" .align-center}

![]({{ site.url }}/assets/images/220709/hangul7.jpg){: width="100%" .align-center}

기존 `Input Sources`에 있던 `English (US)`는 삭제한다. 


## (4) 한영키 설정

`Input Sources`에 새로 추가한 `Korean (Hangul)`옆의 톱니바퀴 버튼을 누른다.

그럼 뜨는 창에서 `Hangul Toggle Key`의 `Add` 버튼을 누른다.

그럼 새로운 창이 떠서 키를 입력하라고 한다.

키보드의 `한영키`를 눌러 입력해준다. 

`Alt_R`가 추가되었으면 잘 설정된 것이다.

![]({{ site.url }}/assets/images/220709/hangul8.jpg){: width="100%" .align-center}


<br/>


# 2. Jetson 한영 설정 

## (1) 한국어팩 설치

`System Settings` > `Language Support` 순서로 이동하면 `Language Support` 창이 뜬다.

![]({{ site.url }}/assets/images/220709/hangul_jetson1.jpg){: width="100%" .align-center}

이후의 내용은 PC Ubuntu 버전과 똑같이 설정 가능하다. (["1. Ubuntu 한영 설정"  > "(1) 한국어팩 설치"]({{ site.url }}/ubuntuHangul/#1-한국어팩-설치) 참고)

처음으로 `Language Support` 창을 열면 보통 설치할지를 묻는다.

`Install` 버튼을 눌러 설치하고 재부팅하면 (보통) 자동적으로 한국어가 설치된다.

설치 및 재부팅 후에는 `한국어`가 설치되어 있는지 확인한다.

만약 자동 설치에서 한국어가 설치되지 않았다면 `Install/Remove Languages…` 버튼을 눌러 `Korean`을 찾아 `Installed` 체크한 후에 `Apply` 버튼을 눌러 수동 설치한다.


## (2) ibus-setup 설정

ibus-setup 설정은 PC Ubuntu 버전과 똑같이 설정 가능하다. (["1. Ubuntu 한영 설정"  > "(2) ibus-setup 설정"]({{ site.url }}/ubuntuHangul/#2-ibus-setup-설정) 참고)

터미널 창에서 ibus-setup 명령어를 실행한다.

```bash
$ ibus-setup
```

그럼 `IBus Preferences` 창이 뜨는데 `Input Method` > `Add` > `Korean` > `Hangul` > `Add` 과정을 수행하여 한글을 추가한다.


## (3) 한글 키보드 입력 설정

먼저 `Text Entry` 창을 연다.

`+` 버튼을 누르고 `Korean (Hangul) (IBus)`을 찾아 선택하여 `Add` 버튼을 눌러 추가한다.

기존에 있던 언어는 삭제한다.

![]({{ site.url }}/assets/images/220709/hangul_jetson2.jpg){: width="100%" .align-center}


## (4) 한영키 설정

`System Settings` > `Keyboard`를 실행한다.

새롭게 뜨는 `Keyboard` 창에서 `Shortcuts` > `Typing`으로 이동하여 아래와 같이 각 설정 값을 변경한다.

- 모든 항목(`Switch to next source`, `Switch to previous source`, `Alternative Characters key`)을 `Disabled`로 변경 (`backspace` 키를 누르면 `Disabled`로 변경됨)
- `Compose Key` 항목을 `Right Alt` 로 변경
- `Switch to next source` 를 선택한 다음 키보드의 `한영` 키를 누름 (`Multikey` 로 변경됨)

![]({{ site.url }}/assets/images/220709/hangul_jetson3.jpg){: width="100%" .align-center}


<br/>