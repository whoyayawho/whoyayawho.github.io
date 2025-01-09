---
title: "[Python] .py 파일을 .pyd 파일로 변환(setup.py 이용)"

sidebar:
  nav: "dev"
---

<br/>

# 1. 개요

파이썬을 사용하다 보면, 파이썬 파일을 바이너리 파일(`.pyd`)로 변환해서 사용해야 할 때가 있다.

`.pyd` 파일로 만들어 사용하면 실행 속도가 빨라질 수 있고, 코드 내용을 바로 확인할 수 없다는 장점이 있다.

<br/>

# 2. 필요 라이브러리 설치

```bash
pip install cython
pip install setuptools
```

<br/>

# 3. `setup.py` 생성

`.pyd` 파일로 변환하고자 하는 파이썬 파일이 있는 디렉토리에 `setup.py` 파일을 생성한다.

```python
"""Setup script for building Cython extensions.

This module handles the compilation of Python files into Cython extensions.
It configures the build process to generate .pyd files on Windows systems.

Dependencies:
    os: Module for operating system operations
    sys: Module for system-specific parameters
    setuptools: Module for easily building Python packages
    Cython.Build: Module for building Cython extensions
    Cython.Distutils: Module for Cython-specific distutils commands
    distutils.command.build_ext: Module for building extensions
"""

import os
import sys
from setuptools import setup
from Cython.Build import cythonize
from Cython.Distutils import Extension
from distutils.command.build_ext import build_ext


class CustomBuildExt(build_ext):
    """Custom build extension class for handling .pyd file generation.

    This class extends the build_ext class to customize the extension file naming
    for Windows systems, ensuring proper .pyd file generation.
    """

    def get_ext_filename(self, ext_name):
        """Get the filename for the extension.

        Args:
            ext_name (str): The name of the extension module

        Returns:
            str: The complete filename for the extension with proper suffix

        Raises:
            RuntimeError: If Python version is not 3.x
        """
        if sys.version_info.major == 3:
            ext_suffix = ".pyd"
        else:
            raise RuntimeError("Unsupported Python version")

        return os.path.join(*ext_name.split(".")) + ext_suffix


current_dir = os.path.dirname(os.path.abspath(__file__))
py_files = [f for f in os.listdir(current_dir) if f.endswith(".py") and f != "setup.py"]

ext_modules = [
    Extension(os.path.splitext(py_file)[0], [py_file]) for py_file in py_files
]

setup(
    ext_modules=cythonize(ext_modules, compiler_directives={"language_level": "3"}),
    cmdclass={"build_ext": CustomBuildExt},
)
```

<br/>

# 4. `.pyd` 파일 생성

`setup.py` 파일이 있는 디렉토리에서 아래 명령어를 실행해서 `.pyd` 파일을 생성한다.

```bash
python setup.py build_ext --inplace
```

`setup.py` 파일이 있는 폴더 내의 모든 `.py` 파일이 `.pyd` 파일로 변환된다.

<br/>
