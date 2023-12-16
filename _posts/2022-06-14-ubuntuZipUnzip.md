---
title: "[Ubuntu] 압축/압축풀기 (zip, unzip, tar)"

sidebar:
    nav: "ubuntu"

toc: true
---

<br/>


우분투에서 압축/압축풀기를 하기 위해 `.zip` 또는 `.tar`을 사용한다.

`tar`는 기본적으로 설치되어 있으나 `zip`은 설치가 되어 있지 않은 경우에는 아래 명령어로 설치가 가능하다.

```bash
$ sudo apt install zip
```

<br/>


# 1. 압축하기

```bash
$ zip ${file_name}.zip -r ${folder_name}
$ tar -cvf ${file_name}.tar ${folder_name}
$ tar -Zcvf ${file_name}.tar.Z ${folder_name}
$ tar -zcvf ${file_name}.tar.gz ${folder_name}
$ tar -jcvf ${file_name}.tar.bz2 ${folder_name}
$ tar -Jcvf ${file_name}.tar.xz ${folder_name}
```

<br/>


# 2. 압축해제

```bash
$ unzip ${file_name}.zip
$ tar -xvf ${file_name}.tar
$ tar -Zxvf ${file_name}.tar.Z
$ tar -zxvf ${file_name}.tar.gz
$ tar -jxvf ${file_name}.tar.bz2
$ tar -Jxvf ${file_name}.tar.xz
```

<br/>


# 3. tar 옵션

| 옵션 | 설명 |
| :---: | :---: |
| -c | tar 압축 |
| -x | tar 압축풀기 |
| -v | 압축/압축풀기 과정을 화면으로 출력 |
| -f | 파일 이름을 지정 |
| -C | 경로를 지정 |
| -Z | compress으로 압축/압축풀기 (.Z) |
| -z | gzip으로 압축/압축풀기 (.gz) |
| -j | bzip2으로 압축/압축풀기 (.bz2) |
| -J | xz으로 압축/압축풀기 (.xz) |

<br/>


