---
title: 개발자를 위한 MacOS App 한번 만들어보죠
author: chanyoung.kim
date: 2025-06-22 00:00:00 +0900
categories: [Project]
tags: [tool]
---

- [**기(起)**](#기起)
  - [다들 안녕한 한주 보내셨나요?](#다들-안녕한-한주-보내셨나요)
  - [Strava \| Running, Cycling & Hiking App](#strava--running-cycling--hiking-app)
    - [Strava 내 기능들](#strava-내-기능들)
  - [해방합시다 탈출합시다](#해방합시다-탈출합시다)
- [**승(承)**](#승承)
  - [탈출 시나리오 0 - MacOS Application](#탈출-시나리오-0--macos-application)
  - [탈출 시나리오 1 - 네트워크](#탈출-시나리오-1--네트워크)
    - [대중적인 네트워크 인터페이스로부터 패킷을 가져온다. ](#대중적인-네트워크-인터페이스로부터-패킷을-가져온다-)
    - [VPN](#vpn)
  - [탈출 시나리오 2 - 사용자 I/O](#탈출-시나리오-2--사용자-io)
- [**전(轉)**](#전轉)
  - [SwiftUI](#swiftui)
  - [felizeter : Hello, World!](#felizeter--hello-world)
  - [felizeter : System Menu Bar App](#felizeter--system-menu-bar-app)
  - [felizeter : User IO Monitoring](#felizeter--user-io-monitoring)
  - [felizeter : Github Event Monitoring](#felizeter--github-event-monitoring)
- [**결(結)**](#결結)

---


<h1 id="기起">**기(起)**</h1>
> **‘일어날 기(起)’**, 시상을 일으키고 문제를 제기한다.


<h2 id="다들-안녕한-한주-보내셨나요">다들 안녕한 한주 보내셨나요?</h2>
![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/2893354b-4f3b-4a9a-921a-04663296b821.png)
> “월요일부터 금요일까지 모두 정말로 고생하셨습니다🙂 즐거운 주말되세요🙋🏻‍♂️”<br/><br/>_(주말을 앞두고 팀 메신저 내 훈훈한 대화가 오고 간다)_

<br/>



**과연 내가 즐겁고~ 뿌듯하고~ 보람차고~ 행복하고~ 열정적으로~ 개발을 했을까?**

→ _‘어찌저찌 바쁘게 일했고 지쳤는데… 뭐랄까… 행복했고 앞으로 더 기대되고 희망찬 느낌은 아니네…!’_

<br/>



✅ **그리고 질문에 답하기 위해서는 지난 시간을 되돌아 봐야한다.**

![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/4bed94f1-9246-4e7e-a4cb-02301b731625.png)
<br/>



하루하루 그저 열심히 살면 되긴 하지만, 그렇게 했을 때 **꾸준하게** 행복하게 할 수 있을까?

<br/>



⭐️ **꾸준히 그리고 앞으로 더 열정적으로 기대가 되는 개발을 할 순 없을까?**

<br/>




<h2 id="strava--running-cycling--hiking-app">Strava | Running, Cycling & Hiking App</h2>
![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/edd101ac-c98f-4cf0-8770-b69a78c61ce4.png)
![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/34314327-0588-41d3-81f6-7a5836f31555.png)
![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/44a79ffa-91b4-4467-b218-afccdccc4756.png)
<br/>



<br/>



![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/0bf32c51-6acb-41c7-82d5-9c85d3806fcc.png)

<h3 id="strava-내-기능들">Strava 내 기능들</h3>
- **활동의 모든 측면을 추적 및 분석합니다.**

- 성과를 측정합니다.

- 친구와 연결하여 흥미진진한 경험을 공유하세요.

- 수십만 개의 클럽이 있고 계속 늘어나고 있습니다.

- Beacon을 사용하여 비상 시 실시간으로 위치를 공유할 수 있습니다.

- 멋진 경험을 혼자만 즐기지 말고 널리 알리세요.

- 새로운 경로를 탐색하고 글로벌 커뮤니티와 경쟁하세요.

<br/>



✅ **개발도 이렇게 하면 정말 즐겁지 않을까요?**

<br/>



🚨 **하루종일 어쩌면 가장 많이 나와 가장 대화하는 컴퓨터**

<br/>



🔍 **가장 기초가 되는 활동의 모든 측면을 추적 및 분석할 수 없을까?**

<br/>



<br/>




<h2 id="해방합시다-탈출합시다">해방합시다 탈출합시다</h2>
![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/a89af6dc-fdd3-4c53-94fc-bf4166a42d08.png)
> 두번째 세미나 발표를 앞두고, 어떤 발표가 재미있을까<br/><br/>**이창형이 발표한 그냥 재미있는 해킹<br/>뭔가 우리팀에 적용할 수도 있을 만한 LLVM**

<br/>



<br/>



✅ **재미있는 발표 어떤 것일까. 내 안의 변화 / 탈출이 아닐까?**

<br/>



<br/>



🚨 **그래. 탈출해보자. 벗어나보자.**

<br/>



<br/>




---


<h1 id="승承">**승(承)**</h1>
> **‘이을 승(承)’**, 기를 이어받아 이야기를 진행한다.

<br/>




<h2 id="탈출-시나리오-0--macos-application">탈출 시나리오 0 - MacOS Application</h2>
![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/3cf7dd56-b062-469a-97a5-3707e4baf994.png)
예전부터 유용한 데스크톱 어플리케이션 혹은 모바일 위젯 기반 앱들을 사용하면서 너무 고마웠다.

- 네이버 캘린더 기념일

- 할 일 목록

- Spectacle

- Fan Control

- Fig

- …

<br/>



**기능이 심플하면서 효과적이었고, 필수적인 기능들이라고 느껴졌다.**

<br/>



✅ **그래서 언젠가 꼭 만들고 싶었다…!**

<br/>



⭐️ **MacOS Menu Bar Application 을 만들어보자 (편리하기에 사람들이 쓰지 않을까?)**

<br/>




<h2 id="탈출-시나리오-1--네트워크">탈출 시나리오 1 - 네트워크</h2>
> 우리가 다루는 영역은 극히 Application

![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/c7f6d3b8-5d0a-40f5-95b8-7bc62e58c582.png)
<br/>



<br/>



✅ **호스트 내 네트워크 트래픽을 가져와보자**

<br/>



<br/>



🔍 **과연 어떻게 가져와야 할까요? (내가 만드는 건 어찌 되었건 응용 프로그램의 형태일텐데)**

<br/>




<h3 id="대중적인-네트워크-인터페이스로부터-패킷을-가져온다-">대중적인 네트워크 인터페이스로부터 패킷을 가져온다. </h3>
> 패킷 스니핑 과정은 수집, 변환, 분석이라는 세 가지 단계로 나누어집니다.

1. 수집

   - 첫 번째 단계로 패킷 스니퍼는 회선에서 원본 바이너리데이터를 수집한다. 일반적으로 패킷을 수집하기 위해 선택된 네트워크 인터페이스를 무차별 모드로 변경한다. 이 모드에서 네트워크 카드는 특정 네트워크를 주소 지정하는 트래픽뿐만 아니라 특정 네트워크 영역 내의 모든 네트워크 트래픽을 엿볼 수 있다.

2. 변환

   - 변환 단계에서는 수집된 바이너리 데이터를 읽을 수 있는 형태로 변환시킨다. 대부분이 커맨드라인으로 작동하는 패킷 스니퍼 프로그램은 변환 단계까지만 수행한다. 패킷 스니퍼 프로그램은 네트워크 데이터의 상세한 분석을 최종 사용자에게 맡기고 기본적인 수준으로만 데이터를 변환해 사용자에게 보여준다.

3. 분석

   - 마지막 분석 단계는 수집된 데이터와 변환된 데이터에 대한 실제적인 분석이 이뤄지는 단계다. 패킷 스니퍼는 스니퍼 프로그램 내부에 존재하는 정보를 이용해 수집된 네트워크 데이터의 프로토콜을 검증하고, 프로토콜의 특징과 내용을 분석한다.

<br/>




<h3 id="vpn">VPN</h3>
> 🔗 [Routing your VPN network traffic | Apple Developer Documentation](https://developer.apple.com/documentation/networkextension/routing_your_vpn_network_traffic)
![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/7328b6e0-5da0-416c-b930-02dfb52a8b0a.png)
<br/>



<br/>



🚨 **야 이거… VPN 을 만들어야 하나… 이거 할 수 있을까?…**

<br/>




<h2 id="탈출-시나리오-2--사용자-io">탈출 시나리오 2 - 사용자 I/O</h2>
```Elixir
MacOS 머신에서 키보드 입력과 같이 사용자의 IO가 입력되고 처리되는 과정은 꽤 복잡합니다. 이 과정은 기본적으로 다음과 같은 단계를 거치게 됩니다.

1. 물리적 입력: 사용자가 키보드 키를 누르면 해당 키의 전기 신호가 키보드 하드웨어를 통해 컴퓨터에 전달됩니다.

2. 디바이스 드라이버: 키보드로부터 전달받은 신호는 키보드 디바이스 드라이버에 의해 해석됩니다. 이 드라이버는 하드웨어 신호를 운영 체제가 이해할 수 있는 데이터 형식으로 변환합니다.

3. 운영 체제 처리: 변환된 데이터는 운영 체제의 인풋 관리 시스템에 의해 처리됩니다. MacOS에서는 이 시스템을 통해 키 입력이 알맞는 응용 프로그램으로 라우팅됩니다.

4. 응용 프로그램 처리: 운영 체제는 활성화된 애플리케이션에 키 입력을 전달하고, 애플리케이션은 이를 처리하여 원하는 동작을 수행합니다. 예를 들어, 텍스트 편집기에서는 키보드 입력을 화면에 보이는 문자로 변환합니다.

이런 과정을 거쳐 사용자의 키 입력이 처리됩니다.
```

<br/>



<br/>



🚨 **운영 체제에게 “모든 키 입력을 저에게 주세요.” 라고 말하면 친절하게 주려나?…**

<br/>



<br/>




---


<h1 id="전轉">**전(轉)**</h1>
> **‘구를 전(轉)’**, 장면과 시상을 새롭게 전환시키고, 결정적으로 방향을 한 번 전환하는 것을 말한다.

<br/>




<h2 id="swiftui">SwiftUI</h2>
> **만드는 입장에서 필요한 건 도구들**

![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/638f3052-0ae7-4fcf-bede-50a405d97491.png)
<br/>



SwiftUI는 Apple의 모든 플랫폼에서 작동하는 코드를 작성할 수 있도록 해줍니다. 

<br/>



그러나, 각 플랫폼의 특정 기능에 맞추어 앱을 조정해야 하는 경우도 있는데, 이 또한 할 수 있다.

<br/>



예를 들어, UIKit, AppKit 또는 WatchKit app의 delegate에 대해 시스템이 통상적으로 하는 콜백에 반응해야 한다면, delegate 객체를 정의하고 적절한 delegate adaptor property wrapper를 사용하여 앱 구조에 인스턴스화 할 수 있다.

<br/>



**Delegate**란?

- **Delegate**는 대리인 또는 대표자를 의미하며, 이 클래스는 애플리케이션의 전반적인 동작과 생명 주기를 관리합니다.

- **Delegate**는 애플리케이션의 상태 변화에 대응하는 메서드를 제공하며, 애플리케이션이 다양한 동작을 실행할 때 시스템으로부터 알림을 받는 역할을 합니다.

   - `**application(_:didFinishLaunchingWithOptions:)**`

      - 애플리케이션의 시작이 완료되었을 때 호출됩니다. 애플리케이션이 시작되자마자 필요한 설정이나 초기화 작업을 여기서 수행합니다.

   - `**applicationDidBecomeActive(_:)**`

      - 애플리케이션이 액티브 상태가 되었을 때 호출됩니다. 애플리케이션이 전경으로 들어오거나 사용자와 상호작용하기 전에 호출됩니다.

   - `**applicationWillResignActive(_:)**`

      - 애플리케이션이 비활성 상태가 될 때 호출됩니다. 애플리케이션이 전경에서 사라지거나, 전화나 메시지와 같은 인터럽트에 대응해야 할 때 호출됩니다.

   - `**applicationDidEnterBackground(_:)**`

      - 애플리케이션이 백그라운드 상태로 전환될 때 호출됩니다. 이 메서드에서는 상태를 저장하거나 백그라운드 작업을 수행합니다.

   - `**applicationWillEnterForeground(_:)**`

      - 애플리케이션이 전경 상태로 전환되기 직전에 호출됩니다. 이 메서드에서는 백그라운드에서 수행한 작업을 정리하거나 사용자 인터페이스를 업데이트합니다.

   - `**applicationWillTerminate(_:)**`

      - 애플리케이션이 종료되기 직전에 호출됩니다. 이 메서드에서는 데이터를 저장하거나 애플리케이션의 상태를 정리합니다.

<br/>




<h2 id="felizeter--hello-world">felizeter : Hello, World!</h2>
feliz + (power) meter 

_죄송하지만, 코드로 봅시다._

<br/>




<h2 id="felizeter--system-menu-bar-app">felizeter : System Menu Bar App</h2>
<br/>



_죄송하지만, 코드로 봅시다._


<h2 id="felizeter--user-io-monitoring">felizeter : User IO Monitoring</h2>
<br/>



_죄송하지만, 코드로 봅시다._

<br/>




<h2 id="felizeter--github-event-monitoring">felizeter : Github Event Monitoring</h2>
<br/>



_죄송하지만, 코드로 봅시다._

<br/>



<br/>



<br/>




---


<h1 id="결結">**결(結)**</h1>
> **‘맺을 결(結)’**, 전체를 묶어 여운과 여정이 깃들도록 거두어 끝맺는다.

![](/assets/pages/4cdf849b-ae03-4dce-9b4b-44112cf59d62/b6194746-36b7-43af-b08a-172cabf181c6.png)
<br/>



<br/>



<br/>



<br/>




---

<br/>



<br/>



