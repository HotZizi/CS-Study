# 쿠키 세션 로컬스토리지 세션스토리지

1. 쿠키 VS 웹스토리지 비교
2. 쿠키 VS 세션 비교

## 1. 쿠키 vs 웹스토리지 

### 쿠키란?
- http는 비연결성, 무상태성 특징이 있기때문에 해결하기 위해 쿠키가 나옴
- 브라우저에 저장되는 작은 크기의 문자열 (최대 4KB)

#### Cookies 2가지 유형
- persistent cookies : 만료일을 포함하지 않고, 브라우저나 탭이 열려있는 동안에만 저장됩니다.
- session cookies :  만료일까지 유저의 디스크에 저장되고 만료일이 지나면 삭제됩니다.

#### 문제점? 
- CSRF 
- XSS
- 부족한 저장용량
- HTTP 요청시 자동으로 모든 쿠키를 전송
 
> CSRF 란?  
> 웹 어플리케이션 취약점 중 하나로 인터넷 사용자(희생자)가 자신의 의지와는 무관하게 공격자가 의도한 행위(수정, 삭제, 등록 등)를 특정 웹사이트에 요청하게 만드는 공격  
> 정상적인 request를 가로채 피해자인 척 하고 백엔드 서버에변조된 request를 보내 악의적인 동작을 수행하는 공격을 의미. (피해자 정보 수정, 정보 열람)

> XSS 란? 
> 공격자가 의도하는 악의적인 js 코드를 피해자 웹 브라우저에서 실행시키는 것  

### 웹스토리지란?
- 최대 5MB -> 쿠키의 부족한 저장용량 해결 
- 요청시 Headers에 전송하지않음 -> 쿠키의 CSRF, 트래픽 문제 해결
- 객체 정보 저장이 가능

||로컬 스토리지|세션 스토리지|
|---|---|---|
|저장범위|도메인/브라우저|도메인/브라우저/탭|
|삭제시기|직접 삭제|탭 종료시|
 

#### 문제점?
- 웹 스토리지 비활성화 설정 (시크릿 모드), 에러 처리 해야함
- HTML5를 지원하지 않는 브라우저의 경우 사용 불가
- XSS
- 만료기간 설정 불가
- 동기적으로 실행 -> 메인스레드를 블로킹함 => 용량이 크면 주의 ‼️ (IndexedDB 사용)

### 쿠키 & 웹스토리지 정리

=> 보안 문제가 있기 때문에 민감한 정보는 저장 x

- **쿠키** (기간 설정, 서버전송 해야하기 때문에 작은 용량)
ex) n일 동안 보지않기, 비로그인 장바구니

- **세션 스토리지** (탭 종료시 삭제되어도 괜찮은것)
ex) 이전 페이지 저장, 이전 스크롤 위치 저장

- **로컬 스토리지** (브라우저 종료시 유지)
ex ) 글 임시저장, 사용자 설정 저장 , 자동로그인 

사실 정해진 답은 없다, 예를 들면 ? 비로그인 장바구니를 쿠키에 넣어야한다는 사람도 있고, 세션스토리지에 넣어야한다는 사람도 있다.
나도 비로그인 장바구니는 장바구니에 많은 양을 담을 수도 없고, 서버 요청시 계속 전송이 된다는 점에서 세션스토리지에 넣어야한다고 생각했는데, 몇개의 쇼핑몰을 살펴보니 (쿠팡도..!) 탭이 삭제되어있어도 장바구니에 담겨져있는것을 확인했다.  
아마도 쿠키를 사용한것 같다..! 왜 쿠키에 넣었을까를 생각해보면, 사용자들이 소비를 더 이끌수 있지 않나싶다... 아무래도 계속 넣어져있으니까?

저번에 JWT 공부를 했을때 토큰을 어디에 저장해야할지 궁금했었다.  
이번에 공부한 것과 + [이글을 참고](https://velog.io/@0307kwon/JWT%EB%8A%94-%EC%96%B4%EB%94%94%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%B4%EC%95%BC%ED%95%A0%EA%B9%8C-localStorage-vs-cookie )해서 정리해본결과.. 는 XSS, CSRF를 잘몰라서 이것 보고 난 후에 다시 생각해보자!!


## 2. 쿠키 vs 세션

###  세션이란?

- 세션은 쿠키를 기반으로 하고 있지만, 사용자 정보 파일을 브라우저에 저장하는 쿠키와 달리 세션은 서버 측에서 관리.

### 쿠키 프로세스
1. 클라이언트가 페이지를 요청
2. 서버에서 쿠키를 생성
3. HTTP 헤더에 쿠키를 포함 시켜 응답
4. 브라우저가 종료되어도 쿠키 만료 기간이 있다면 클라이언트에서 보관하고 있음
5. 같은 요청을 할 경우 HTTP 헤더에 쿠키를 함께 보냄
6. 서버에서 쿠키를 읽어 이전 상태 정보를 변경 할 필요가 있을 때 쿠키를 업데이트 하여 변경된 쿠키를 HTTP 헤더에 포함시켜 응답


### 세션 프로세스

1. 클라이언트가 서버에 접속 시 세션 ID를 발급 받음
2. 클라이언트는 세션 ID에 대해 쿠키를 사용해서 저장하고 가지고 있음
3. 클라리언트는 서버에 요청할 때, 이 쿠키의 세션 ID를 같이 서버에 전달해서 요청
4. 서버는 세션 ID를 전달 받아서 별다른 작업없이 세션 ID로 세션에 있는 클라언트 정보를 가져와서 사용
5. 클라이언트 정보를 가지고 서버 요청을 처리하여 클라이언트에게 응답
ex) 로그인 정보 유지  

### 문제점? 
- 세션은 서버의 자원을 사용하기 때문에 무분별하게 만들다보면 서버의 메모리가 감당할 수 없어질 수가 있고 속도가 느려질 수 있다.

### 쿠키와 세션 비교
||쿠키|세션|
|---|---|---|
|저장위치|클라이언트에 파일로 저장|서버에 저장|
|보안|클라이언트 로컬에 저장되기 떄문에 변질되거나 request에서 스나이핑당할 우려가 있어서 보안 취약|쿠키를 이용해서 세션id만 저장하고 그것으로 구분해서 서버에서 처리하기 떄문에 비교적 안전 (보안 면에서 쿠키보다 우수)|
|라이프사이클| 만료시간은 있지만 파일로 저장되기 떄문에 브라우저를 종료해도 계속해서 정보가 남아 있을수 있음.|만료기간을 정할수는 있지만 브라우저가 종료되면 그 에 상관없이 삭제됨|




