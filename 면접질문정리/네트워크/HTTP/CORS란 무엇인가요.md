# CORS란 무엇인가요?

도메인 또는 포트가 다른 서버의 자원을 요청하는 메커니즘

**교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)**는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제

> 👉🏻 CORS 체제는 브라우저와 서버 간의 안전한 교차 출처 요청 및 데이터 전송을 지원한다.
> 최신 브라우저는 XMLHttpRequest 또는 Fetch와 같은 API에서 CORS를 사용하여 교차 출처 HTTP 요청의 위험을 완화 한다.

-   웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행한다

-   ⭐ 브라우저는 보안 상의 이유로, 스크립트에서 시작한 교차 출처 HTTP 요청을 제한한다.
    ex) domain-a.com ↔domain-b.com 간의 요청은 CORS 정책 위반으로, 브라우저에서 요청을 제한)

-   따라서 다른 출처의 리소스를 불러오기 위해서는, 그 출처에서 교차 출처 리소스 공유에 대한 헤더(CORS)를 응답시 반환 해주어야 한다

## CORS는 어떻게 동작하나요?

1. 기본적으로 웹은 다른 출처의 리소스를 요청할 때는 HTTP 프로토콜을 사용하여 요청을 하는데, 이때 브라우저는 요청 헤더(request header)에 Origin 필드에 요청을 보내는 출처를 담아 전송한다.
2. 서버는 요청에 대한 응답을 하는데, 응답 헤더(response header)에 Access-control-Allow-Origin 이라는 값에 '이 리소스를 접근하는 것이 허용된 출처'를 내려준다. 이후 응답을 받은 브라우저는 자신이 보냈던 요청의 Origin과 서버가 보내준 응답의 Access-Control-Allow-Origin을 비교해본 후 이 응답이 유효한 응답인지 아닌지를 결정한다

> 이것이 기본적인 CORS 동작의 흐름이다. 하지만 모든 CORS 동작의 방식은 아니다.

## CORS 동작의 시나리오

### 1. Preflight Request

Preflight 방식은, 요청을 한번에 보내는 것이 아니라 예비 요청과 본 요청으로 나누어서 서버로 전송한다.

본 요청을 보내기 전 미리 예비로 보내는 요청을 Preflight라고 하며, HTTP 메서드 중 하나인 OPTIONS 메서드를 사용한다.

> WHY?
> 예비 요청을 함으로써 본 요청을 보내기 전 브라우저 스스로가 요청을 보내는 것에 대한 안전성을 확인함에 있다.
> 서버는 이 예비 요청에 대한 응답으로 현재 자신이 어떤 것들을 허용 하고, 어떤 것들을 금지하고 있는지에 대한 정보를 응답 헤더에 담아서 브라우저에게 다시 보내준다.

단순히 Origin에 대한 정보 뿐만 아니라 자신이 예비 요청 이후에 보낼 본 요청에 대한 다른 정보들도 함께 전송 한다. 어떤 헤더를 포함 할 것인지, 어떤 HTTP 메서드를 사용하여 요청을 보낼 것인지 말이다.

### 2. Simple Request

Preflight 요청과는 달리, 예비 요청을 보내지 않고, 서버에게 바로 본 요청을 전송한다.

이 후 서버가 응답 헤더에 Access-Control-Allow-Origin과 같은 값을 보내주면 그때 브라우저가 CORS 정책 위반 여부를 검사하는 방식이다.

#### 동작 조건

1. 요청의 메서드는 GET, HEAD, POST 중 하나여야 한다.
2. Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width 외의 다른 헤더를 사용하면 안된다.
3. 만약 Content-Type를 사용하는 경우에는 application/x-www-form-urlencoded, multipart/form-data, text/plain만 허용된다.

### 3. Credentialed Request

Credentialed Request.
인증된 요청을 사용하는 방법이다.

다른 출처 간 통신의 좀 더 보안을 강화하고자 할 때 사용한다. 브라우저가 제공하는 비동기 리소스 요청 API인 XMLHttpRequest 객체나 fetch API는 별도의 옵션 없이 브라우저의 쿠키 정보나 인증과 관련된 헤더를 함부로 요청에 담지 않는다. 이때 요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 바로 credentials 옵션이다.

credentials도 세가지 옵션을 가지고 있다.

-   same-origin : 같은 출처 간 요청에만 인증 정보를 담을 수 있다.
-   include : 모든 요청에 인증 정보를 담을 수 있다.
-   omit - : 모든 요청에 인증 정보를 담지 않는다.

    > 👉🏻 다른 출처 사이트로의 요청에 쿠키와 같은 인증정보를 포함시키고자 한다면 ?
    > → credentials: 'include' 옵션을 추가

동작 조건

1. Access-Control-Allow-Origin: \* 이면 안되며, 명시적인 URL을 설정하여햐 한다.
   ex) Access-Control-Allow-Origin: https://xxx.com
2. 응답 헤더에는 반드시 Access-Control-Allow-Credentials: true가 존재해야한다.

-   출처 https://evan-moon.github.io/2020/05/21/about-cors/#credentialed-request
