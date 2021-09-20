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

### 4. CORS 접근제어 시나리오

- **Preflight 요청**

<img src="https://user-images.githubusercontent.com/62633444/133958884-1b48a8bf-6af5-48e6-90d7-0ac6815bad70.jpeg" width="700" height="300"/>
<br/>

1. OPTIONS 메서드를 통해 다른 도메인의 리소스에 요청이 가능한지 확인 작업
2. 요청이 가능하다면 실제 요청을 보낸다


<img src="https://user-images.githubusercontent.com/62633444/133958985-fa8c2b4f-7e62-4678-87c4-fbe2c87cc08b.jpeg" width="600" height="300"/>
<img src="https://user-images.githubusercontent.com/62633444/133959192-12a3da61-ea96-4669-81fe-d50de9f30d66.jpeg" width="600" height="300"/>
<br/>




