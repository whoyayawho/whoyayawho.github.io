---
title: "[Python] 파일/폴더의 경로 관련 함수 (os.path)"

sidebar:
    nav: "dev"

toc: true
---

<br/>

# 1. 상대 경로를 절대 경로로 변경

상대 경로만을 사용하다보면 간혹 실행 파일의 위치에 따라 오류가 발생하는 경우가 있기 때문에 모두 절대 경로로 바꾸어 사용하는 것이 안전하다. 

파이썬을 실행할 때 `.py` 스크립트를 실행하는 경우와 `.exe` 실행파일로 만들어 실행하는 경우가 있다. 

각 방법에 따라 현재 경로를 가져오는 방법이 다르기 때문에 아래와 같이 함수로 만들어 사용하면 두 경우 모두 대응이 가능하다. 

```python
def get_abs_path(path: str) -> str:
    if getattr(sys, "frozen", False):
        abs_path = os.path.dirname(sys.executable + path)
    else:
        abs_path = os.path.abspath(os.path.dirname(os.path.abspath(__file__)) + path)

    return abs_path
```

<br/>


# 2. 폴더가 없는 경우에 폴더 생성

파일을 생성하려고 할 때, 폴더가 없는 경우에 폴더를 먼저 생성해야 하는 경우가 있다. 

그런 경우에 아래와 같이 폴더가 있는지 확인 후에 없으면 폴더를 생성한다. 

```python
if not os.path.exists(dir_path):
    os.makedirs(dir_path)
```

<br/>


# 3. 폴더에서 특정 확장자의 파일 경로만 가져오기

특정 폴더에서 원하는 확장자의 파일만 가져오고 싶은 경우에 아래와 같은 함수를 만들어 사용한다. 

아래 함수는 이미지에 해당하는 확장자 파일만 가져오는 함수이다. 

```python
def get_image_files(folder_path, extensions=('jpg', 'jpeg', 'png', 'gif', 'bmp')):
    image_files = []
    for file_name in os.listdir(folder_path):
        if file_name.lower().endswith(extensions):
            image_files.append(os.path.join(folder_path, file_name))

    return image_files
```

<br/>


# 4. 파일의 폴더 경로 가져오기 

```python
dir_path = os.path.dirname(file_path)
```

<br/>


# 5. 파일의 이름과 확장자 분리하기 

```python
filename, extension = os.path.splitext(os.path.basename(file_path))
```

<br/>