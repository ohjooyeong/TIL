# Q. 3-way handshake는 무엇이고 각 과정은 어떻게 되나요?

[답변]

3-way handshake는 TCP/IP 프로토콜로 통신하기 전, 정확한 정보 전송을 위해 상대방 컴퓨터와 세션을 수립하는(연결을 하는) 과정입니다. (TCP연결 초기화)

클라이언트가 서버에게 접속을 요청하는 SYN 패킷을 보내면, 서버는 요청을 수락하는 ACK를 포함하여 SYN+ACK 패킷을 클라이언트에게 발송합니다. 클라이언트가 이것을 수신한 후, 다시 ACK를 서버에게 발송하면 연결이 이루어지고, 이로써 데이터를 주고 받을 수 있게 됩니다.

[TIP]

> 자주 나오진 않지만 아주 기초적인 네트워크 지식이기 때문에 꼭 알고 넘어가야 하는 내용입니다.<br>
> HTTP 1.1과 2.0 버전은 모두 TCP 프로토콜을 사용합니다. 그래서 우리가 네이버에 접속할 때마다 네이버의 서버와 나의 노트북이 3-way handshake를 하면서 서로를 확인하게 됩니다.<br>
> 면접에서는 3-way handshake를 하는 목적은 무엇인지, 각 step의 절차는 어떻게 되는지를 중점적으로 보시면됩니다. 4-way handshake는 가벼운 마음으로 읽어보시면 충분합니다.

## TCP 3 way handshake

TCP 통신은 아래와 같은 3단계의 과정을 거칩니다.

1. Connection setup (tcp 연결 초기화) - 3way handshaking
2. Data transfer (데이터 전송)
3. Connection termination (tcp 연결 종료) - 4way handshaking

우리가 공부한 3-way handshaking이 바로 Connection setup의 과정입니다.

## 4way handshaking

3-way handshake를 통해 Connection setup을 했다면 tcp연결을 종료하는 Connection termination 과정은 4-way handshaking을 통해 이루어집니다.

TCP connection termaination은 양방향으로 2개의 연결이 독립적으로 닫히기 때문에 4-way 단계를 밟게 됩니다.

1. Client process에서 active close를 하면, client tcp에서 FIN세그먼트를 보냅니다.
2. Server는 FIN 세그먼트를 받았다는 응답에 대한 ACK를 client로 보냅니다. 이때, server내의 process에게 EOF를 보내지만, 아직 process는 close되지 않을 수 있습니다.
3. Server process로부터 passive close를 받으면 server tcp에서 FIN 세그먼트를 client TCP에게 보냅니다.
4. Server tcp가 ACK를 받게 되면 연결이 종료됩니다.

### Q. 그럼 4-way handshake는 뭔가요?

[답변]

3-way handshake를 통해 Connection setup을 했다면 tcp연결을 종료하는 Connection termination 과정은 4-way handshaking을 통해 이루어집니다.

TCP connection termination은 양방향으로 2개의 연결이 독립적으로 닫히기 때문에 4-way 단계를 밟게 됩니다.
