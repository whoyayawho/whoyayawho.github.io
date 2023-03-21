---
title: "[Windows] VS Code에서 PowerShell UnauthorizedAccess 오류 해결"

sidebar:
    nav: "windows"

toc: false
---

<br/>


Visual Studio Code에서 터미널 창을 열면 PowerShell이 실행된다. 

그런데 이때 권한 문제로 UnauthorizedAccess 오류가 뜨는 경우가 있다. 

그런 경우에는 아래와 같이 권한 설정을 한다. 

- 관리자 모드로 PowerShell 실행

- `Set-ExecutionPolicy RemoteSigned` 명령어 실행  
`A`를 눌러 모두 예를 선택한다.

- `Get-ExecutionPolicy` 명령어를 실행하여 확인

<br/>
