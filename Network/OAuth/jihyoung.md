# OAuth

### OAuth란?
OAuth는 Open Authorization, Open Authentication을 뜻하는 것으로, 인터넷 사용자들이 비밀번호를 제공하지 않고, 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수있는 개방형 표준 방법 

: 자신의 애플리케이션에서 사용자 인증을 하기 위해 다른 애플리케이션의 사용자 인증방식을 하도록 `인가`하는 것

##### 인증 : 식별가능한 정보로 서비스에 등록된 사용자의 신원을 입증하는 절차 
##### 인가 : 사용자가 요청하는 요청을 실행할 수 있는 권한 여부를 확인하는 절차

<br>


이러한 매커니즘은 구글, 페이스북, 트위터 등이 사용하고 있으며 타사 애플리케이션 및 웹사이트의 계정에 대한 정보를 공유할 수 있도록 허용해준다.

: 구글, 페이스북에서 이미 사용자 인증을 수행했기 때문에 나의 애플리케이션에서는 그 회사로부터 로그인 권한을 부여 받기만 하면 되는 것


<br>

### 사용 용어

- **Client** : Resource를 직접 사용하는 사용자
- **Resource owner** : OAuth를 사용하는 사용자 / 일반 어플리케이션 ex) 왓챠
- **Authorization Server** : OAuth 인증 서버
- **Resource Server** : Rest API Server / 사용자 인증이 잘 되어 있는 애플리케이션 ex) 페이스북, 구글 ...
- **Access Token** : 인증 후에 사용자가 서비스 제공자가 아닌 소비자를 통해 보호 자원에 접근하기 위한 키 값
  
<br>


### 인증 과정

<br>

![image](https://user-images.githubusercontent.com/59171154/137711348-b1fc6b6d-69c6-4ac7-ae7b-7f8ba47611c8.png)

> 1. 왓챠에 접속
> 2. "페이스북으로 회원가입 하기" 버튼 클릭
> 3. 페이스북 로그인 창으로 이동 ( A)
> 4. 페이스북 로그인 성공 ( B )
> 5. "해당 사이트의 접근을 허용할 것인가?" 창이 생성
> 6. "허용"을 누르면( C ) 왓챠에서 로그인 목적으로 사용할 수 있는 토큰( Access token )을 페이스북이 발급 ( D )
> 7. 발급받은 토큰을 이용하여 만료기간까지 서비스를 사용 ( E, F ) 




OAuth 인증을 통해 애플리케이션 API를 유저 대신에 접근할 수 있는 권한을 얻을 수 있다.
OAuth가 사용되기 전에는 외부 사이트와 인증 기반의 데이터를 연동할 때 인증방식의 표준이 없었기 때문에, 기존의 기본인증인 아이디와 비밀번호를 사용하였다.
이는 유저의 비밀번호가 노출될 가망성이 크기 때문에 보안상 취약한 구조였다.
이를 보안하기 위해 OAuth의 인증은 API를 제공하는 서버에서 진행하고, 유저가 인증되었다는 Access Token을 발급한다.
발급된 Access token으로 타 애플리케이션에서는 API를 안전하고 쉽게 사용할 수 있다.





Reference : https://gdtbgl93.tistory.com/180, https://showerbugs.github.io/2017-11-16/OAuth-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C, https://cheese10yun.github.io/oauth2/
https://velog.io/@piecemaker/OAuth2-%EC%9D%B8%EC%A6%9D-%EB%B0%A9%EC%8B%9D%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90
https://interconnection.tistory.com/76