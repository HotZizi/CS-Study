> HTTP  : 웹상에서 클라이언트와 서버 간 통신을 위한 프로토콜

### TCP/UDP

||TCP|UDP|
|------|---|---|
|연결 방식|연결형 서비스|비연결형 서비스|
|패킷 교환|가상회선 방식|데이터 그램 방식|
|전송 순서 보장|보장함|보장하지않음|
|신뢰성|높음|낮음|
|전송 속도|느림|빠름|

### HTTP

HTTP/0.9 ~ HTTP/2.0은 TCP를 사용한다.

#### HTTP/0.9
- HTTP 0.9는 요청이 단일 라인(one line)
- 메소드는 GET만 있었으며 응답은 헤더 없이 HTML 문서 형태 그 자체

```
GET /mypage.html
```

```
<HTML>
A very simple HTML page
</HTML>
```

#### HTTP/1.0

 - 버전 정보, 상태 코드, 헤더가 생김
 - 헤더와 POST 메소드 도입 => HTML 파일 외에 이미지, 비디오, 단순 텍스트 등을 전송 가능
 
```
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)
```

```
200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML> 
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
(connection closed)
```

- 단점 : 하나의 connection에서 1개의 요청과 1개의 응답만 처리할 수 있음 

**이게 왜 단점 일까?** 
> 예를 들어 클라이언트가 어떤 HTML 문서를 요청했는데 그 페이지 안에 img 파일이 10개, css 5 파일, js 5 파일 도합 20파일이 있다면 커넥션 20개를 다 따로 맺어서 파일을 받아야 하는 것이다.
HTTP는 TCP/IP 기반 통신 프로토콜인데, TCP는 연결을 맺을 때 3-way 핸드쉐이킹을 하고 시작을 한다. HTTP/1.0은 파일이 20개일 때 이걸 20번을 해야 된다는 얘기다.

#### HTTP/1.1
- HTTP의 한계를 극복하기 위해 만들어짐
- HTTP 메소드(PUT, Patch, options, delete 등)가 추가
- Persistent Connection, Pipelining 

![](https://images.velog.io/images/zzi99/post/de1f843f-22ed-472c-985c-2941f594462e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-26%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.31.07.png)

**Persistent Connection 란?**
> 지정한 timeout 시간동안 connection을 닫지 않는 방식
하나의 connection을 열어 두면, 여러 요청이 하나의 connection 안에서 이뤄짐
tcp connection을 재활용하는 이점을 가지고 3 way handshake 비용을 감소시켜 HTTP/1.0버전보다 네트워크 사용시간이 줄어들었다.

![](https://images.velog.io/images/zzi99/post/74b3edb0-84d5-48b8-8f24-9ef6cd36bb4c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-26%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.30.18.png)
**Pipelining 란?**
> 하나의 커넥션에서 응답을 기다리지않고 여러요청을 순차적으로 보내 그 순서에 맞게 응답하는 방식으로 지연시간을 줄이는 방법

**Pipelining의 단점**
> 📌 Head of Line Blocking 문제점  
1번째 요청에 대한 처리 시간이 매우 길어지면 2,3번째 요청은 대기해야한다.  
📌 Header 구조의 중복 문제점  
주고 받는 데이터의 크기가 불필요하게 커졌다.

#### HTTP/2.0
- 어플리케이션 계층에서 바이너리 프레이밍 계층이 생김
  -  메시지를 frame 단위로 2개 분할
이 2개의 frame을 바이너리로 인코딩하여
데이터 파싱, 전송속도 향상 및 오류 발생 가능성이 줄어들게 되었다.
- 클라이언트와 서버의 connection 속에 stream (데이터 양방향 흐름) 안에 frame들로 이뤄진 요청, 응답 메시지가 전송
- 데이터가 frame 단위로 쪼개져 메시지간의 순서가 사라짐 (Head of Line Blocking 해결)
- 먼저 전송하고 싶은 stream에 가중치를 두어 리소스의 전송 우선순위를 설정가능
- 클라이언트가 요청하지 않은 파일을 알아서 서버가 응답
- 헤더의 크기를 줄여 페이지 로드 시간이 감소 (static dynamic table를 이용하여 Header 구조의 중복 해결)

### QUIC
구글에서 만든 전송 계층 프로토콜로 udp를 기반

**왜 UDP를 선택했을까?**
> tcp는 신뢰성을 확보하지만, 기능이나 구조가 이미 가득 차있기에, 그 상태에서 발생하는 지연을 줄이기 힘든 구조이다.
udp는 tcp에 비해 별도 기능이 없어서 개발자가 원하는 기능을 구현할 여지가 충분하다.
이를 바탕으로 **tcp의 지연을 줄이면서 신뢰성을 확보하는 quic 프로토콜을 만들게 되었다.**

- 보안 측면 강화 
  - TLS 👉 데이터 암호화 프로토콜이 기본적으로 적용   
  - Source Address Token 을 필요에 따라 발급 👉 IP Spoofing / Replay Attack을 방지
- 데이터 전송 속도 향상
  - 첫 connection 설정에서 필요한 정보와 함께 데이터를 같이 전송하여 connection 성공시, 설정을 캐싱하여 다음 connection때 handshake 없이 바로 데이터 전송이 가능해진다.
- 하나의 connection 안의 독립 stream으로 인해
  - 하나의 stream에서 병목현상이 생기더라도 문제가 발생한 stream만 멈추고 다른 stream에 영향을 미치지 않는다.

#### HTTP/3.0
2018년 10월에 quic 프로토콜을 바탕으로 한 HTTP/3.0 버전이 나왔다.
구글, 유투브는 이미 사용중이다.
