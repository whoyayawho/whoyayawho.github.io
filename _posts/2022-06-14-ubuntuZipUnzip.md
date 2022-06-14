---
title: "[Ubuntu] 압축/압축풀기 (zip, unzip, tar)"

sidebar:
    nav: "ubuntu"
---

<br/>


우분투에서 압축/압축풀기를 하기 위해 `.zip` 또는 `.tar` 형식을 사용한다.


# 1. zip / unzip

## (1) zip 압축

```bash
$ zip ${file_name}.zip -r ${folder_name}
```

> `aaa` 폴더 전체를 `aaa.zip`으로 압축 예시
> ```bash
> $ zip aaa.zip -r ./aaa
> ```
{: .notice--info}

## (2) zip 압축풀기 (unzip)

```bash
$ unzip ${file_name}.zip
```


<br/>


# 2. tar

## (1) tar 압축

```bash
$ tar -cvf ${file_name}.tar ${folder_name}
```

> `aaa` 폴더 전체를 `aaa.tar`으로 압축 예시
> ```bash
> $ tar -cvf aaa.tar ./aaa
> ```
{: .notice--info}

## (2) tar.gz 압축

```bash
$ tar -zcvf ${file_name}.tar.gz ${folder_name}
```

> `aaa` 폴더 전체를 `aaa.tar.gz`으로 압축 예시
> ```bash
> $ tar -zcvf aaa.tar.gz ./aaa
> ```
{: .notice--info}

## (3) tar 압축풀기

```bash
$ tar -xvf ${file_name}.tar
```

## (4) tar.gz 압축풀기

```bash
$ tar -zxvf ${file_name}.tar.gz
```

## (5) tar 옵션

| 옵션 | 설명 |
| :---: | :---: |
| -c | 파일을 tar로 압축 |
| -p | 파일 권한을 지정 |
| -v | 압축/압축풀기 과정을 화면으로 출력 |
| -f | 파일 이름을 지정 |
| -C | 경로를 지정 |
| -x | tar 압축풀기 |
| -z | gzip으로 압축/압축풀기 |




<br/>


