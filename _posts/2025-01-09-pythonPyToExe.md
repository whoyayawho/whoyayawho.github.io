---
title: "[Python] .py 파일을 .exe 파일로 변환(pyinstaller)"

sidebar:
  nav: "dev"
---

<br/>

# 1. 개요

파이썬을 사용하다 보면, 파이썬 파일을 실행 파일(`.exe`)로 변환해서 사용해야 할 때가 있다.

`.exe` 파일로 만들어 사용하면 파이썬이 없는 컴퓨터에서도 실행이 가능하다는 장점이 있다.

<br/>

# 2. 필요 라이브러리 설치

```bash
pip install setuptools cython pyinstaller
```

<br/>

# 3. 단일 `.py` 파일을 `.exe` 파일로 변환

하나의 `file_to_make_exe.py` 파일을 `file_to_make_exe.exe` 파일로 만들기 위해서는 아래 명령어를 실행한다.

```bash
pyinstaller -F -i "NONE" --add-data "{추가파일};." file_to_make_exe.py
```

`-F` 옵션이 없으면 폴더 하나에 `.exe` 파일과 다른 필요한 파일들이 생성된다.

따라서 프로그램을 실행하기 위해서는 `.exe` 파일 외에 폴더 내에 같이 생성되는 다른 파일들도 필요하다.

모든 파일을 하나의 파일로 만들기 위해서는 `-F` 옵션을 넣어준다.

그러면 하나의 `.exe` 파일만 생성된다.

`-i` 옵션은 아이콘을 추가해주는데 "NONE"은 아이콘을 추가하지 않는다는 뜻이다.

`--add-data` 옵션은 추가적으로 넣어줄 파일을 지정해준다.

<br/>

# 4. 여러 개의 `.py` 파일을 사용하는 프로그램을 `.exe` 파일로 변환

## (1) 파일 트리 구성

먼저, 아래 파일 트리와 같이 구성한다.

```
python_program
│  .gitignore
│  make.py
│  file_to_make_exe.py
│
└─lib
        setup.py
        file_to_make_pyd1.py
        file_to_make_pyd2.py
        file_to_make_pyd3.py
```

`.exe` 파일로 만들 `.py` 파일을 make.py 파일과 동일한 폴더에 둔다.

그리고 `.exe`로 만들 파일을 제외한 다른 `.py` 파일들은 lib 폴더에 넣는다.

lib 폴더에 넣어둔 `.py` 파일들은 각각 `.pyd` 파일로 변환해서 `.exe` 파일에 포함하고자 한다.

## (2) `make.py` 파일 작성

```python
"""Build script for generating executable and PYD files.

This module handles the build process for generating executable and PYD files from Python source.
It provides functionality for cleaning up build artifacts, copying PYD files, and generating
the final executable.

Functions:
    run_cmd: Execute a shell command in a specified directory
    remove_file: Remove files matching a given pattern
    remove_directory: Remove a directory and its contents
    cleanup_build_files: Clean up build artifacts
    copy_pyd_files: Copy generated PYD files to target location
    main: Main build process orchestration
"""

import os
import glob
import shutil
import subprocess
from pathlib import Path
from typing import Union


def run_cmd(cmd: str, cwd_dir: Union[str, Path]) -> None:
    """Execute a shell command in the specified directory.

    Args:
        cmd (str): The command to execute
        cwd_dir (Union[str, Path]): Working directory for command execution

    Prints:
        Command output or error message if execution fails
    """
    try:
        result = subprocess.run(
            cmd,
            shell=True,
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True,
            cwd=str(cwd_dir),
            check=True,
        )
        print(result.stdout)
    except subprocess.CalledProcessError as e:
        print(f"Command execution failed: {e.stderr}")


def remove_file(pattern: str) -> None:
    """Remove files matching the specified pattern.

    Args:
        pattern (str): Glob pattern for files to remove

    Prints:
        Success or failure message for each file deletion
    """
    for file_path in glob.glob(pattern):
        try:
            os.remove(file_path)
            print(f"File deleted: {file_path}")
        except OSError as e:
            print(f"Failed to delete file: {file_path} - {e}")


def remove_directory(dir_path: Union[str, Path]) -> None:
    """Remove a directory and all its contents.

    Args:
        dir_path (Union[str, Path]): Path to the directory to remove

    Prints:
        Success or failure message for directory deletion
    """
    path = Path(dir_path)
    if path.exists() and path.is_dir():
        try:
            shutil.rmtree(path)
            print(f"Directory deleted: {path}")
        except OSError as e:
            print(f"Failed to delete directory: {path} - {e}")


def cleanup_build_files() -> None:
    """Clean up build artifacts and temporary files.

    Removes PYD files, spec files, C source files, and build directories.
    """
    patterns = ["*.pyd", "*.spec", "./lib/*.spec", "./lib/*.c", "./lib/*.pyd"]
    directories = ["build", "./lib/build"]

    for pattern in patterns:
        remove_file(pattern)
    for directory in directories:
        remove_directory(directory)


def copy_pyd_files() -> None:
    """Copy generated PYD files from lib directory to current directory.

    Prints:
        Success or failure message for each file copy operation
    """
    for pyd_file in glob.glob("./lib/*.pyd"):
        try:
            dest = Path(".") / Path(pyd_file).name
            shutil.copy(pyd_file, dest)
            print(f"PYD file copied: {dest}")
        except shutil.Error as e:
            print(f"Failed to copy PYD file: {pyd_file} - {e}")


def main():
    """Main build process orchestration.

    Executes the complete build process:
    1. Cleans up existing build artifacts
    2. Generates PYD files
    3. Creates executable file
    4. Performs final cleanup
    """
    print("Build process started")

    remove_file("*.exe")
    cleanup_build_files()
    remove_directory("dist")

    if os.path.exists("./lib"):
        print("Generating .pyd files...")
        try:
            run_cmd("python ./setup.py build_ext --inplace", "./lib")
            copy_pyd_files()
        except (subprocess.CalledProcessError, shutil.Error, OSError) as e:
            print(f"Failed to generate PYD files: {e}")
            return
    else:
        print("Skipping .pyd generation - lib directory not found")

    print("Generating EXE file...")
    for py_file in glob.glob("*.py"):
        if py_file != "make.py":
            run_cmd(f'pyinstaller -i "NONE" {py_file}', ".")

    cleanup_build_files()
    print("Build process completed")


if __name__ == "__main__":
    main()
```

## (3) `setup.py` 파일 작성

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

## (4) `.gitignore` 파일 작성

```
_venv_
*.exe
*.spec
*.pyd
*.c
*.pyc
*.pyo
```

<br/>

# 5. 실행

아래 명령어를 실행하면 dist 폴더에 `.exe` 파일이 생성된다.

```bash
python make.py
```

<br/>
