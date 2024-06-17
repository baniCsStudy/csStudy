
## 관련 질문
<details>
  <summary> HTTP 메소드에 대해서 설명해주세요.</summary>
  <blockquote>
    클라이언트가 서버에 전송하는 요청의 종류를 정의한 것으로, 대표적으로 GET, POST, PUT, DELETE, PATCH가 있습니다. GET은 서버에서 데이터를 요청, POST는 서버에 데이터를 전송, PUT은 서버에 있는 데이터의 전체 내용을 대체, DELETE는 서버에서 데이터를 삭제, PATCH는 서버에 있는 데이터의 부분을 업데이트하는 역할을 합니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTP와 HTTPS의 차이에 대해서 설명해주세요.</summary>
  <blockquote>
    HTTP는 서버와 클라이언트 간 보안 절차가 없지만, HTTPS는 암호화, 복호화와 같은 보안 절차를 걸치기 때문에 보안 측면에서 훨씬 안전합니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTP의 status code에 대해서 설명해주세요.</summary>
  <blockquote>
    서버가 클라이언트에게 요청 처리 결과를 알려주는 상태 코드로, 100번대부터 500번대까지 존재합니다. 1XX는 정보 응답, 2XX는 성공, 3XX는 리디렉션, 4XX는 클라이언트 오류, 5XX는 서버 오류로 요약할 수 있습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>HTTP/1.1에 비해 HTTP/2에서 개선된 사항에 대해서 설명해주세요.</summary>
  <blockquote>
    1.1에 비해 지연시간이 줄어들어 응답 시간이 더 빨라졌으며 멀티플렉싱을 지원합니다. 멀티플렉싱은 여러 개의 스트림을 사용하여 송수신하는 것으로, 특정 스트림의 패킷이 손실되어도 나머지 스트림은 멀쩡하게 동작하도록 하는 역할을 합니다.
</details>
<br/> 
<details>
  <summary>HOL Blocking에 대해서 설명해주시고 해결하기 위한 방법을 말씀해주세요.</summary>
  <blockquote>
    HOL Blocking은 네트워크에서 같은 큐에 있는 패킷이 그 첫 번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상을 말합니다. 이러한 현상은 멀티플렉싱을 이용해 여러 개의 스트림을 병렬적으로 처리함으로써 해결할 수 있습니다.
</details>
<br/>
<details>
  <summary>검색엔진 최적화를 하기 위한 방법에 대해서 말씀해주세요.</summary>
  <blockquote>
    검색엔진을 최적화하기 위한 방법으로는 캐노니컬 설정, 메타 설정, 페이지 속도 개선, 사이트맵 관리 등이 있습니다. 
</details>
<br/>

<hr/>

## HTTP (Hypertext Transfer Protocol)

웹 브라우저와 웹 서버 간의 통신을 위한 표준 프로토콜. 사용자가 웹 사이트를 방문하면 사용자 브라우저가 웹 서버에 HTTP 요청을 전송하고 웹 서버는 HTTP 응답으로 응답

### HTTP/1.1/2/3

최초의 HTTP 버전이 HTTP/1.1이고, HTTP/2와 HTTP/3은 프로토콜 자체를 업그레이드한 버전. 데이터 전송 시스템을 수정하며 효율성을 개선

### HTTP 메소드

클라이언트가 서버에 전송하는 요청의 종류를 정의

- **GET**:
  - 서버로부터 데이터를 요청
  - 요청 데이터는 URL 쿼리 문자열에 포함

- **POST**:
  - 서버에 새로운 데이터를 생성하거나 기존 데이터를 업데이트
  - 요청 데이터는 HTTP 메시지 본문에 포함
  - 서버 상태를 변경할 수 있는 요청에 사용됨

- **PUT**:
  - 서버에 있는 데이터를 대체하거나 업데이트
  - POST와 유사하지만, PUT은 데이터의 전체 내용을 대체

- **DELETE**:
  - 서버에 있는 데이터를 삭제

- **PATCH**:
  - 데이터의 부분적인 업데이트
  - PUT과 달리 데이터의 전체 내용을 대체하지 않음

#### ❔ GET보다 POST가 보안 측면에서 더 좋다?

- URL에 데이터의 정보가 들어있지 않아 더 안전함

#### ❔ POST보다 GET이 속도가 더 빠르다?

- GET은 캐싱을 하기 때문에 더 빠를 수 있음

### HTTP 상태 코드 (Status Code)

서버가 클라이언트에게 요청 처리 결과를 알려주는 상태 코드

- **1XX**: 정보 응답
- **2XX**: 성공
- **3XX**: 리디렉션
- **4XX**: 클라이언트 오류
- **5XX**: 서버 오류

## HTTPS (Hypertext Transfer Protocol Secure)

HTTP의 확장 버전 또는 더 안전한 버전. HTTPS에서는 브라우저와 서버가 데이터를 전송하기 전에 안전하고 암호화된 연결을 설정

### HTTP와의 차이

1. **보안**
   - HTTP 메세지는 일반 텍스트이므로 권한이 없는 당사자가 인터넷을 통해 쉽게 엑세스하고 읽을 수 있지만, HTTPS는 모든 데이터를 암호화된 형태로 전송하므로 제3자가 데이터를 가로챌 수 없음
   - HTTPS에서는 HTTP 요청 및 응답을 추가로 암호화하기 위해 SSL/TLS와 함께 HTTP/2를 사용

2. **권위**
   - 검색 엔진은 HTTP의 신뢰성이 더 낮기 때문에 보통 HTTP 웹 사이트 콘텐츠의 순위를 HTTPS 웹 페이지보다 낮게 지정

3. **성능**
   - HTTPS 웹 애플리케이션은 HTTP 애플리케이션보다 로드 속도가 더 빠름

### SSL/TLS 인증서

시스템에서 ID를 확인하고 이후에 Secure Sockets Layer/전송 계층 보안(SSL/TLS) 프로토콜을 사용하여 다른 시스템에 대한 암호화된 네트워크 연결을 설정할 수 있도록 하는 디지털 객체

### 보안을 위해 고려해야 할 HTTP 관련 사항

1. **HTTPS 사용**
   - HTTPS는 SSL/TLS 암호화를 통해 데이터 전송을 안전하게 보호

2. **CORS (Cross-Origin Resource Sharing) 정책 설정**
   - CORS 정책은 브라우저에서 다른 출처의 리소스 접근을 제한하여 보안을 강화. 허용된 출처, 메서드, 헤더 등을 명시적으로 설정해야 함

3. **HTTP 보안 헤더 관리**
   - HTTPS 사용을 강제하거나 콘텐츠 소스의 허용 범위를 제한하는 등의 방법으로 외부로부터의 공격을 방지

<hr/>

<details>
  <summary>출처</summary>
  <div>https://aws.amazon.com/ko/compare/the-difference-between-https-and-http/</div>
  <div>https://www.cloudflare.com/ko-kr/learning/ddos/glossary/hypertext-transfer-protocol-http/</div>
  <div>https://velog.io/@haron/HTTP-%EB%A9%94%EC%84%9C%EB%93%9C%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%84%EB%8A%94%EB%8C%80%EB%A1%9C-%EB%A7%90%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94</div>
</details>
