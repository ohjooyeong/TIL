# Q. HTTP가 뭔지 설명해주세요.

[답변]

HTTP는 HyperText Transfer Protocol의 약자로 서버-클라이언트 모델을 따르면서 request/response구조로 웹 상에서 정보를 주고받을 수 있는 프로토콜입니다. TCP/IP 기반으로 작동하며, HTTP의 가장 큰 특징은 Connectionless와 Stateless입니다.

[TIP]

> 광범위한 질문이라 더 대답하기 어려울 수 있어요. 간혹 HTTP가 어떤 용어의 약자인지 물어보기도 하고, 구성요소를 묻기도 하고, 특징들을 물어보기도 합니다. HTTP는 웹개발자에게 특히 중요하기 때문에 기본적인 구조와 특징은 꼭 알아두시기 바랍니다.

## HTTP

HTTP는 HyperText Transfer Protocol의 약자로 웹 상에서 정보를 전송하기 위한 통신 프로토콜로써 HTML과 같은 문서를 전송하는 것에 사용됩니다.

클라이언트가 HTTP request를 서버에 보내면 서버는 HTTP response를 클라이언트에 보내는 구조입니다. request message는 start line(method, path, HTTP version), headers, body로 이루어져 있고 response message는 status line(HTTP version, status code, status message), headers, body로 이루어져 있습니다.

HTTP는 서버에 연결 후 요청에 응답을 받으면 연결을 끊어버리는 Connectionless 특성을 갖습니다. 이로 인해 많은 사람이 웹을 이용하더라도 실제 동시 접속을 최소화하여 더 많은 유저의 요청을 처리할 수 있습니다. 하지만 연결을 끊었기 때문에, 클라이언트의 이전 상태(로그인 유무 등)를 알 수가 없다는 Stateless특성이 생기게 됩니다. 정보를 유지할 수 없는 Connectionless, Stateless 특성을 가진 HTTP의 단점을 해결하기 위해 cookie, session, jwt 등이 도입되었습니다.

또한 HTTP는 정보를 text 형식으로 주고받기 때문에 중간에 인터셉트할 경우 데이터 유출이 발생할 수 있는 문제가 있어, HTTP에 암호화를 추가한 프로토콜이 바로 HTTPS입니다.
