# URI (Uniform Resource Identifier)

URI는 로케이터(locator), 이름(name) 또는 둘다 추가로 분류될 수 있다.

![ex_screenshot](./img/uri.png)

![ex_screenshot](./img/urlurn.png)

## URI란

-   Uniform: 리소스 식별하는 통일된 방식
-   Resource: 자원, URI로 식별할 수 있는 모든 것(제한없음)
-   Identifier: 다른 항목과 구분하는데 필요한 정보

-   URL: Uniform Resource Locator
-   URL: Uniform Resource Name

## URL, URN

-   URL - Locator: 리소스가 있는 위치를 지정
-   URN - Name: 리소스에 이름을 부여
-   위치는 변할 수 있지만, 이름은 변하지 않는다.
-   urn:isbn:8960777331 (어떤 책의 isbn URN)
-   URN 이름만으로 실제 리소스를 찾는 방법이 보편화되있지 않음.

### URL 전체 문법

-   sheme://[userinfo@]host[:port][/path][?query][#fragment]
-   https://www.google.com:444/search?q=hello&hl=ko

-   주로 프로토콜 사용
-   프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
    -   예) http, https, ftp 등등
-   http는 80포트, https는 443 포트를 주로 사용, 포트는 생략 가능
-   https는 http에 보안 추가(HTTP Secure)
