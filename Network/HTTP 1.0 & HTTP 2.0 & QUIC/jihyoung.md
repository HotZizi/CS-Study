# HTTP 1.0 & HTTP 2.0 & QUIC

#### HTTP : Web상에서 클라이언트와 서버 간 통신을 위한 어플리케이션 계층 프로토콜

<br>

## TCP/UDP

전송 프로토콜인 TCP와 UDP에 대해 알아보자

<br>

### TCP
- 3 way handshake를 통해 신뢰성있는 connection을 수립한다.
  - 3 way handshake : 
    클라이언트와 서버가 상호간에 데이터를 주고 받을 준비가 되어있다는 합의를 하는 과정
- 3 way handshake를 통해 connection을 수립하면 클라이언트는 data를 전송하고 서버는 잘 받았다는 의미로 ack 패킷을 보낸다.
- 신뢰성 구축에 신경을 많이 쓴 프로토콜이다.


<br>


### UDP
받는 쪽에서 데이터를 제대로 받고 있는지조차 고려하지 않은 통신 프로토콜이다.

<br>

### 정리

||TCP|UDP|
|------|---|---|
|연결 방식|연결형 서비스|비연결형 서비스|
|패킷 교환|가상회선 방식|데이터 그램 방식|
|전송 순서 보장|보장함|보장하지않음|
|신뢰성|높음|낮음|
|전송 속도|느림|빠름|

<br>

## HTTP 
HTTP/0.9 ~ HTTP/2.0은 TCP를 사용

<br>

### HTTP/0.9
- 요청이 단일 라인
- 매우 간단한 프로토콜이지만 확장하기 어렵다.
- GET 메소드만 존재하고 응답은 헤더 없이 HTML 문서 형태 그 자체가 된다.

``` html
GET /mypage.html
```

```html
<HTML>
A very simple HTML page
</HTML>
```
<br>

### HTTP/1.0
- 헤더, 응답 메시지, 상태 코드, Content-Type이 생김
- html 이외의 다른 타입의 파일도 전송이 가능해짐
- 하나의 connection에서 1개의 요청과 1개의 응답만 처리할 수 있다.
- 여러 개의 리소스를 요청하기 위해서 여러 번의 connection을 생성하고 끊는 작업을 반복해야 했다.
    - 중복 connection 수립 과정으로 인한 레이턴시 발생 (성능 저하)
    - 서버 부하 비용 증가

<br>

```html
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)
```

```html
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

<br>

### HTTP/1.0의 Keep Alive 헤더

<br>

![](https://images.velog.io/images/hellojihyoung/post/6cab420d-977d-450c-b2b4-38b8fd86c70f/image.png)

tcp connection을 서버와 클라이언트가 한번만 사용하고 끊지 않고 연결을 계속 유지하겠다는 의미이다.

이를 통해 tcp connection 재활용이 가능하게 되었다.
- handshake 문제, 느린 연결 문제
  
하지만, HTTP/1.0의 표준이 아니므로 표준 벤더사마다 지원여부가 달랐다. (완벽한 해결방안이 아님)


<br>

### HTTP/1.1
- HTTP/1.0의 한계를 극복하기위해서 keep alive 헤더를 사용하지 않고 Persistent Connection, Pipelining 개념을 도입
- HTTP 메소드(PUT, Patch, options, delete 등) 추가
- 
<br>

### Persistent Connection
- 지정한 timeout 시간동안 connection을 닫지 않는 방식이다.
- 하나의 connection을 열어 두면, 여러 요청이 하나의 connection 안에서 이뤄진다.
- tcp connection을 재활용하는 이점을 가지고 3 way handshake 비용을 감소시켜 HTTP/1.0버전보다 네트워크 사용시간이 줄어들었다.

<br>

### Pipelining 
- HTTP의 특성상 서버는 클라이언트에게 받은 요청을 FIFO 방식으로 처리하여 (순서대로 응답하여) 대기 시간이 길어지는 단점이 생긴다. 이를 해결하기 위해 Pipelining 개념이 도입되었다.
- 클라이언트에게서 받은 요청 순서대로 서버가 응답한다.
(AB 순서로 요청을 보냈을 때, B의 작업이 먼저 완료되어도 응답 순서를 지키기위해 A의 작업이 끝나기 전까지 B의 작업을 응답할 수 없다.)

- 문제점
  - 1번째 요청에 대한 처리 시간이 매우 길어지면 2,3번째 요청은 대기해야한다.
- 주고 받는 데이터의 크기가 불필요하게 커졌다.

<br>

### HTTP/2.0
기존 HTTP/1.X 버전의 성능 향상에 초점을 맞춘 프로토콜이다.

표준의 대체가 아닌 확장 개념이다.

2015년도에 등장하여 네이버, 페이스북, 인스타그램에서 사용하는 프로토콜이다.

<br>

- 어플리케이션 계층에서 바이너리 프레이밍 계층이 생김
    - 메시지를 frame 단위로 2개 분할
    - 이 2개의 frame을 바이너리로 인코딩하여
    - 데이터 파싱, 전송속도 향상 및 오류 발생 가능성이 줄어들게 되었다.
- 클라이언트와 서버의 connection 속에 stream (데이터 양방향 흐름) 안에 frame들로 이뤄진 요청, 응답 메시지가 전송
- 데이터가 frame 단위로 쪼개져 메시지간의 순서가 사라지게 되었다.
  - 먼저 도착한 frame부터 조립되어 요청과 응답의 순서가 무의미해졌다
  - 이를 통해 Head of Line Blocking 문제가 해결되었다.
-  먼저 전송하고 싶은 stream에 가중치를 두어 리소스의 전송 우선순위를 설정
-  클라이언트가 요청하지 않은 파일을 알아서 서버가 응답
-  헤더의 크기를 줄여 페이지 로드 시간이 감소


<br>



<br>


<br>

## QUIC
구글에서 만든 전송 계층 프로토콜로 udp를 기반으로 한다.

<br>

### UDP 선택 이유
tcp는 신뢰성을 확보하지만, 기능이나 구조가 이미 가득 차있기에, 그 상태에서 발생하는 지연을 줄이기 힘든 구조이기 때문이다.

udp는 tcp에 비해 별도 기능이 없기 때문에 개발자가 원하는 기능을 구현할 여지가 충분하다. 
이를 바탕으로 tcp의 지연을 줄이면서 신뢰성을 확보하는 quic 프로토콜을 만들게 되었다. 

<br>

### QUIC의 이점
1. 데이터 전송 속도 향상
   
    첫 연결 설정에서 필요한 정보와 함께 데이터를 같이 전송

    -> 성공하면 설정을 캐싱하여 다음 연결 시 handshake 없이 바로 데이터 전송
    - 클라이언트가 Connection UUID를 가지고 있으면 connection을 재수립할 필요가 없어진다.
    - 
##### Handshake : 통신의 양측간 조건을 합의해 가는 정보 교환 과정

  <br>

2. 보안 측면 강화
- TLS : 데이터 암호화 프로토콜이 기본적으로 적용   
- Source Address Token 을 필요에 따라 발급 : IP Spoofing / Replay Attack을 방지

<br>

3. 향상된 Multiplexing
   
   <br>

   ![](https://images.velog.io/images/hellojihyoung/post/d8e5478b-7def-4a04-b9d9-b8cab3a84e5d/image.png)
   
- tcp 를 이용한 http/2.0 stream은 하나의 tcp chain에서 데이터들이 엮인 상태에서 전송이 된다
- quic을 이용한 http/3.0 stream은 하나의 connection 안의 독립 stream으로 인해 Multiplexing이 향상되었다.
  
    - 하나의 stream에서 병목현상이 생기더라도 문제가 발생한 stream만 멈추고 다른 stream에 영향을 미치지 않는다.

    - 이를 통해 head of line blocking 문제를 해결하고 레이턴시를 줄여 성능향상을 이뤄내었다.
  
<br>

## HTTP/3.0
2018년 10월에 quic 프로토콜을 바탕으로 한 HTTP/3.0 버전이 나왔다.
구글, 유투브는 이미 사용중이다.

<br>