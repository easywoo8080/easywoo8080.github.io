---
title: mydoc
tags: [Jekyll]
keywords: Jekyll write 작성법 블로그 mydoc
last_updated: August 12, 2026
summary: "문서 작성법에 대한 설명"
sidebar: mydoc_sidebar
permalink: mydoc_example.html
folder: mydoc
---

조사해보니, 이 저장소는 단순한 Jekyll Markdown 문서가 아니라 **`_config.yml`의 설정 + Front Matter + Markdown + Sidebar 데이터**가 결합되어 동작하는 문서 사이트 테마입니다.

[원본 GitHub 저장소](https://github.com/tomjoht/documentation-theme-jekyll/tree/gh-pages?utm_source=chatgpt.com)

## 1. 가장 기본적인 문서 작성법

실제 문서는 주로 `pages/mydoc/` 아래에 `.md` 파일로 작성되어 있습니다. 예를 들어 `mydoc_code_samples.md`가 있습니다.

기본 형태는 다음과 같습니다.

```markdown
---
title: 문서 제목
tags: [formatting]
keywords: 키워드1 키워드2
last_updated: August 12, 2026
summary: "문서에 대한 간단한 설명"
sidebar: mydoc_sidebar
permalink: mydoc_example.html
folder: mydoc
---

# 문서 제목

본문을 작성합니다.

## 1. 소제목

내용입니다.

## 2. 소제목

내용입니다.
```

여기서 `---` 사이가 **Front Matter**입니다.

---

## 2. Front Matter가 중요함

이 테마에서는 단순히 Markdown만 작성하면 끝나는 게 아니라 위쪽 설정이 상당히 중요합니다.

### 주요 항목

| 항목             | 의미       |
| -------------- | -------- |
| `title`        | 문서 제목    |
| `tags`         | 태그       |
| `keywords`     | 검색용 키워드  |
| `last_updated` | 최종 수정일   |
| `summary`      | 문서 요약    |
| `sidebar`      | 사용할 사이드바 |
| `permalink`    | 생성될 URL  |
| `folder`       | 문서 그룹    |

예를 들어:

```yaml
---
title: DHCP 동작 과정
tags: [network, dhcp]
keywords: DHCP DORA Discover Offer Request ACK
last_updated: August 12, 2026
summary: "DHCP의 DORA 과정을 설명합니다."
sidebar: mydoc_sidebar
permalink: dhcp.html
folder: mydoc
---
```

그러면 `permalink`에 따라 문서 URL을 지정할 수 있습니다.

---

# 3. Markdown은 일반 Markdown과 거의 동일

본문은 일반적인 Markdown 문법을 사용합니다.

### 제목

```markdown
# DHCP

## DHCP란?

### DHCP 동작 과정
```

### 강조

```markdown
**중요한 내용**

*강조*

`코드`
```

### 목록

```markdown
- Discover
- Offer
- Request
- ACK
```

### 번호 목록

```markdown
1. Discover
2. Offer
3. Request
4. ACK
```

---

# 4. 코드 블록

이 테마는 **언어를 지정한 fenced code block**을 사용합니다. 실제 샘플 문서에서도 다음 방식을 사용합니다.

````markdown
```js
console.log('hello');
````

````

결과:

```js
console.log('hello');
````

예를 들어 Java라면:

````markdown
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
````

````

Python:

```markdown
```python
print("Hello")
````

````

Bash:

```markdown
```bash
git clone https://github.com/example/example.git
````

````

이 테마는 내부적으로 **Rouge**를 syntax highlighter로 사용합니다. 

---

# 5. 링크

일반 Markdown 링크를 사용합니다.

```markdown
[GitHub](https://github.com/)
````

또는 내부 문서끼리 연결할 때 테마에서 정의한 링크 참조를 사용할 수도 있습니다.

실제 문서에서도:

```markdown
[mydoc_help_api]
```

같은 형태를 사용하고 있습니다.

그리고 문서 마지막에:

```markdown
{% include links.html %}
```

를 넣는 패턴도 있습니다.

---

# 6. 이미지

일반 Markdown 방식으로 넣으면 됩니다.

```markdown
![DHCP 구조](images/dhcp.png)
```

또는 HTML을 직접 사용할 수도 있습니다.

```html
<img src="images/dhcp.png" alt="DHCP 구조">
```

다만 **이미지 경로는 Jekyll의 실제 파일 구조를 기준으로 잡아야 합니다.**

---

# 7. 표

GFM Markdown 표를 사용할 수 있습니다.

```markdown
| 단계 | 메시지 | 설명 |
|---|---|---|
| 1 | Discover | DHCP 서버 탐색 |
| 2 | Offer | IP 주소 제안 |
| 3 | Request | IP 주소 요청 |
| 4 | ACK | IP 주소 할당 |
```

`_config.yml`에서도 Markdown 엔진으로 `kramdown`을 사용하고 GFM 입력을 활성화하고 있습니다.

---

# 8. Alert / 경고 박스

이 테마의 특징 중 하나입니다.

예를 들어 문서에서 일반적인 Markdown만 사용하는 것이 아니라 테마가 제공하는 **Alert 스타일**을 사용할 수 있습니다.

이 부분은 저장소의 `mydoc_alerts.md`에 별도로 정리되어 있습니다.

즉 이 테마를 제대로 사용하려면 단순 Markdown 문법뿐 아니라:

* Alert
* Tooltip
* Include
* Sidebar
* Tab
* Content reuse
* Conditional logic

등 테마 자체 기능을 같이 익히는 것이 좋습니다.

---

# 9. Sidebar가 핵심

이 테마에서 일반 Jekyll과 가장 다른 부분입니다.

`_config.yml`에 다음과 같이 Sidebar들이 등록되어 있습니다.

```yaml
sidebars:
- home_sidebar
- mydoc_sidebar
- product1_sidebar
- product2_sidebar
- other
```

그리고 문서에서:

```yaml
sidebar: mydoc_sidebar
```

라고 지정합니다.

즉,

```text
Markdown 문서
       ↓
Front Matter
       ↓
sidebar: mydoc_sidebar
       ↓
mydoc_sidebar
       ↓
왼쪽 문서 메뉴
```

구조입니다.

따라서 **문서를 추가했는데 왼쪽 메뉴에 안 나타나는 경우**, Markdown 파일 자체보다 Sidebar 설정을 먼저 확인해야 합니다.

---

# 10. 실제 프로젝트 구조

이 저장소를 보면 대략 이런 구조입니다.

```text
documentation-theme-jekyll/
│
├── _config.yml
│
├── _data/
│
├── _includes/
│
├── _layouts/
│
├── _posts/
│
├── _tooltips/
│
├── pages/
│   │
│   ├── mydoc/
│   │   ├── mydoc_about.md
│   │   ├── mydoc_code_samples.md
│   │   ├── mydoc_collections.md
│   │   ├── ...
│   │
│   ├── product1/
│   ├── product2/
│   ├── news/
│   └── tags/
│
├── Gemfile
└── ...
```

실제로 `pages` 아래에는 `mydoc`, `news`, `product1`, `product2`, `tags` 등의 문서 그룹이 존재합니다.

---

## 11. 따라서 새 문서를 만든다면

예를 들어 네트워크 문서를 작성한다고 하면:

```text
pages/
└── mydoc/
    ├── network.md
    ├── dhcp.md
    ├── arp.md
    └── subnet.md
```

`dhcp.md`:

````markdown
---
title: DHCP
tags: [network, dhcp]
keywords: DHCP DORA Discover Offer Request ACK
last_updated: August 12, 2026
summary: "DHCP의 동작 과정과 DORA 절차를 설명합니다."
sidebar: mydoc_sidebar
permalink: dhcp.html
folder: mydoc
---

# DHCP

DHCP는 네트워크에 연결된 장치에 IP 설정을 자동으로 할당하는 프로토콜입니다.

## DORA

DHCP는 다음 네 단계로 동작합니다.

1. Discover
2. Offer
3. Request
4. ACK

## DHCP Discover

클라이언트가 DHCP 서버를 찾기 위해 메시지를 전송합니다.

```text
Client → DHCP Server
DHCP Discover
````

## DHCP Offer

서버가 사용할 IP 주소를 제안합니다.

```text
DHCP Server → Client
DHCP Offer
```

````

이런 식으로 작성하면 됩니다.

---

## 12. 이 테마에서 특히 알아야 할 것

제가 보기에는 이 저장소를 사용할 때 **아래 순서로 공부하는 것이 가장 효율적**입니다.

```text
① Markdown
   ↓
② Front Matter
   ↓
③ Sidebar
   ↓
④ Include
   ↓
⑤ Alert / Tab
   ↓
⑥ Tooltip
   ↓
⑦ Content reuse
   ↓
⑧ Jekyll 변수 / Liquid
````

특히 **①~③만 알아도 일반적인 기술문서 작성은 충분히 가능합니다.**

그리고 이 테마의 `_config.yml`에는 `pages`, `posts`, `tooltips` 각각에 기본 `layout`, `sidebar`, `search`, `comments` 등을 자동 적용하는 설정도 들어가 있습니다.

### 핵심만 정리하면

```text
.md 파일
  │
  ├─ Front Matter
  │    ├─ title
  │    ├─ permalink
  │    ├─ sidebar
  │    └─ tags / keywords
  │
  └─ Markdown 본문
       ├─ 제목
       ├─ 목록
       ├─ 표
       ├─ 코드
       ├─ 이미지
       └─ 링크
```

**즉, 이 저장소에서 문서 작성의 핵심은 `Markdown + Front Matter + Sidebar` 3개입니다.**

원하시면 다음으로 이 저장소의 **`mydoc_sidebar` 작성법까지 실제 파일을 기준으로 분석해서, "문서 추가 → 왼쪽 메뉴 추가 → 하위 메뉴 추가 → 접기/펼치기"까지 한 번에 정리**해드릴 수 있습니다.
