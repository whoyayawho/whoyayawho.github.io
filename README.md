# whoyayawho.github.io

## Install requirements

```bash
$ sudo apt install ruby ruby-dev build-essential
$ echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
$ echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc
$ source ~/.bashrc
$ gem install jekyll bundler
```

## Install dependencies

```bash
$ cd whoyayawho.github.io
$ bundle
$ bundle add webrick
```

## Test

```bash
$ bundle exec jekyll serve
```
