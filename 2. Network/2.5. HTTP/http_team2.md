# HTTP

## 관련 질문
<details>
  <summary>HTTP 통신은 OSI 7계층에서 어떤 계층에 속하나요?</summary>
  <blockquote>
    OSI 7계층에서 애플리케이션 계층에 속합니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTP/1.1이 HTTP/1.0에 비해 개선된 점을 설명해주세요</summary>
  <blockquote>
    HTTP/1.1의 경우 클라이언트와 서버가 통신할 때, TCP를 초기화한 이후 keep-alive라는 옵션으로 RTT의 감소 효과를 얻었습니다.<br/>
    HTTP/1.0에도 keep-alive라는 옵션은 존재했지만, 표준화가 되어 있지 않아 사실상 HTTP/1.1에서 개선된 사항으로 볼 수 있습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTP/2에서 HTTP/1.1에 비해 개선된 것 중 한 가지만 말씀해주시고, 그 장점에 대해 설명해주세요</summary>
  <blockquote>
    HTTP/2에서 개선된 사항으로는 멀티플렉싱이 있습니다.<br/>
    멀티플렉싱은 클라이언트와 서버의 통신에서 하나의 요청으로 여러 파일을 응답할 수 있는 기능인데, 이로인해 HTTP/1.1의 문제점은 HOL Blocking이 해결됐습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>www.naver.com을 주소창에 입력하면 어떻게 될까요?</summary>
  <blockquote>
    <a href="https://youtu.be/YahjHM9UNCA?si=Pj_wt2ZaOZ7SsxDB">링크 참고</a>
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTP/3가 HTTP/2에 비해 변경된 점을 설명해주세요</summary>
  <blockquote>
    HTTP/3는 UDP 기반으로 QUIC라는 계층 위에서 동작합니다.<br/>
    TCP를 사용하지 않기 때문에 3-way handshake 과정을 거치지 않고, 이 덕분에 초기 연결 설정 시 지연 시간 감소라는 효과를 얻었습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTPS에 대해 설명해주세요</summary>
  <blockquote>
    HTTP Secure로 HTTP에 보안이 추가된 형태입니다.<br/>
    SSL/TLS 계층을 넣어 통신을 암호화하며 이를 통해 공격자가 사용자 정보를 가로채는 인터셉터를 방지할 수 있습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTPS에 인증 메커니즘을 수행하는 방법을 설명해주시고 인증서 발급이 가능한 기업을 하나만 말씀해주세요</summary>
  <blockquote>
    CA에서 발급한 인증서를 기반으로 사용자가 해당 서버를 신뢰할 수 있는 서버로 보장받으면 사이트의 인증이 됩니다.<br/>
    인증서 발급 방법으로는 사이트의 공개키를 CA에 제출하여 인증서를 발급받을 수 있습니다.<br/>
    CA 발급이 가능한 기업으로는 대표적으로 아마존이 있습니다.
  </blockquote>
</details>

<br/><br/>

## HTTP란?
- HyperText Transfer Protocol
- 하이퍼텍스트 링크를 사용하여 웹 페이지를 로드하는 데 사용
- OSI 7계층에서 애플리케이션 계층
- HTTP/1.0부터 시작해서 현재는 HTTP/3까지 발전함

## HTTP/1.0
- HTTP/1.0은 한 연결당 하나의 요청을 처리하도록 설계됨
- 단점으로 요청이 증가할수록 RTT가 증가<br/>
> 따라서, RTT의 증가를 해결하기 위한 방향으로 발전했다.

`RTT : 패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간이며 패킷 왕복 시간`

<br/>

### RTT 증가를 해결하기 위한 방법
1. 이미지 스플리팅
	- 많은 이미지를 다운로드받을 경우 과부하가 발생
    - 많은 이미지가 합쳐 있는 하나의 이미지를 다운받아 css의 background-position을 이용해 이미지를 표기하는 방법
    - 예제 코드
      ```css
      #icons>li>a {
        background-image: url("icons.png");
        width: 25px;
        display: inline-block;
        height: 25px;
        repeat: no-repeat;
      }
      #icons>li:nth-child(1)>a {
        background-position: 2px -8px;
      }
      #icons>li:nth-child(2)>a {
        background-position: -29px -8px;
      }
      ```

2. 코드 압축
	- 이름 그대로 작성한 코드를 띄어쓰기, 개행을 포함해 압축하는 방법
    - 예제 코드
      ```js
      const express = require('express')
      const app = express()
      const port = 3000
      
      app.get('/', (req, res) => {
        res.send('Hello World!')
      })

      app.listen(port, () => {
          console.log(`Example app listening on port ${port}`)
        })
      ```
    - 이렇게 긴 코드를 아래처럼 압축
      ```js
      const express=require("express"),app=express(),port=3e3;app.get("/",(e,p)=>{p.send("Hello World!")}),app.
      listen(3e3,()=>{console.log("Example app listening on port 3000")});
      ```

3. 이미지 Base64 인코딩
	- 이미지 파일을 64진법으로 이루어진 문자열로 인코딩하는 방법
    - 장점 : 이미지에 대해 서버에 HTTP 요청을 할 필요 없음
    - 단점 : Base64 문자열로 변환할 경우 37% 정도 크기가 더 커짐

    `인코딩 : 정보의 형태나 형식을 표준화, 보안, 처리 속도 향상, 저장 공간 절약 등을 위해 다른 형태나 형식으로 변환하는 처리 방식`
    
<br/>

#### 이미지 인코딩
> 이미지 인코딩은 무엇이고, RTT는 감소하는데 왜 크기는 더 커질까?<br/>
[이미지 인코딩 방식](https://velog.io/@wns450/이미지-인코딩-방식)

## HTTP/1.1
- HTTP/1.0에서 HTTP/2로 발전하지 않고 HTTP/1.1로 한번 거쳐 발전
- HTTP/1.1의 경우 TCP를 초기화한 이후 keep-alive라는 옵션으로 여러 파일 송수신이 가능
- HTTP/1.0에도 keep-alive는 존재하지만, 비표준화 상태
![keep-alive](https://velog.velcdn.com/images/calendar2/post/6686ba7a-8e77-4240-b190-836e0c216fff/image.jpg)

> 그림처럼 HTTP/1.1에서는 TCP 세션을 유지하는 keep-alive 옵션이 표준화되어 있어, 통신 간에 RTT를 감소할 수 있었다.<br/>
다만, 후술할 두 가지 단점이 있어 HTTP/2로 발전한다.

### HTTP/1.1 단점
#### HOL Blocking(Head Of Line Blocking)
- 네트워크에서 같은 큐에 있는 패킷이 그 첫 번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상

![HOLB](https://velog.velcdn.com/images/calendar2/post/dd070e8e-8a25-4c66-afb3-8cea024e89ce/image.jpg)

> 그림처럼 첫 번째 요청에 대한 응답이 지연되면서 뒤에 있는 두 번째, 세 번째 요청에 대한 응답도 지연되는 현상이 HOL Blocking 현상이다.

#### 무거운 헤더 구조
- HTTP/1.1부터 헤더에 쿠키와 같은 많은 메타데이터를 포함
- 압축이 되지 않아 무거워짐

## HTTP/2
- HTTP/1.1의 단점을 보완하며 등장
- 개선사항으로 멀티플렉싱, 헤더 압축, 서버 푸시가 존재

### 멀티플렉싱
- 멀티 프로세스, 멀티 쓰레드와 비슷한 개념
- HTTP/1.1까지는 하나의 요청과 하나의 응답에서 하나의 파일만이 전달
- HTTP/2에서는 멀티플렉싱을 통해 하나의 요청과 하나의 응답에서 여러 파일 전달이 가능
> 즉, 데이터 전달 속도가 비약적으로 증가했다.<br/>
이 기술의 발전으로 HTTP/1.1의 HOL Blocking이 해결되었다.

<br/>

### 헤더 압축
- HTTP/1.1의 문제인 무거운 헤더를 압축하여 해결
- 헤더를 압축하기 위해 허프만 코딩 알고리즘을 활용

#### 허프만 코딩 알고리즘이란?
- 문자열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트 수를 사용하여 표현하고, 빈도가 낮은 정보는 비트 수를 많이 사용하여 표현해서 전체 데이터의 표현에 필요한 비트양을 줄이는 원리
- 더 자세한 내용은 링크를 참조<br/>
[허프만 코딩](https://velog.io/@junhok82/허프만-코딩Huffman-coding)

### 서버 푸시
- 클라이언트의 요청 없이 서버가 리소스를 푸시하는 것
> 이게 무슨 말이냐하면 웹 페이지를 로드할 때 일반적으로 클라이언트는 html 파일을 요청한다.<br/>
그럼 서버는 html 파일을 응답해주는데, html 파일에는 요소를 꾸밀 css가 종속된 경우가 많다.<br/>
그럼 HTTP/1.1의 경우 클라이언트가 css 파일을 한 번 더 요청한다.<br/>
반면, HTTP/2의 경우 html 파일을 응답하면서 css 파일도 푸시해준다.<br/>
이 서버 푸시라는 기능이 발달하면서 이후에 모바일의 앱 푸시 알림과 같은 기능의 구현이 가능해진다.

<br/>

## HTTP/3
> HTTP/2에서 지금 우리가 사용하고 있는 HTTP/3으로 발전했다.<br/>
HTTP/2와 비교해서 다음 사항이 개선되고 변경되었다.

- HTTP/2는 TCP 위에서 동작, HTTP/3은 QUIC라는 계층 위에서 동작
- HTTP/3은 TCP 기반이 아닌 UDP 기반
> 이 개선사항은 초기 연결 설정 시 지연 시간 감소의 효과를 얻었다.

<br/>

### 초기 연결 설정 시 지연 시간 감소
![QUIC](https://velog.velcdn.com/images/calendar2/post/4032ef7f-cbbd-4c64-b4bb-c81b7475e933/image.jpg)

> 그림을 보면 QUIC는 3-웨이 핸드셰이크 과정을 거치지 않는다.<br/>
그렇기에 첫 연결 설정에서 1-RTT만 소요되며, 클라이언트와 서버가 한 번의 요청, 응답만 성공하면 바로 본 통신이 시작된다.<br/>
TCP/UDP 등의 개념은 이것보다 훨씬 더 복잡하다.<br/>
더 깊은 지식은 아래 링크 참고<br/>
[[네트워크] TCP/UDP와 3-Way Handshake & 4-Way Handshake](https://velog.io/@averycode/네트워크-TCPUDP와-3-Way-Handshake4-Way-Handshake)

<br/>

## HTTPS
> HTTPS는 HTTP Secure로 기존 HTTP 통신에 보안이 추가된 형태이다.<br/>
HTTP/2부터 HTTPS 위에서 동작하였고, 애플리케이션 계층과 전송 계층 사이에 SSL/TLS 계층을 넣으면서 통신을 암호화한다.

```
SSL : Secure Socket Layer
TLS : Transport Layer Security Protocol
```

### SSL/TLS
- SSL 1.0부터 TLS 1.3까지 발전
- 클라이언트와 서버가 통신할 때 제 3자가 사용자 정보를 인터셉터 방지
- 보안 세션을 기반으로 데이터를 암호화
- 인증 메커니즘, 키 교환 암호화 알고리즘, 해싱 알고리즘 사용

> SSL/TLS는 HTTP에 보안을 제공하는데, 클라이언트와 서버가 통신할 때 제 3자가 메시지를 도청하거나 변조하지 못하도록 한다.

#### 보안 세션
- 보안이 시작되고 끝나는 동안 유지되는 세션
- SSL/TLS는 핸드셰이크를 통해 보안 세션을 생성

`세션이란? : 운영체제가 어떠한 사용자로부터 자신의 자산 이용을 허락하는 일정한 기간을 뜻한다. 즉, 사용자는 일정 시간 동안 응용 프로그램, 자원 등을 사용할 수 있다.`

> HTTPS 통신을 할 때, 클라이언트는 서버에 **사이퍼 슈트**를 전달한다.<br/>
서버는 전달받은 사이퍼 슈트의 암호화 알고리즘 리스트를 제공할 수 있는지 확인하며, 제공할 수 있다면 인증 메커니즘이 진행된다.

#### 사이퍼 슈트
- 프로토콜, AEAD 사이퍼 모드, 해싱 알고리즘이 나열된 규칙
- 다섯 개가 존재
  - TLS_AES_128_GCM_SHA256
  - TLS_AES_256_GCM_SHA384
  - TLS_CHACHA20_POLY1305_SHA256
  - TLS_AES_128_GCM_SHA256
  - TLS_AES_128_GCM_8_SHA256
  
> 예를 들어 첫 번째 사이퍼 슈트의 경우에는 TLS 프로토콜, AES_128_GCM라는 AEAD 사이퍼 모드, SHA256 해싱 알고리즘이 들어있다.

#### AEAD 사이퍼 모드
- Authenticated Encryption with Associated Data
- 데이터 암호화 알고리즘

> AES_128_GCM의 경우 128비트의 키를 사용하는 표준 블록 암호화 기술과 병렬 계산에 용이한 암호화 알고리즘인 GCM이 결합된 것을 뜻한다.

#### 인증 메커니즘
- CA(Certificate Authorities)에서 발급한 인증서를 기반으로 이뤄짐
- 인증서는 서비스 정보, 공개키, 지문, 디지털 서명 등으로 이뤄짐

> CA에서 발급한 인증서로 '공개키'를 클라이언트에 제공하면 안전한 연결이 가능하며, 신뢰할 수 있는 서버임을 보장한다.
CA 발급은 아무나 할 수 없는데, 대표적으로 Comodo, GoDaddy, GlobalSign, 아마존 등이 가능하다.

#### 암호화 알고리즘
- 키 교환 암호화 알고리즘으로는 두 가지가 존재
  - 대수곡선 기반 : ECDHE
  - 모듈식 기반 : DHE
- 두 알고리즘 모두 디피-헬만 방식을 근간으로 제작

> 디피-헬만 알고리즘이란?
y = g^x mod p
위 식에서 g와 x와 p를 안다면 y는 구하기 쉽지만 g와 y와 p를 안다면 x를 구하기는 어렵다는 원리에 기반한 알고리즘이다.<br/>
더 자세한 내용은 링크 참고<br/>
[디피 헬먼, DH 알고리즘](https://blog.naver.com/vjhh0712v/221469049348)

#### 해싱 알고리즘
- 데이터를 추정하기 힘든 더 작고, 섞여 있는 조각으로 만드는 알고리즘
- SSL/TLS는 SHA-256과 SHA-384 알고리즘을 사용

> SHA-256 알고리즘의 경우 해시 함수의 결과값이 256비트인 알고리즘이다.<br/>
쉽게 말하면 어떤 길이의 값을 입력해도 256비트의 고정된 결과값을 만들어서 출력하는 방식이다.<br/>
더 자세한 내용은 링크를 참고<br/>
[SHA-256?](https://bloccat.tistory.com/4)

```
해시 : 다양한 길이를 가진 데이터를 고정된 길이를 가진 데이터로 매핑(mapping)한 값
해싱 : 임의의 데이터를 해시로 바꿔주는 일이며 해시 함수가 이를 담당
해시 함수 : 임의의 데이터를 입력으로 받아 일정한 길이의 데이터로 바꿔주는 함수
```

### HTTPS와 SEO
- SEO란 Search Engine Optimization으로 검색엔진 최적화를 뜻함
- 구글 검색은 사이트 내 모든 요소가 동일할 경우 HTTPS 서비스를 하는 사이트가 SEO 순위가 높음
- SEO 최적화를 위해 캐노니컬 설정, 메타 설정, 페이지 속도 개선, 사이트맵 관리 등의 방법이 존재

#### 캐노니컬 설정
- 다음처럼 사이트 link에 캐노니컬을 설정
  ```html
  <link rel="canonical" href="https://example.com/page2.php" />
  ```

#### 메타 설정
- html 파일의 head 부분에 메타를 설정
- 아래는 애플 웹 사이트의 메타
  ```html
  <meta property="analytics-track" content="Apple - Index/Tab">
  <meta property="analytics-s-channel" content="homepage">
  <meta property="analytics-s-bucket-0" content="applestoreww">
  <meta property="analytics-s-bucket-1" content="applestoreww">
  <meta property="analytics-s-bucket-2" content="applestoreww">
  <meta name="Description" content="Discover the innovative world of Apple and shop everything iPhone,
  iPad, Apple Watch, Mac, and Apple TV, plus explore accessories, entertainment, and expert device
  support.">
  <meta property="og:title" content="Apple">
  ```

#### 페이지 속도 개선
> 웹 페이지의 로딩 속도가 느릴 경우, 사용자의 감소로 이어지고 이는 검색엔진 노출의 어려움으로 이어진다.

#### 사이트맵 관리
- 사이트맵을 정기적으로 관리하여 SEO 최적화
- 예시 사이트맵(xml 파일로 되어있다)
  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
      <loc>http://kundol.co.kr/</loc>
      <lastmod>수정날짜</lastmod>
      <changefreq>daily</changefreq>
      <priority>1.1</priority>
    </url>
  </urlset>
  ```

### HTTPS 구축 방법
- CA에서 구매한 인증키를 기반으로 HTTPS 서비스를 구축
- 서버 앞단의 HTTPS를 제공하는 로드밸런서를 두어 구축
- 서버 앞단에 HTTPS를 제공하는 CDN을 둬서 구축