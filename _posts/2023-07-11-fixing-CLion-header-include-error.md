---
title: CLion 프로젝트 실행 시 헤더 include 오류 해결 방법
author: chanyoung.kim
date: 2023-07-11 00:00:00 +0900
categories: [ErrorHandling]
tags: []
---

간만에 CLion 으로 코드 테스트 및 확인할 부분이 생겨, 지난 프로젝트를 열었다. 하지만, 기본 헤더 파일들(stdio.h)을 가져오지 못하는 이슈가 존재했다. 이를 해결하는 과정에 대해서 설명한다.

<br/>




---

<br/>




<h3 id="원인-(Xcode-업데이트로-인한-버전-이슈)">원인 (Xcode 업데이트로 인한 버전 이슈)</h3>
> The toolchain may have been updated or changed. It's strongly advised to reset the CMake cache and reload the project. Reason: The previously configured CMAKE_OSX_ROOT '/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX12.3.sdk' is not available

- 친절하게도 CLion 내 Notifications 를 살펴보면, `CMAKE_OSX_ROOT` 경로가 올바르지 못한 것을 확인할 수 있다.

- CMake는 크로스 플랫폼의 오픈소스 빌드 시스템으로, 이를 통해 프로젝트를 빌드, 테스트 및 패키징한다. `CMAKE_OSX_ROOT` 설정은 MacOS 운영 체제를 대상으로하는 프로젝트를 빌드하는 데 필요한 루트 디렉토리를 나타낸다. 이 경로가 잘못되면 CMake는 프로젝트를 빌드하는 데 필요한 도구와 라이브러리를 찾지 못하게 된다.

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

- Warning 내 SDK 경로를 살펴보니, 버전이 업그레이드 된 것을 확인할 수 있다.

   - 기억을 떠올려보니, 최근 Xcode 업데이트를 진행하면서 버전이 변경됐던 것이다.

- **결론적으로 버전 이슈로 인해 발생한 문제이다.**

<br/>




<h3 id="해결-방법">해결 방법</h3>
(Settings → Build, Execution, Deployment → CMake) 내 **Cache variables** `CMAKE_OSX_SYSROOT` 경로가 잘못 명시되어 있으므로, 이 부분을 고쳐주면 된다.

1. Cache 제거를 위해서 편리하게 cmake-build-debug 폴더를 모두 지운다.

2. CMake Project 를 Reload 한다.

<br/>



`+a`

CMake cache는 CMake가 프로젝트를 빌드하는 데 사용하는 변수들의 집합이다. 이러한 변수들은 빌드 시스템의 설정, 사용된 컴파일러의 세부 정보, 빌드 옵션 등을 포함한다. 때로는 이 cache가 오래되거나 잘못된 정보를 포함하게 되어 빌드 문제를 일으킬 수 있다. 이 경우, cache를 지우는 것은 문제 해결의 첫걸음이 될 수 있다.

<br/>



**Reload 시 실행되는 명령어,**

```Shell
/Applications/CLion.app/Contents/bin/cmake/mac/bin/cmake -DCMAKE_BUILD_TYPE=Debug -G "CodeBlocks - Unix Makefiles" -S /Users/user/oss/c-lang-tutorial/tutorial -B /Users/user/oss/c-lang-tutorial/tutorial/cmake-build-debug
```

- CLion의 CMake 바이너리를 사용하여 Debug 모드의 Unix Makefile을 생성하고, 소스 코드 디렉토리는 `**/Users/user/oss/c-lang-tutorial/tutorial**`로, 빌드 디렉토리는 `**/Users/user/oss/c-lang-tutorial/tutorial/cmake-build-debug**`로 설정하라는 것을 의미한다.

<br/>



**Reload 를 통해, stdio.h 를 정상적으로 가져올 수 있다.**

```Shell
$ pwd
/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX13.3.sdk/usr/include

$ ls -al | grep stdio.h
-rw-r--r--    7 root  wheel    6201  3  5 08:11 _stdio.h
-rw-r--r--    7 root  wheel   16699  3 10 13:51 stdio.h
```

<br/>




<h3 id="C-컴파일러(cc)-사용과-관련하여">C 컴파일러(cc) 사용과 관련하여</h3>
> C 컴파일러에 대한 명세는 (Settings → Build, Execution, Deployment → Toolchains) 내 존재한다.

<br/>



[https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-macos.html#debugger](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-macos.html#debugger)

<br/>



공식 문서를 참고했을 때에도 `xcode-select` 를 통해서 command line developer tools 를 다운로드 하도록 안내하고 있다.

<br/>



**이후 CMake 에 의해 시스템에 설치된 Build Tool 및 컴파일러가 자동으로 인식된다.**

```Shell
$ ls -al /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/cc
lrwxr-xr-x  1 root  wheel  5  6 24 23:59 /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/cc -> clang
```

- 컴파일러로써 cc → clang 이 인식된다.

- cc는 일반적으로 Unix 시스템에서 C 컴파일러를 가리키는 전통적인 이름이다. 오늘날 대부분의 시스템에서 cc는 Clang이나 GCC와 같은 실제 컴파일러를 가리키는 심볼릭 링크이다.

<br/>



