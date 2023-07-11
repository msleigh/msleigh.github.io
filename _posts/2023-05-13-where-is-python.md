---
layout: post
title:  "Where is Python on macOS?"
description: "Finding out where Python lives on macOS systems (using Homebrew)"
date: 2023-05-14
author: msleigh
categories: python macos homebrew
---

This post provides a guide for installing and managing Python on macOS, covering system and Homebrew installations.

## System Python

MacOS hasn't come with a system Python installed since Monterey 12.3, when the
Python 2 installation was removed
([release notes](https://developer.apple.com/documentation/macos-release-notes/macos-12_3-release-notes/#Python)).
A Python 3 executable is included, but this is a shim that runs the [XCode Command Line
Tools](https://developer.apple.com/library/archive/technotes/tn2339/_index.html#//apple_ref/doc/uid/DTS40014588-CH1-WHAT_IS_THE_COMMAND_LINE_TOOLS_PACKAGE_) version of Python 3, and requires the XCode Command Line Tools to be installed
first.

(The Command Line Tools package is a small self-contained package, separate from XCode, to support command line development in macOS. It consists of the macOS SDK, and command-line tools such as Clang, Python, GCC, Git, etc., which are installed in the `/Library/Developer/CommandLineTools` directory. MacOS 10.9 and later include shims, or wrapper executables, installed in `/usr/bin`, which map tools included in `/usr/bin` to the corresponding one inside XCode.)

Running `python3` (or other developer tools such as `git`, `gcc`, `clang`, ...) prompts
the installation of XCode CLT, or it can be triggered manually with:

```bash
xcode-select --install
```

after which there are working Python 3 and Pip 3 executables:

```bash
$ ls -l /usr/bin/python*
-rwxr-xr-x 76 root wheel 167120 Apr  4 08:24 /usr/bin/python3

$ /usr/bin/python3 --version
Python 3.9.6
```

```bash
$ ls -l /usr/bin/pip*
-rwxr-xr-x 76 root wheel 167120 Apr  4 08:24 /usr/bin/pip3

$ /usr/bin/pip3 --version
pip 21.2.4 from /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/...
```

Note that the full XCode application is not required.

To see what else is installed in the XCode CLT:

```bash
ls -l /Library/Developer/CommandLineTools/usr/bin/
```

## Homebrew Python

It's most likely however you'll want to install Python, and manage multiple
Python installations, with [Homebrew](https://docs.brew.sh). (Note that the installation
of XCode Command Line Tools as described above is required to use Homebrew, although it
will be triggered automatically by the Homebrew installation.)

Homebrew installs software in `/usr/local/` on Intel Macs and in `/opt/homebrew` for
Apple M1 Macs; you can find out where on your system by running:

```bash
brew --prefix
```

Homebrew installs Python in `$(brew --prefix)/bin/`:

```bash
$ ls -l $(brew --prefix)/bin/python*[0-9]
lrwxr-xr-x 1 msleigh admin 40 May 13 13:42 /usr/local/bin/python3 -> ../Cellar/python@3.11/3.11.3/bin/python3
lrwxr-xr-x 1 msleigh admin 44 May 13 13:50 /usr/local/bin/python3.10 -> ../Cellar/python@3.10/3.10.11/bin/python3.10
lrwxr-xr-x 1 msleigh admin 43 May 13 13:42 /usr/local/bin/python3.11 -> ../Cellar/python@3.11/3.11.3/bin/python3.11
lrwxr-xr-x 1 msleigh admin 41 Jan 26 17:52 /usr/local/bin/python3.9 -> ../Cellar/python@3.9/3.9.16/bin/python3.9

$ l $(brew --prefix)/bin/pip*
lrwxr-xr-x 1 msleigh admin 37 May 13 13:43 /usr/local/bin/pip3 -> ../Cellar/python@3.11/3.11.3/bin/pip3
lrwxr-xr-x 1 msleigh admin 41 May 13 13:50 /usr/local/bin/pip3.10 -> ../Cellar/python@3.10/3.10.11/bin/pip3.10
lrwxr-xr-x 1 msleigh admin 40 May 13 13:43 /usr/local/bin/pip3.11 -> ../Cellar/python@3.11/3.11.3/bin/pip3.11
lrwxr-xr-x 1 msleigh admin 38 Jan 26 17:52 /usr/local/bin/pip3.9 -> ../Cellar/python@3.9/3.9.16/bin/pip3.9
```

Installing via:

```bash
brew install python
```

installs the latest version of Python (3.11 at the time of writing), or you can install
a version explicitly, e.g.:

```bash
brew install python@3.9
```

Each installed version has its own `site-packages` folder for Python packages installed
by `pip`:

```bash
¢ ls -ld $(brew --prefix)/lib/python*/site-packages
drwxr-xr-x 16 msleigh staff  512 May 14 00:22 /usr/local/lib/python3.10/site-packages
drwxr-xr-x 19 msleigh staff  608 May 13 13:52 /usr/local/lib/python3.11/site-packages
drwxr-xr-x 67 msleigh staff 2144 Jan 26 17:52 /usr/local/lib/python3.9/site-packages
```

Removing an old version of Python _doesn't_ remove the associated `site-packages`
directory:

```bash
$ brew uninstall python@3.8
Uninstalling /usr/local/Cellar/python@3.8/3.8.16... (5,041 files, 80MB)

$ ls -l /usr/local/lib/python3.8/site-packages/
total 12
drwxr-xr-x  3 msleigh staff   96 May 14 20:07 __pycache__
drwxr-xr-x  5 msleigh staff  160 May 14 20:07 _distutils_hack
-rw-r--r--  1 msleigh staff  151 May 14 20:07 distutils-precedence.pth
-rw-r--r--  1 msleigh staff  126 Dec 21  2020 easy_install.py
drwxr-xr-x  9 msleigh staff  288 May 14 20:07 pip
drwxr-xr-x  8 msleigh staff  256 May 14 20:07 pip-22.3.1-py3.8.egg-info
drwxr-xr-x  8 msleigh staff  256 May 14 20:07 pkg_resources
drwxr-xr-x 48 msleigh staff 1536 May 14 20:07 setuptools
drwxr-xr-x  8 msleigh staff  256 May 14 20:07 setuptools-65.6.3-py3.8.egg-info
-rw-r--r--  1 msleigh staff 2157 May 14 20:07 sitecustomize.py
drwxr-xr-x 16 msleigh staff  512 May 14 20:07 wheel
drwxr-xr-x  9 msleigh staff  288 Sep 30  2020 wheel-0.34.2-py3.8.egg-info
drwxr-xr-x  9 msleigh staff  288 Dec 23  2020 wheel-0.35.1-py3.8.egg-info
drwxr-xr-x  9 msleigh staff  288 Jul  9  2021 wheel-0.36.2-py3.8.egg-info
drwxr-xr-x  9 msleigh staff  288 Nov 19  2021 wheel-0.37.0-py3.8.egg-info
drwxr-xr-x  9 msleigh staff  288 Nov  6  2022 wheel-0.37.1-py3.8.egg-info
drwxr-xr-x  9 msleigh staff  288 May 14 20:07 wheel-0.38.4-py3.8.egg-info
```

but these can be deleted manually.
