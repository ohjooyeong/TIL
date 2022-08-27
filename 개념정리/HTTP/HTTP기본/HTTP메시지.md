# HTTP 메시지

## HTTP 요청, 응답 메시지 구조

![ex_screenshot](./img/httpmsg.png)

### 시작라인

요청 메시지

-   start-line = request-line / status-line
-   request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)

-   HTTP 메서드 (GET: 조회)
-   요청 대상(/search?q=hello?hl=ko)
-   HTTP version

-   종류: GET, POST, PUT, DELETE

    -   GET: 리소스 조회
    -   POST: 요청 내역 처리

응답 메시지

-   status-line = HTTP-version SP status-code SP reason-phrase CRLF

-   HTTP 버전
-   HTTP 상태 코드: 요청 성공, 실패를 나타냄
    -   200: 성공
    -   400: 클라이언트 요청 오류
    -   500: 서버 내부 오류
-   이유 문구: 사람이 이해할 수 있는 짧은 상태 코드 설명 글

### 헤더 라인

-   header-field = field-name : OWS field-value OWS
-   field-name은 대소문자 구문 없음

용도

-   HTTP 전송에 필요한 모든 부가정보
-   예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보
-   표준 헤더가 너무 많음
-   필요시 임의의 헤더 추가 가능

### 메시지 바디

-   실제 전송할 데이터
-   HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능
