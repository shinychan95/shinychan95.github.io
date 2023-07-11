---
title: CLion 프로젝트 실행 시 헤더 include 오류 해결 방법
author: chanyoung.kim
date: 2023-07-11 00:00:00 +0900
categories: [ErrorHandling]
tags: []
---

> `#include <stdio.h>` 인식 오류

### 원인 (Xcode 업데이트로 인한 버전 이슈)
```Shell
The toolchain may have been updated or changed. It's strongly advised to reset the CMake cache and reload the project. Reason: The previously configured CMAKE_OSX_ROOT '/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX12.3.sdk' is not available
```

- 친절하게도 Notifications 를 살펴보면, 환경이 변경되었다는 warning 이 존재한다.

<br/>



```Shell
$ ls -al /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs
total 0
drwxr-xr-x  5 root  wheel  160  6 25 00:00 .
drwxr-xr-x  6 root  wheel  192  5 20 10:16 ..
drwxr-xr-x  7 root  wheel  224  3 10 09:58 MacOSX.sdk
lrwxr-xr-x  1 root  wheel   10  6 24 23:59 MacOSX13.3.sdk -> MacOSX.sdk
lrwxr-xr-x  1 root  wheel   10  6 24 23:59 MacOSX13.sdk -> MacOSX.sdk
```

- 결론적으로 버전 이슈로 인해 발생한 문제이다.

<br/>



### 해결 방법
> (Settings → Build, Execution, Deployment → CMake) 내 Cache variables `CMAKE_OSX_SYSROOT` 값의 경로가  ‘/…/MacOSX12.3.sdk’ 경로로 잘못 명시되어 있다.

0. 즉, Cache 제거를 위해서 편리하게 cmake-build-debug 폴더를 모두 지운다.

0. CMake Project 를 Reload 한다.

<br/>



Reload 시 실행되는 명령어,

```Shell
/Applications/CLion.app/Contents/bin/cmake/mac/bin/cmake -DCMAKE_BUILD_TYPE=Debug -G "CodeBlocks - Unix Makefiles" -S /Users/user/oss/c-lang-tutorial/tutorial -B /Users/user/oss/c-lang-tutorial/tutorial/cmake-build-debug
```

- CLion의 CMake 바이너리를 사용하여 Debug 모드의 Unix Makefile을 생성하고, 소스 코드 디렉토리는 `**/Users/user/oss/c-lang-tutorial/tutorial**`로, 빌드 디렉토리는 `**/Users/user/oss/c-lang-tutorial/tutorial/cmake-build-debug**`로 설정하라는 것을 의미한다.

<br/>



Reload 를 통해, stdio.h 를 정상적으로 가져올 수 있다.

```Shell
$ pwd
/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX13.3.sdk/usr/include

$ ls -al | grep stdio.h
-rw-r--r--    7 root  wheel    6201  3  5 08:11 _stdio.h
-rw-r--r--    7 root  wheel   16699  3 10 13:51 stdio.h
```

<br/>



### C 컴파일러(cc) 사용과 관련하여
> C 컴파일러에 대한 명세는 (Settings → Build, Execution, Deployment → Toolchains) 내 존재

<br/>



[https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-macos.html#debugger](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-macos.html#debugger)

<br/>



공식 문서를 참고했을 때에도 `xcode-select` 를 통해서 command line developer tools 를 다운로드 하도록 안내한다. (

<br/>



**이후 CMake 에 의해 시스템에 설치된 Build Tool 및 컴파일러가 자동으로 인식된다.**

```Shell
$ ls -al /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/cc
lrwxr-xr-x  1 root  wheel  5  6 24 23:59 /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/cc -> clang
```

- 컴파일러로써 clang 이 인식된다.

