# Q. URL을 주소창에 쳤을 때 화면이 나오기까지의 과정을 네트워크 관점으로 설명해주세요.

[답변]

1. 사용자가 브라우저에 URL 입력
2. 브라우저는 DNS를 통해 서버의 IP 주소를 찾는다
3. client에서 HTTP request 메시지 => TCP/IP 패킷 생성 => server로 전송
4. server에서 HTTP request에 대한 HTTP response 메시지 => TCP/IP 패킷 생성 => client로 전송
5. 도착한 HTTP response message는 웹 브라우저에 의해 출력(렌더링)

[TIP]

> 굉장히 자주 나오는 면접 질문중에 하나입니다. 이 질문을 통해서 면접관 입장에서는 지원자가 웹개발 전반적인 프로세스에 대해서 잘 이해하고 있는지를 다각적으로 판단할 수 있어서 좋습니다. 특히 해당 질문은 frontend 관점에서 집중적으로 물어볼 수 있고, backend 관점에서 깊에 물어볼 수 있습니다. 별다른 언급이 없다면 네트워크 관점에서 절차에 따라 설명하면 충분한 답변을 할 수 있습니다.<Br>
> HTTP protocol과 TCP protocol을 거쳐서 패킷이 되는 과정, request 메세지를 받은 서버에서는 HTTP response message를 구성하여 client로 전송하는 것 등을 절차에 맞게 순차적으로 설명하면 됩니다.

## 웹 동작 방식

1. 유저가 브라우저에서 www.google.com(URL)을 입력을 하면 HTTP request message를 생성합니다.
2. IP 주소를 알아야 전송을 할 수 있으므로, DNS lookup을 통해 해당 Domain의 server IP주소를 알아냅니다.
3. 반환된 IP주소(구글의 server IP)로 HTTP 요청 메시지(request message) 전송 요청을 합니다.
   1. 생성된 HTTP 요청 메시지를 TCP/IP층에 전달합니다.
   2. HTTP 요청 메시지에 헤더를 추가해서 TCP/IP 패킷을 생성합니다.
4. 해당 패킷은 전기신호로 랜선을 통해 네트워크로 전송되고, 목적지 IP에 도달합니다.
5. 구글 server에 도착한 패킷은 unpacking을 통해 message를 복원하고 server의 process로 보냅니다.
6. server의 process는 HTTP 요청 메시지에 대한 response data를 가지고 HTTP 응답 메시지 (response message)를 생성합니다.
7. HTTP 응답 메시지를 전달받은 방식 그대로 client IP로 전송을 합니다
8. HTTP response 메시지에 담긴 데이터를 토대로 웹브라우저에서 HTML 렌더링을 하여 모니터에 검색창이 보여집니다.
