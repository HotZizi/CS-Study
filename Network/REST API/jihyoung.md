# REST API

## REST란?

<br>

### REST의 정의
- *Representational State Transfer* 의 약자
- `자원`을 이름(자원의 표현)으로 구분하여 해당 자원의 `상태`(정보)를 주고 받는 모든 것을 의미한다.

**HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.**

<br>

### REST의 요소
1. Method

    | Method | 의미   | Idempotent |
    | ------ | ------ | ---------- |
    | POST   | Create | No         |
    | GET    | Select | Yes        |
    | PUT    | Update | Yes        |
    | DELETE | Delete | Yes        |

    > Idempotent : 한 번 수행하냐, 여러 번 수행했을 때 결과가 같나?

<br>

2. Resource
   - http://myweb/users와 같은 URI
   - 모든 것을 Resource (명사)로 표현하고, 세부 Resource에는 id를 붙인다.
  
<br>

3. Message
    * Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
    * 메시지 포맷이 존재

      : JSON, XML 과 같은 형태가 있음 (최근에는 JSON 
      을 씀)
    
      ```text
      HTTP POST, http://myweb/users/
      {
      	"users" : {
      		"name" : "terry"
      	}
      }
      ```
<br>

### REST의 장단점

#### 장점
- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.  
- 서버와 클라이언트의 역할을 명확하게 분리한다.

<br>

#### 단점
- 표준이 존재하지 않는다.
- REST API가 분산환경에 적합하지 않다.(멱등성을 보장하기 힘들기 때문)
  - 멱등성: 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질
- 사용할 수 있는 메소드가 4가지 밖에 없다.
  - HTTP Method 형태가 제한적이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴진다.
- 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
  - PUT, DELETE를 사용하지 못하는 점
  - pushState를 지원하지 않는 점

<br>

### REST 특징
1. Server-Client(서버-클라이언트 구조)

- 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
    - REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
   - Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
- 서로 간 의존성이 줄어든다.
  
  <br>

2. Stateless(무상태)
   
- HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
- Client의 context를 Server에 저장하지 않는다.
    - 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
- Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
    - 각 API 서버는 Client의 요청만을 단순 처리한다.
    - 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
    - 물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
    - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

<br>

3. Cacheable(캐시 처리 가능)
   
- 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
    - 즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
    - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
- 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
- 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.

<br>

4. Layered System(계층화)
- Client는 REST API Server만 호출한다.
- REST Server는 다중 계층으로 구성될 수 있다.
    - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
    - 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
- PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.

<br>

5. Uniform Interface(인터페이스 일관성)
   
- URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
특정 언어나 기술에 종속되지 않는다.

<br>

6. Resource 지향 아키텍쳐 (ROA : Resource Oriented Architecture)

- Resource 기반의 복수형 명사 형태의 정의를 권장.

<br>

7. Code-On-Demand(optional)

- Server로부터 스크립트를 받아서 Client에서 실행한다.
- 반드시 충족할 필요는 없다.

<br>

### REST API란?
- REST 기반으로 서비스 API를 구현하는 것


<br>

### REST API의 특징
- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
- REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.

<br>

## RESTful이란?
RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어

- REST를 REST답게 쓰기 위한 방법으로, REST 원리를 따르는 시스템을 RESTful 이란 용어로 지칭
- RESTful의 목적은 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.


#### Reference https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html, https://gyoogle.dev/blog/web-knowledge/REST%20API.html