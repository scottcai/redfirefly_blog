---
title: FFmpeg系列之一 编译
date: 2021-02-11T18:30:06+09:00
description: 分别为windows linux android系统编译ffmpeg
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: 漆黑中的萤火虫
authorEmoji: 🤖
tags:
- ffmpeg
- 音视频
categories:
- syntax
series:
- Themes Guide
image: images/ffmpeg/logo.png
---

### 源码下载

下载地址 http://ffmpeg.org/download.html

# Windows系统编译

####  安装MSYS2的编译环境

* 下载地址  https://www.msys2.org/

* 点击可执行程序安装，默认安装

* 打开msys2_shell.cmd，执行

  ```shell
  # 更新数据库和核心包
  pacman -Syu
  # 安装编译工具链
  pacman -S make pkg-config diffutils yasm
  #32位版本
  pacman -S mingw-w64-x86_64-nasm mingw-w64-x86_64-gcc mingw-w64-x86_64-SDL2
  #64位版本
  #pacman -S mingw-w64-i686-nasm mingw-w64-i686-gcc mingw-w64-i686-SDL2
  ```

* 在msys2目录下新建 msys_vs2019.bat, 内容

  ```shell
  set MSYS2_PATH_TYPE=inherit
  call "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars32.bat"
  msys2_shell.cmd -mingw64
  ```

* 将C:\msys2\usr\bin\link.exe改一下名，因为会和vc的link.exe重名

* 将ffmpeg源码放到home目录下

#### 编译命令:

```shell
 ./configure --disable-asm --enable-avdevice --enable-doc --disable-programs --enable-avresample  --enable-shared --enable-static --disable-bzlib  --enable-gray --disable-libopenjpeg --disable-iconv --disable-zlib --prefix=./vs2019_build --toolchain=msvc --arch=x86  --enable-debug
 
make -j8

make install
```



##### 编译配置选项详解(待补充)：

* --enable-shared/--disable-shared 表示是否要编译动态库
* --enable-static/--disable-static 表示是否要编译静态库
* --prefix  表示要安装的目录



#### 调试

* 编译完后的相关文件会安装到 vs2019_build下

* 将编译过程中产生的pdb文件拷贝到bin下

  ![](/images/ffmpeg/20210215/compile_out.png)

* 将生成的dll拷贝的vs工程的Debug目录下

* 配置include目录

  ![](/images/ffmpeg/20210215/include_config.jpg)

* 配置链接库目录

  ![](/images/ffmpeg/20210215/lib_config.jpg)

* 在vs代码中打断点即可进行调试







> 本文参考： https://blog.csdn.net/Tui_GuiGe/article/details/90320224





# Linux系统编译



未完待续...





# Android系统编译

未完待续...