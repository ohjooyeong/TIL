# TCP, UDP

## 인터넷 프로토콜 스택의 4계층

애플리케이션 계층 - HTTP, FTP
전송 계층 - TCP, UDP
인터넷 계층 - IP
네트워크 인터페이스 계층

![ex_screenshot](./img/tcpudp.png)

## TCP/IP 패킷 정보

출발지 Port, 목적지 Port, 전송제어, 순서, 검증 정보

## TCP 특징

전송 제어 프로토콜(Transmission Control Protocol)

-   연결지향 - TCP 3way handshake(가상 연결)
-   데이터 전달 보증
-   순서 보장

-   신뢰성 있는 프로토콜
-   현재는 대부분 TCP 사용

## TCP 3 way handshake

![ex_screenshot](./img/tcphand.png)

## UDP 특징

사용자 데이터그램 프로토콜(User Datagram Protocol)

-   하얀 도화지에 비유(기능이 거의 없음)
-   연결지향 - TCP 3 way handshake X
-   데이터 전달 보증 X
-   순서 보장 X
-   데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
-   정리
    -   IP와 거의 같다. +PORT +체크섬 정도만 추가
    -   애플리케이션에서 추가 작업 필요
