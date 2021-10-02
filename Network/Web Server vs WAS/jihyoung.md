# Web Server vs WAS

<<<<<<< HEAD
=======
<br>

>>>>>>> c76187be8402a6461ed7ae9d12e85a411ede9b03
## 정적 페이지와 동적 페이지

<img src="https://gmlwjd9405.github.io/images/web/static-vs-dynamic.png">

<br>

### 정적 페이지 (Static Pages)
- 바뀌지 않는 페이지
- 항상 동일한 페이지를 반환
   - image, html, css, javascript 파일과 같이 컴퓨터에 저장된 파일들

<br>

### 동적 페이지 (Dynamic Pages)
- 인자에 따라 바뀌는 페이지
- 인자의 내용에 맞게 동적인 contents를 반환
     - 서버에 저장된 데이터 변경에 따라 contents 변환
- 웹 서버에 의해 실행되는 프로그램을 통해 만들어진 결과물

<br>

## Web Server와 WAS

<<<<<<< HEAD
=======
<br>
>>>>>>> c76187be8402a6461ed7ae9d12e85a411ede9b03

<img src="https://gmlwjd9405.github.io/images/web/webserver-vs-was1.png">

<br>

### Web Server
#### 1. 개념
- 하드웨어 : Web 서버가 설치되어 있는 컴퓨터
- 소프트웨어 : 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 `정적인 컨텐츠`(.html .jpeg .css 등)` 를 제공하는 컴퓨터 프로그램

<br>
  
#### 2. 기능
- Http 프로토콜을 기반으로, 클라이언트의 요청을 서비스하는 기능을 담당
   -  정적 컨텐츠 제공
      -  WAS를 거치지 않고 바로 자원 제공
   -  동적 컨텐츠 제공을 위한 요청 전달
      -  클라이언트의 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)한다.

<br>
 
#### 3. 예시
Apache Server, Nginx, IIS(Windows 전용 Web 서버) 등

<br>
 
### WAS
#### 1. 개념
- Web Application Server의 약자
- DB 조회 및 다양한 로직 처리 요구시 `동적인 컨텐츠`를 제공하기 위해 만들어진 애플리케이션 서버
- HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)
- "웹 컨테이너(Web Container)" 혹은 "서블릿 컨테이너(Servlet Container)" 라고도 불린다.
   - Container란 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 말한다.

즉, WAS는 JSP, Servlet 구동 환경을 제공한다.

<br>
 

#### 2. 역할 및 기능

> WAS = Web Server + Web Container

- 역할
  - Web Server 기능들을 구조적으로 분리하여 처리하고자하는 목적으로 제시되었다.
    - 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용된다.
    - 주로 DB 서버와 같이 수행된다.
- 기능
  - 프로그램 실행 환경 및 DB 접속 기능 제공
  -  여러 트랜잭션 관리 기능
  -  업무 처리하는 비즈니스 로직 수행

<br>
 
#### 3. 예시
Tomcat, JBoss, Jeus, Web Sphere 등

<br>

## Web Server와 WAS를 구분하는 이유
<br>

![image](https://user-images.githubusercontent.com/59171154/135722059-b5f3474d-a790-45f5-983b-cd149d287289.png)

<br>

### Web Server가 필요한 이유

> Web Server에서는 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담을 줄일 수 있다.

클라이언트(웹 브라우저)에 이미지 파일(정적 컨텐츠)을 보내는 과정을 생각해보자.  
이미지 파일과 같은 정적인 파일들은 웹 문서(HTML 문서)가 클라이언트로 보내질 때 함께 가는 것이 아니다.  
클라이언트는 HTML 문서를 먼저 받고 그에 맞게 필요한 이미지 파일들을 다시 서버로 요청하면 그때서야 이미지 파일을 받아온다.  
Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고 앞단에서 빠르게 보내줄 수 있다.

<br>

### WAS가 필요한 이유
> 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때 그때 결과를 만들어서 제공함으로써 자원을 효율적으로 사용할 수 있다.

웹 페이지는 정적 컨텐츠와 동적 컨텐츠가 모두 존재한다.  
따라서 사용자의 요청에 맞게 적절한 동적 컨텐츠를 만들어서 제공해야 한다.  
이때, Web Server만을 이용한다면 사용자가 원하는 요청에 대한 결과값을 모두 미리 만들어 놓고 서비스를 해야 한다.  
하지만 이렇게 수행하기에는 자원이 절대적으로 부족하다.


<br>

### 효율적인 방법
결론적으로 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성 을 위해 Web Server와 WAS를 분리한다.  Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인 형태로 설정하여 분산 처리를 할 수 있도록 한다.

<<<<<<< HEAD
=======
<br>

>>>>>>> c76187be8402a6461ed7ae9d12e85a411ede9b03
<img src="https://gmlwjd9405.github.io/images/web/web-service-architecture.png">


<br>
<br>

참조 
- https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html
<<<<<<< HEAD
- https://www.youtube.com/watch?v=NyhbNtOq0Bc
=======
- https://www.youtube.com/watch?v=NyhbNtOq0Bc
>>>>>>> c76187be8402a6461ed7ae9d12e85a411ede9b03
