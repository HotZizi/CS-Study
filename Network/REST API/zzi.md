# REST API

## 1. REST
### REST란?  
REpresentataional 표현
State 상태
Transfer 전달 의 약자

> **자원**을 이름(자원의 표현)으로 구분하여 해당 **자원의 상태(정보)를 주고 받는** 모든 것을 의미한다.

**즉 REST란**  
HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
HTTP Method(POST, GET, PUT, DELETE)를 통해
해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.
 

> CRUD Operation이란
> CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create(생성), Read(읽기), Update(갱신), Delete(삭제)를 묶어서 일컫는 말로 
> REST에서의 CRUD Operation 동작 예시는 다음과 같다.

### REST 구성요소

- 자원(Resource) : HTTP URI

- 자원에 대한 행위(Verb) : HTTP Method

- 자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load

### REST의 특징

- **Uniform Interface (유니폼 인터페이스)**  
HTTP 표준만 따른다면 어떤 언어 혹은 어떤 플랫폼에서 사용하여도 사용이 가능한 인터페이스 스타일이다.
안드로이드 플랫폼, IOS 플랫폼 등 특정 언어나 플랫폼에 종속되지 않고 사용이 가능하다.
- **Stateless (상태 정보 유지 안함)**   
Rest는 상태 정보를 유지하지 않는다.
서버는 각각의 요청을 완전히 다른 것으로 인식하고 처리를 한다.
이전 요청이 다음 요청 처리에 연관이 되면 안된다.
- **Cacheable (캐시 가능)**  
HTTP의 기존 웹 표준을 그대로 사용하기 때문에 HTTP가 가진 캐싱 기능 적용이 가능하다.  
- **Self-descriptiveness (자체 표현 구조)**  
Rest API 메시지만 보고도 쉽게 이해할 수 있는 자체 표현 구조로 되어있다.
- **Client-Server**    
Rest 서버는 API 제공을 하고 클라이언트는 사용자 인증에 관련된 일들을 직접 관리한다.
자원이 있는 쪽을 Server라고 하고 자원을 요청하는 쪽이 Client가 된다.
서로간의 의존성이 줄어들기 때문에 역할이 확실하게 구분되어 개발해야할 내용들이 명확해진다.
- **Layerd System (계층화)**  
클라이언트는 Rest API 서버만 호출한다.
Rest 서버는 다중 계층으로 구성될수 있으면 로드 밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의
유연성을 둘 수 있다.

## 2. REST API

### REST API란?
RESPT API란 REST의 원리를 따르는 API를 의미합니다.

### REST API 설계규칙
- **URI는 정보의 자원을 표현해야한다.**  
자원의 이름은 동사보다는 **명사**를 사용한다.
URI는 자원을 표현하는데 중점을 두어야 하기 때문에 행위에 대한 표현이 들어가면 안된다.
(URI에 HTTP METHOD와 행위에대한 동사 표현이 들어가면 안된다.)
GET /users/321
- **자원에 대한 행위는 HTTP METHOD로 표현한다. (GET, POST, PUT DELETE)**  
URI에 자원의 행위에 대한 표현이 들어가지 않는 대신 HTTP METHOD를 통해 대신한다.
GET /users/321 321 ID를 가진 유저 정보를 가져오기
DELETE /users/321 321 ID를 가진 유저 정보를 삭제하기
POST /users 유저를 생성하기
- **슬래시 (/)는 계층 관계를 나타내는데 사용한다.**  
http://restapi.test.com/users/rooms
http://restapi.test.com/users/board
- **URI 마지막은 슬래시(/)를 사용하면 안된다.**  
http://restapi.test.com/users/rooms/ [X]
http://restapi.test.com/users/rooms  [O]
- **하이픈 (-)은 URI의 가독성을 높이는데 사용한다.**  
불가피하게 긴 URI를 사용하게 될 경우 하이픈을 이용하여 가독성을 높인다.
언더바 혹은 밑줄은 URI에 사용하지 않는다.
밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 한다.
그래서 대신 언더바를 사용하지 않고 하이픈을 이용한다.
- **URI는 경로에는 소문자가 적합하다.**  
URI 경로에는 대문자 사용을 피해야한다.
대소문자에 따라 각자 다른 리소스로 인식하기 때문이다.
RFC3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이다.
- **파일 확장자는 URI에 포함하지 않는다.**  
REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
Accept header를 사용한다.

### REST 장단점  


**장점**
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- 서버와 클라이언트의 명확한 구분이 가능하다.


**단점**
- HTTP Method 형태가 제한적이다.
- 표준이 자체가 존재하지 않아 정의가 필요하다.

## 3.RESTFUL API

### RESTFUL API란?
RESTFUL이란 REST의 원리를 따르는 시스템을 의미한다.
하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아니다.  
REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며
모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있다.


