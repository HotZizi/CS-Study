# CORS

### 1. SOP 

다른 출처의 리소스를 사용하는것에 제한하느 보안 방식

**출처란?**  

<img src="https://user-images.githubusercontent.com/62633444/133958266-d4899a81-89b0-4040-a264-1c8c3b50608c.PNG" width="700" height="200"/>

-> protocol,host,port가 모두 같으면 같은 출처라고 판단함 (인터넷 익스플로러는 포트가 달라도 같은 출처로 판단함)

<br/>

### 2. 왜 SOP를 사용할까?

-> 해커가 사용자의 인증토큰을 가져와 서버에 요청을 할수도 있기때문에

**그러면 다른 출처의 리소스가 필요하다면 어떻게 할까?**

> CORS


<br/>

### 3. CORS란?


**Cross-Origin Resource Sharing**
- 다른 출처의 자원을 공유
- 추가 http 헤더를 이용하여 한 출처에서 실행중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제입니다.

<br/>

### 4. CORS 접근제어 시나리오 (CORS 요청)

- **Preflight 요청**

<img src="https://user-images.githubusercontent.com/62633444/133958884-1b48a8bf-6af5-48e6-90d7-0ac6815bad70.jpeg" width="700" height="300"/>
<br/>

1. OPTIONS 메서드를 통해 다른 도메인의 리소스에 요청이 가능한지 확인 작업
2. 요청이 가능하다면 실제 요청을 보낸다


<img src="https://user-images.githubusercontent.com/62633444/133958985-fa8c2b4f-7e62-4678-87c4-fbe2c87cc08b.jpeg" width="600" height="300"/>
<img src="https://user-images.githubusercontent.com/62633444/133959192-12a3da61-ea96-4669-81fe-d50de9f30d66.jpeg" width="600" height="300"/>
<br/>

- **Simple Request**

Prefilight 요청없이 바로 요청을 날린다.
다음 조건을 만족해야한다..
1. get,post,head 메서드중 하나
2. content-type이 application/x-www-form-urlencoded,multipart/form-data,text/plain 중 하나
3. 헤더는 accept,accept-language,content-language,content-type만 허용

<br/>
<img src="https://user-images.githubusercontent.com/62633444/133959500-3ac033ab-1053-478b-ac5c-7981a0b763d6.jpeg" width="500" height="300"/>
<br/>

**왜 preflight가 필요할까?**
-> CORS를 모르는 서버를 위해서다.

preflight가 없을 경우) 
<br/>
<img src="https://user-images.githubusercontent.com/62633444/133959804-5368e959-e24a-45c9-a5ee-34c45c07d9ab.jpeg" width="600" height="300"/>
<br/><br/>

preflight가 있을 경우)
<br/>
<img src="https://user-images.githubusercontent.com/62633444/133959950-f8a37431-920e-4b21-ad15-ca14f6e3604e.jpeg" width="600" height="300"/>
<br/><br/>


- **Credentialed Request**

인증 관련 헤더를 포함할 때 사용하는 요청이다.  

클라이언트 측)
credentials : include

서버 측)
Access-Control-Allow-Credentials : true
(Access-Control-Allow-Origin: * 은 안된다.)

### 5. 해결방안
Access-Control-Allow-Origin 세팅, Proxy 서버 사용 등등


