---
title: "[Windows] \"이 사진에 대한 자세한 정보\" 아이콘 삭제 (배경화면 Windows 추천)"

sidebar:
    nav: "windows"

toc: true
---

<br/>

# 1. 개요

윈도우에서는 배경화면을 "Windows 추천"으로 설정할 수 있다. 

추천 배경화면으로 설정하면 일정 시간 마다 자동으로 고화질의 멋진 사진으로 수시로 변경된다.

그런데 추천 배경화면으로 설정하면 배경화면에 아래와 같은 아이콘이 생긴다. 

![]({{ site.url }}/assets/images/240924/image.png){: .align-center}

배경화면의 아이콘을 없애기 위해서는 아래와 같이 레지스트리를 수정한다. 

<br/>

# 2. 바탕화면 아이콘 없애기

## (1) 레지스트리 편집기 열기

`win + R`키를 눌러 실행 창을 연 후에 `regedit` 명령어를 쳐서 레지스트리 편집기를 연다. 

![]({{ site.url }}/assets/images/240924/image2.png){: width="60%" .align-center}

또는, 시작 버튼을 눌러 `레지스트리 편집기`를 검색해서 열어도 된다. 


## (2) 레지스트리 생성 및 수정

### a. 레지스트리 위치 찾기

레지스트리 편집기에서 아래 위치를 찾는다. 

`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\HideDesktopIcons\NewStartPanel`


### b. 레지스트리 생성

`NewStartPanel`에서 오른쪽 버튼을 눌러 `DWORD(32비트) 값`을 새로 만든다. 

![]({{ site.url }}/assets/images/240924/image3.png){: .align-center}


### c. 레지스트리 수정

새로 생성한 레지스트리의 이름을 `{2cc5ca98-6485-489a-920e-b3e88a6ccce3}`으로 수정하고, 해당 레지스트리를 더블클릭하여 값을 1로 설정한다.

![]({{ site.url }}/assets/images/240924/image4.png){: width="100%" .align-center}

![]({{ site.url }}/assets/images/240924/image5.png){: width="100%" .align-center}


<br/>


# 3. 결과 확인

레지스트리를 수정한 후에 배경화면을 새로고침 하면 아이콘이 없어진 것을 확인할 수 있다. 

<br/>