---
title: "[Git] submodule 사용하기"

sidebar:
    nav: "dev"

toc: true
---

<br/>

# 1. 개요

Git을 사용하다보면 이미 만들어 놓은 레포지토리를 현재 레포지토리에 가져와서 사용할 필요가 종종 있다. 

이를 위해서 사용할 레포지토리를 현재 레포지토리에 submodule로 추가하면 된다. 

<br/>


# 2. 메인 모듈에 서브 모듈 추가

서브 모듈을 추가하는 명령어를 실행하면 현재 레포지토리에 추가할 레포지토리가 서브 모듈로 추가된다. 

서브 모듈을 추가하면 해당 위치에 서브 모듈 이름의 폴더가 생성되고, 메인 모듈 폴더에 `.gitmodules` 파일이 생성된다. 

`.gitmodules` 파일에서 서브 모듈의 경로와 url 주소를 확인할 수 있다. 

```bash
$ cd {서브모듈 추가할 폴더}
$ git submodule add {서브모듈 URL}
```

<br/>


# 3. 서브 모듈 pull 

서브 모듈 pull을 하는 방법은 일반적인 git pull과 동일하다. 

```bash
$ cd {서브모듈}
$ git checkout master
$ git pull origin master
```

<br/>


# 4. 서브 모듈 push 

서브 모듈 push을 하는 방법은 일반적인 git push와 동일하다. 

다만, 서브 모듈을 수정하고 커밋을 생성했다면 메일 모듈에서도 커밋을 생성해야 한다. 

서브 모듈만 커밋하고 푸시하면 메인 모듈에서는 최근 서브 모듈 커밋이 아닌 이전 커밋을 사용한다. 

```bash
$ cd {서브모듈}
$ git add --all
$ git commit -m "{커밋내용}"
$ git push -u origin master
```

<br/>


# 5. 서브 모듈 삭제

```bash
$ git rm -f my_submodule
```

<br/>


# 6. 서브 모듈 경로 수정 

```bash
$ git mv old/path/to/module new/path/to/module
```

<br/>


# 7. 메인 모듈 clone 주의사항 

서브 모듈을 추가한 메인 모듈을 clone 할 경우에 그냥 단순히 clone 명령어만 사용하면 서브 모듈이 빈 폴더로 생성된다.

`--recurse-submodules` 옵션을 추가해서 실행해야 서브 모듈의 파일도 잘 받아진다. 

```bash
$ git clone --recurse-submodules {main module URL}
```

<br/>