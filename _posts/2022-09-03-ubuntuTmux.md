---
title: "[Ubuntu] Tmux 사용법"

sidebar:
    nav: "ubuntu"
---

<br/>

# 1. 설치

```bash
$ sudo apt install tmux
```

<br>


# 2. 단축키

| 단축키 | 설명 |
| :---: | :---: |
| Ctrl-b + % | 가로로 화면 분할 |
| Ctrl-b + " | 세로로 화면 분할 |
| Ctrl-b + 방향키 | 분할 화면 이동 |
| Ctrl-b + d | tmux detach |
| Ctrl-b + c | 윈도우 추가 |
| Ctrl-b + [ | 스크롤모드 |

<br>


# 3. 터미널 명령어

- tmux 세션을 새롭게 만들기
```bash
tmux new-session -d -s ${session 이름}
# 예) tmux new-session -d -s whoyayawho
```

- tmux 세션 목록 확인
```bash
tmux ls
```

- tmux attach
```bash
tmux attach -t ${session 이름}
# 예) tmux attach -t whoyayawho
```

- tmux 윈도우를 새롭게 만들기
```bash
tmux new-window -t ${session 이름}:${window 번호}
# 예) tmux new-window -t whoyayawho:1
# 예) tmux new-window -t whoyayawho:2
```

- tmux 윈도우에 `Ctrl-c` 키 명령 보내기
```bash
tmux send-keys -t ${session 이름}:${window 번호} C-c
# 예) tmux send-keys -t whoyayawho:1 C-c
```

<br>


# 4. 마우스 모드

tmux는 기본적으로 마우스 사용이 안 되서 사용이 불편하다. (특히, 휠 스크롤..)

하지만 마우스 모드를 켜면 마우스 휠을 통한 스크롤, 마우스 클릭을 통한 윈도우 이동 등이 가능해진다.

`~/.tmux.conf` 파일에 아래와 같이 작성

```bash
set -g mouse on
```

파일 작성 후 아래 명령어 실행을 통해 적용

```bash
$ tmux source ~/.tmux.conf
```

<br>

