---
title: Notion 글, 버튼 하나로 블로그 배포 가능?
author: chanyoung.kim
date: 2023-04-23 00:00:00 +0900
categories: [Project]
tags: [notion, tool, blog]
---

_( 본 글은 네이버 사내 스터디 오프라인 세미나 준비를 하면서 했던 프로젝트 정리입니다 )_

<br/>



결과물 링크 - [https://github.com/shinychan95/make-notion-blog](https://github.com/shinychan95/make-notion-blog)


---

## 주제를 정한 목적

> 🦖 _흥미롭고 유익하고 관심을 끌만한 주제는 무엇이 있을까?_

- Notion 을 사용하고 있는 우리 _(특히 나…)_

- 그리고 필수 소양인 `개발 블로그`

   - Notion 도 블로그로 만들 수 있지만, SEO(검색엔진 최적화) 관점에서 검색이 잘 안된다.

   - 뭐 다들 운영하면서 광고로 돈 벌고 계시잖아요? 🤷🏻‍♂️

      <details>
      <summary>…</summary>
         아니요… 저는 마음만 몇십 번 먹었지만, 꾸준히 하지 못하고 있습니다… 

      </details>

   - **Notion 에 편하게 글 적고 알아서 블로그에 반영이 된다면?**

<br/>



### 얻어갈 수 있는 점
- 개념, 지식, 설명

- 하나의 프로젝트 기반 결과물

- `+a` Honey Tips

<br/>



### **결론적으로 주제는! Notion 글, 버튼 하나로 블로그 배포 가능?**
> **“가능하지 않다”** 라는 결론으로 귀결될 가능성이 크다.<br/><br/>하지만, 오프라인으로 동작하는 Notion 이기에, 로컬 내부 DB 에 접근하여 할 수 있지 않을까?<br/>(데이터 저장 형식은?)

<br/>



하지만, 이를 조사하면서 Notion 서비스가 어떻게 `offline` 에서 사용 가능한지 공부해보고 싶다.

<br/>



**특히, 어떻게 데이터를 저장하고 관리하는지 공부해보고 싶다. (압축을 하는지, 형식은 어떤 방식인지)**

<br/>



_만약 이것이 가능하다면, 꽤나 네이버 내에서 유용한 공유가 되지 않을까 싶다…!_

<br/>




---

## lsof 명령어를 통해 노션 캐시 데이터를 찾을 수 없을까?

참고 자료 : [https://www.lesstif.com/system-admin/lsof-20776078.html](https://www.lesstif.com/system-admin/lsof-20776078.html)

> 🦖 `lsof` 명령어를 활용하여 Notion과 관련되어 열려 있는 파일 목록들을 모두 살펴볼 수 있다.

<br/>



```Shell
user ➜  ~ lsof -c Notion
COMMAND     PID USER   FD      TYPE             DEVICE  SIZE/OFF                NODE NAME
Notion      650 user  cwd       DIR               1,18       640                   2 /
Notion      650 user  txt       REG               1,18    238944            54595517 /Applications/Notion.app/Contents/MacOS/Notion
Notion      650 user  txt       REG               1,18     51456            59745768 /Library/Preferences/Logging/.plist-cache.GaIilKan
Notion      650 user  txt       REG               1,18    147520            54609114 /Applications/Notion.app/Contents/Frameworks/Squirrel.framework/Versions/A/Squirrel
Notion      650 user  txt       REG               1,18    108608            54609124 /Applications/Notion.app/Contents/Frameworks/Mantle.framework/Versions/A/Mantle
...
Notion      794 user  cwd       DIR               1,18       640                   2 /
Notion      794 user  txt       REG               1,18    122784            54609133 /Applications/Notion.app/Contents/Frameworks/Notion Helper (GPU).app/Contents/MacOS/Notion Helper (GPU)
Notion      794 user  txt       REG               1,18    147520            54609114 /Applications/Notion.app/Contents/Frameworks/Squirrel.framework/Versions/A/Squirrel
Notion      794 user  txt       REG               1,18    108608            54609124 /Applications/Notion.app/Contents/Frameworks/Mantle.framework/Versions/A/Mantle
Notion      794 user  txt       REG               1,18    390656            54609095 /Applications/Notion.app/Contents/Frameworks/ReactiveObjC.framework/Versions/A/ReactiveObjC
...
Notion      795 user  cwd       DIR               1,18       640                   2 /
Notion      795 user  txt       REG               1,18    122784            54609102 /Applications/Notion.app/Contents/Frameworks/Notion Helper.app/Contents/MacOS/Notion Helper
Notion      795 user  txt       REG               1,18    147520            54609114 /Applications/Notion.app/Contents/Frameworks/Squirrel.framework/Versions/A/Squirrel
Notion      795 user  txt       REG               1,18    108608            54609124 /Applications/Notion.app/Contents/Frameworks/Mantle.framework/Versions/A/Mantle
Notion      795 user  txt       REG               1,18     28672              617445 /Users/user/Library/Application Support/Notion/Partitions/notion/Cookies
...
Notion      959 user  cwd       DIR               1,18       640                   2 /
Notion      959 user  txt       REG               1,18    122784            54609102 /Applications/Notion.app/Contents/Frameworks/Notion Helper.app/Contents/MacOS/Notion Helper
Notion      959 user  txt       REG               1,18     51456            59745768 /Library/Preferences/Logging/.plist-cache.GaIilKan
Notion      959 user  txt       REG               1,18    147520            54609114 /Applications/Notion.app/Contents/Frameworks/Squirrel.framework/Versions/A/Squirrel
Notion      959 user  txt       REG               1,18    108608            54609124 /Applications/Notion.app/Contents/Frameworks/Mantle.framework/Versions/A/Mantle
...
Notion    62734 user  cwd       DIR               1,18       640                   2 /
Notion    62734 user  txt       REG               1,18    122784            54609142 /Applications/Notion.app/Contents/Frameworks/Notion Helper (Renderer).app/Contents/MacOS/Notion Helper (Renderer)
Notion    62734 user  txt       REG               1,18     51456            59745768 /Library/Preferences/Logging/.plist-cache.GaIilKan
Notion    62734 user  txt       REG               1,18     94156            54608944 /Applications/Notion.app/Contents/Frameworks/Electron Framework.framework/Versions/A/Resources/chrome_100_percent.pak
Notion    62734 user  txt       REG               1,18    147520            54609114 /Applications/Notion.app/Contents/Frameworks/Squirrel.framework/Versions/A/Squirrel
...
Notion    62735 user  cwd       DIR               1,18       640                   2 /
Notion    62735 user  txt       REG               1,18    122784            54609142 /Applications/Notion.app/Contents/Frameworks/Notion Helper (Renderer).app/Contents/MacOS/Notion Helper (Renderer)
Notion    62735 user  txt       REG               1,18     51456            59745768 /Library/Preferences/Logging/.plist-cache.GaIilKan
Notion    62735 user  txt       REG               1,18     94156            54608944 /Applications/Notion.app/Contents/Frameworks/Electron Framework.framework/Versions/A/Resources/chrome_100_percent.pak
Notion    62735 user  txt       REG               1,18    147520            54609114 /Applications/Notion.app/Contents/Frameworks/Squirrel.framework/Versions/A/Squirrel
...
Notion    62736 user  cwd       DIR               1,18       640                   2 /
Notion    62736 user  txt       REG               1,18    122784            54609142 /Applications/Notion.app/Contents/Frameworks/Notion Helper (Renderer).app/Contents/MacOS/Notion Helper (Renderer)
Notion    62736 user  txt       REG               1,18     51456            59745768 /Library/Preferences/Logging/.plist-cache.GaIilKan
Notion    62736 user  txt       REG               1,18     94156            54608944 /Applications/Notion.app/Contents/Frameworks/Electron Framework.framework/Versions/A/Resources/chrome_100_percent.pak
Notion    62736 user  txt       REG               1,18    147520            54609114 /Applications/Notion.app/Contents/Frameworks/Squirrel.framework/Versions/A/Squirrel
Notion    62736 user  txt       REG               1,18    108608            54609124 /Applications/Notion.app/Contents/Frameworks/Mantle.framework/Versions/A/Mantle
...
```

- 각 프로세스 별로 파일이 참 많이도 떠 있구나.

- 이들 중 높은 확률로 메인 프로그램에 해당하는 `650` 프로세스가 연 파일들을 살펴보았다.

- 하지만, 왠만한 파일을 까봐도 역시나 깨져서 보일 뿐이다.

- **결론적으로 찾은 파일 혹은 키워드**

   ```Shell
   Notion      650 user  txt       REG               1,18      8192              617448 /Users/user/Library/Application Support/Notion/Partitions/notion/GPUCache/data_0
   Notion      650 user  txt       REG               1,18     28672              617561 /Users/user/Library/Application Support/Notion/Partitions/notion/databases/Databases.db
   Notion      650 user   75r      REG               1,18   2195268            60037157 /Users/user/Library/Application Support/Notion/Partitions/notion/IndexedDB/notion_www.notion.so_0.indexeddb.leveldb/037217.ldb
   Notion      650 user   79u      REG               1,18     83072            59749851 /Users/user/Library/Saved Application State/notion.id.savedState/data.data
   ```

   <br/>




---

## 인터넷 망령 모드 시작

### Notion 의 offline 모드에 대해 검색
~~[https://notionzen.com/notion-offline/](https://notionzen.com/notion-offline/)~~

- 기존에 offline으로도 Notion 사용을 했었고, 한번 봤던 페이지들은 로딩없이 보이길래, 어딘가에 다 저장하고 있는 줄 알았다.

- web-based application

- offline 상황에서 다시 인터넷이 연결되면 약 20% 가량 데이터를 잃게 된다. ~~(완전 초기 지금은 아니다)~~

<br/>



### Notion 공식 블로그 내 데이터 모델 발견
~~[https://www.notion.so/blog/data-model-behind-notion](https://www.notion.so/blog/data-model-behind-notion)~~

- 노션 내 정보는 어떤 제약이나 가두리가 존재하지 않는다.

- 노션에서 보는 모든 것을 block이다. (텍스트, 이미지, 리스트, 데이터베이스 내 row, 심지어 페이지 자체도)

- like LEGO 🟥🟨⬜️⬛️

- 물론 block들이 정보화되기 위해서는 엔지니어링 팀이 미쳐날 뛸 노릇이지만, atomic 하고 그래프스러운 데이터 모델을을 원했다.

- **아래 자세하게 정리해보자.**

   - ‣ 

<br/>




---

## 인터넷 망령 모드 이어서

### indexdDB 에 코드 레벨로 접근할 수 없을까?
~~[https://web.dev/indexeddb/](https://web.dev/indexeddb/)~~

- ⭐️ **조력자의 등장** ⭐️ → ‣ 

   - 하지만, notion 에서는 SQLite 로 옮긴 상태이다. ([****Notion's page load and navigation times just got faster****](https://www.notion.so/ko-kr/blog/faster-page-load-navigation)****)****

      - SQLite 이전에는 클라이언트 측 저장소로 IndexedDB에 의존. 하지만 저장소 할당량, 여러 버그 및 특히 Windows 기기에서의 성능 문제로 인해 IndexedDB 를 사용하지 않게 되었다.

<br/>



~~[https://www.npmjs.com/package/notion-to-md](https://www.npmjs.com/package/notion-to-md)~~

- Local RecordCache 로부터 데이터를 가져와서 md 로 만드는 것이 아닌, Notion 서버로 요청을 보내서 가져오는 것으로 보인다.

- 하지만, 결론적으로 RecordCache 로부터 데이터를 가져오고 이를 md 로 만드는 것이 실질적으로 어렵다면, 이 방법을 택해보자.

- [x] web-based application 이니 인터넷과 통신하는 과정에서 서버가 존재하고, 혹시 API 기능이 존재하려나?
   - Local 에 따로 API 서버는 존재하지 않고, Notion API 를 통해서, 왠만한 조회 및 연동 기능은 존재한다.

   - [https://developers.notion.com/docs/getting-started](https://developers.notion.com/docs/getting-started)

   - 결론적으로 Notion API 를 위 오픈소스처럼 이용하기는 합니다. **하지만 다릅니다.**

<br/>



⭐️ **조력자의 등장** ⭐️ → ‣ 

<br/>




---

## Notion 데이터 모델 분석

### **Block basics**
![](/assets/pages/1eafdee6-189c-46fe-a0fe-5bff83f07309/188c99c2-d7a1-42f3-922f-76351b5f1ab4.png)
- `ID`

   - 페이지 block의 경우, URL 마지막 부분

   - randomly-generated UUIDs (UUID v4) 

      - ex) 95473e9f-a2ab-4f0c-8115-21810a961f4f

      - _성능 이슈는 없을까? →_ ‣

- `Properties`

   - 가장 중점이 되는 데이터인 **title**

- `Type`

   - header (#, ##, ###), text, code, divider, bulleted_list, numbered_list, toggle, …

   - _제 Notion 데이터 기준 31가지 종류 존재_

- `Content`

   - an array (or ordered set) of block IDs representing the content inside this block

- `Parent`

   - the block ID of the block’s parent

<br/>



### How blocks fit together
- 서로 다른 타입 간 `Turn into` 가능하다.

   - `Type` 과 `Property` 간 커플링이 존재하지 않아서 변환 및 렌더링에 문제없다.

   - ex) ‘to_do’ → ‘text’,  

      - property 내 checked 데이터는 변함이 없다.

- `Content` 로 인해 render tree 를 이룰 수 있다.

- 권한 또한 상속된다.

<br/>



### Life of a block
- 새로운 block 을 생성하거나 업데이트 하는 경우,

   - 해당 transaction 작업이 `local state` 에 반영

   - 네이티브 앱에서는 SQLite 또는 ⭐️IndexedDB⭐️ 위에 LRU 캐시인 RecordCache를 사용하여 접근한 모든 레코드를 로컬에 저장합니다.

- 그리고 나서  transaction 은 TransactionQueue 에 저장된다. 

   - 최종적으로 Notion 서버에 동기화된다.

- 실시간 업데이트의 경우, MessageStore 로의 웹 소켓 연결을 사용한다. 

   - 즉, 같은 페이지를 보고 있는 경우, Producer, Subscriber 구조로 연결되어 모든 block 들에 대한 subscriber 가 된다.

   - 변경 사항은 먼저 saveTransactions process 를 거치고 난 뒤, 해당 응답을 통해 MessageStore 에 새로운 recorded version 이 확인되면, 연결된 소켓들에게 변경 사항들을 전달한다.

   - 변경 사항을 받은 클라이언트들은 local cache 와 비교하여 version 을 확인한다. 

   - 그리고 나면, Notion 서버로 **syncRecordValues 요청을 보내게 되고, outdated 인 경우, 새로운 Record 를 응답받아 local cache 에 업데이트 및 re-render 한다.**

- block 읽기 과정은,

   - 링크를 통해 페이지를 열게 되면, 먼저 local cache 내용을 확인한다.

   - 이후 Notion API 를 통해서 version 을 비교하여, outdated 인 경우 re-rendering.

<br/>




---

## 드디어 local cache 데이터, 눈 앞에 오다

![](/assets/pages/1eafdee6-189c-46fe-a0fe-5bff83f07309/2456a53a-1772-450c-ba2c-d911c909f1d7.png)
![](/assets/pages/1eafdee6-189c-46fe-a0fe-5bff83f07309/61efae01-695d-4861-bc0d-0f3ce58729e0.png)
**SQLite DB Location :  /Users/user/Library/Application Support/Notion/notion.db **

- ⭐️ **조력자의 도움** ⭐️

<br/>



> 🦖 **자. 여기까지 왔는데, 과연 버튼 하나로 블로그 배포가 성공하였을까요?**

<br/>




---

## ⭐️ 조력자 ⭐️ GPT-4 홍보를 시작합니다.

> 🦖 **대부분의  막히는 부분에 대한 해결도 기능에 대한 코드 작성도 모두 ChatGPT 가 수행하였습니다.**

<br/>



### UUID v4
```YAML
Me : 
UUID v4 로 ID 를 저장할 경우 데이터 조회 및 수정에 있어서 성능적 혹은 기타 장점이 있는거야?

ChatGPT :
UUID v4를 사용하여 ID를 저장할 때 성능적이나 기타 장점은 다음과 같습니다:
  1. 고유성: UUID v4는 난수를 기반으로 생성되므로, 중복되거나 충돌할 확률이 매우 낮습니다. 이는 대규모 분산 시스템에서 특히 중요하며, 고유한 식별자가 필요한 경우에도 유용합니다.
  2. 비순차적 ID 생성: UUID는 일련번호와 달리 순차적이지 않습니다. 이는 레코드를 생성할 때 순차적 ID를 사용하면서 발생할 수 있는 인덱싱 성능 저하 문제를 완화할 수 있습니다.
  3. 보안: UUID v4는 난수로 생성되므로, 외부 공격자가 레코드의 ID를 예측하기 어렵습니다. 이를 통해 무차별 대입 공격(Brute Force Attack) 등의 보안 위협을 줄일 수 있습니다.
  4. 범용성: UUID는 다양한 시스템 및 언어에서 사용할 수 있으며, 표준화되어 있습니다. 이로 인해 여러 시스템 간에 식별자를 쉽게 교환하고 호환성 문제를 최소화할 수 있습니다.

그러나 UUID v4를 사용할 때 주의해야 할 몇 가지 단점도 있습니다:
  1. 저장 공간: UUID는 128비트이며, 일반적으로 36자의 문자열 형태로 표현됩니다. 이는 정수형 ID에 비해 저장 공간이 더 많이 필요합니다.
  2. 가독성: UUID는 길고 난수 기반으로 생성되므로, 사람이 읽고 이해하기 어렵습니다. 이로 인해 디버깅이나 로깅에서 어려움을 겪을 수 있습니다.
  3. 조회 성능: UUID는 인덱스를 기반으로 검색할 때 순차적이지 않으므로, 일부 데이터베이스에서 조회 성능에 영향을 미칠 수 있습니다. 이를 최적화하기 위해 데이터베이스 별로 적절한 인덱싱 전략을 적용해야 할 수도 있습니다.

결론적으로, UUID v4의 사용은 여러 장점을 제공하지만, 단점도 함께 고려해야 합니다. 상황에 따라 적절한 식별자 타입을 선택하는 것이 중요합니다.

---
Me :
UUID v4 를 빠르게 조회하기 위한 방법은 없을까? 성능 최적화 관점에서?

ChatGPT :
UUID v4를 빠르게 조회하기 위한 성능 최적화 방법은 다양하게 존재합니다. 데이터베이스 종류와 구조에 따라 사용할 수 있는 전략이 다르지만, 일반적인 몇 가지 방법을 소개합니다:
  1. 인덱싱: UUID 필드를 인덱싱하여 조회 성능을 향상시킬 수 있습니다. 인덱스는 데이터베이스에서 데이터를 빠르게 찾을 수 있도록 도와주는 구조입니다. 인덱싱을 사용하면 데이터베이스가 전체 테이블을 스캔하는 대신 인덱스를 이용해 레코드를 빠르게 찾을 수 있습니다.
  2. 파티셔닝: 테이블을 논리적 또는 물리적으로 여러 파티션으로 나누어 조회 성능을 개선할 수 있습니다. 이 방법은 특히 큰 테이블에서 유용하며, 쿼리가 특정 파티션 범위 내에서만 실행되도록 함으로써 전체 테이블 스캔을 줄이고 성능을 향상시킵니다.
  3. 클러스터링: 일부 데이터베이스 관리 시스템(DBMS)에서는 데이터를 클러스터링하여 저장할 수 있습니다. 클러스터링을 사용하면 관련 데이터를 물리적으로 가까운 위치에 저장하여 조회 성능을 향상시킬 수 있습니다. 예를 들어, PostgreSQL에서는 클러스터링 인덱스를 사용하여 UUID를 기준으로 데이터를 정렬할 수 있습니다.
  4. 압축 방식 변경: UUID는 크기가 큰 식별자이기 때문에, 압축 방식을 변경하여 저장 공간을 줄이는 것이 조회 성능에 도움이 될 수 있습니다. 예를 들어, MySQL에서는 BINARY(16) 형식으로 UUID를 저장하여 공간을 절약하고 성능을 개선할 수 있습니다.
  5. 캐싱: 자주 조회되는 UUID를 캐싱하여 데이터베이스에 대한 부하를 줄이고 성능을 향상시킬 수 있습니다. 캐싱은 메모리에 데이터를 임시로 저장하여 빠르게 접근할 수 있도록 합니다. 애플리케이션 레벨에서 캐싱을 구현할 수도 있고, 데이터베이스 관리 시스템에서 지원하는 캐싱 기능을 사용할 수도 있습니다.
```

[https://devs0n.tistory.com/39](https://devs0n.tistory.com/39)

- 물론 위 블로그 글을 확인하니, sequential 하게 id 를 생성하여 insert 비용을 낮출 수 있다고 한다.

<br/>



<br/>



### IndexedDB → SQLite
```YAML
Me :
너가 한 말 중에 "플랫폼에 따라 IndexedDB 또는 SQLite을 사용하여" 이 부분이 궁금한거야. 어떤 플랫폼에서는 IndexedDB 를 사용하고, 어떤 플랫폼에서는 SQLite 을 사용하는지 설명해줘.

ChatGPT :
네, 알겠습니다. Notion에서 사용하는 데이터베이스는 플랫폼에 따라 달라집니다. 일반적으로 IndexedDB와 SQLite의 사용이 다음과 같이 구분됩니다:

1. IndexedDB:
IndexedDB는 주로 웹 브라우저에서 사용되는 클라이언트 측 저장 기술입니다. Notion의 웹 버전에서는 IndexedDB를 사용하여 사용자 데이터를 로컬에 저장하고 관리합니다. 모든 주요 웹 브라우저(Chrome, Firefox, Safari 등)는 IndexedDB를 지원합니다.

2. SQLite:
SQLite는 가벼운 파일 기반의 데이터베이스로, 주로 모바일 및 데스크톱 애플리케이션에서 사용됩니다. Notion의 iOS, Android 및 데스크톱 애플리케이션(Windows, macOS)에서는 SQLite를 사용하여 사용자 데이터를 로컬에 저장하고 관리합니다.

결론적으로, Notion의 웹 버전에서는 IndexedDB를 사용하고, 모바일 및 데스크톱 애플리케이션에서는 SQLite를 사용하여 데이터를 저장하고 관리합니다. 이렇게 플랫폼에 적합한 데이터베이스를 사용함으로써, Notion은 각 플랫폼에서 최적의 성능과 사용자 경험을 제공할 수 있습니다.

---
Me :
그렇다면 현재 내 macbook 에 Notion App 이 실행 중인데, IndexedDB 데이터에 접근할 수 있는 방법이 있을까?

ChatGPT :
제가 이해한 바로는 현재 MacBook에서 Notion 애플리케이션을 사용 중이신 것 같습니다. 이 경우, Notion 애플리케이션은 SQLite 데이터베이스를 사용하여 데이터를 저장하고 관리합니다. 따라서 여러분이 찾으시는 것은 IndexedDB가 아닌 SQLite 데이터베이스입니다.

그럼에도 불구하고, 웹 브라우저를 사용하여 Notion에 접속한 경우에만 IndexedDB에 접근할 수 있습니다. 이 경우, 웹 브라우저의 개발자 도구를 사용하여 IndexedDB 데이터에 접근할 수 있습니다. 아래는 크롬에서 IndexedDB에 접근하는 방법입니다:

1. 크롬 브라우저를 열고 Notion 웹 애플리케이션에 로그인합니다.
2. 웹 페이지에서 마우스 오른쪽 버튼을 클릭하고 "검사"를 선택하여 개발자 도구를 엽니다.
3. 개발자 도구의 상단 탭에서 "Application" (또는 "Storage"로 변경된 경우도 있습니다)을 선택합니다.
4. 왼쪽 사이드바에서 "IndexedDB"를 찾아 펼칩니다. 그러면 Notion과 관련된 IndexedDB 데이터베이스가 표시됩니다.

하지만, Notion 데스크톱 애플리케이션의 경우 SQLite 데이터베이스에 접근하는 것이 더 적합합니다. SQLite 데이터베이스를 열기 위해 DB Browser for SQLite와 같은 도구를 사용하거나, SQLite 명령줄 도구를 사용하여 데이터베이스 파일을 열 수 있습니다. 일반적으로 Notion 애플리케이션의 데이터베이스 파일은 다음 위치에 저장됩니다:

- macOS: ~/Library/Application Support/Notion
- Windows: %APPDATA%\Notion
이 폴더에서 notion.db 또는 비슷한 이름의 파일을 찾아 SQLite 도구로 열 수 있습니다. 하지만 이 작업은 주의가 필요하며, Notion의 동작에 영향을 줄 수 있으므로 권장하지 않습니다. 이러한 작업은 데이터 손실 또는 문제가 발생할 수 있으므로 백업을 먼저 만들어 두는 것이 좋습니다.
```

<br/>



### SQLite Browser 및 코드 레벨 접근
```YAML
Me :
SQLite 도구는 어떤 것들이 있지? 혹시 Go 로 코드로 작성해서 cache 데이터에 접근할 수 없을까?

ChatGPT : 
SQLite 도구는 여러 가지가 있으며, 일반적으로 데이터베이스 생성, 조회, 수정, 삭제 등의 작업을 수행할 수 있습니다. 여기 몇 가지 인기 있는 SQLite 도구를 소개합니다:

1. DB Browser for SQLite (https://sqlitebrowser.org): 이 도구는 SQLite 데이터베이스를 시각적으로 탐색하고 관리할 수 있는 오픈 소스 애플리케이션입니다. macOS, Windows 및 Linux에서 사용할 수 있습니다.
2. SQLiteStudio (https://sqlitestudio.pl): 이 또한 오픈 소스이며, 사용이 간편한 SQLite 데이터베이스 관리 도구입니다. 여러 플랫폼에서 사용할 수 있습니다.
3. SQLiteSpy (http://www.yunqa.de/delphi/doku.php/products/sqlitespy/index): 이 도구는 Windows 전용이며, SQLite 데이터베이스를 빠르게 검토하고 분석할 수 있는 무료 프로그램입니다.
4. sqlite3: sqlite3는 SQLite에서 제공하는 기본 명령줄 도구로, 대부분의 운영 체제에 포함되어 있습니다. 이 도구를 사용하면 터미널에서 직접 SQLite 데이터베이스를 관리할 수 있습니다.

Go 언어를 사용하여 SQLite 데이터베이스에 접근하는 것도 가능합니다. Go에서 SQLite를 사용하려면 "github.com/mattn/go-sqlite3" 패키지를 사용할 수 있습니다. 이 패키지는 Go에서 SQLite 데이터베이스를 사용할 수 있게 해주는 도구입니다.

다음은 간단한 Go 코드 예제입니다:
...

이 예제에서는 ./notion.db라는 SQLite 데이터베이스 파일을 열고, some_table이라는 테이블에서 모든 레코드를 조회한 다음, 각 레코드의 id와 name을 출력합니다. 실제로 Notion의 데이터베이스에 접근하려면 적절한 테이블 이름과 열 이름을 사용해야 합니다.
```

