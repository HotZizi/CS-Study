# JWT

## 정의
JSON Web Token의 줄임말로, 필요한 모든 정보와 검증을 위한 Signature를 포함하는 JSON 객체를 통해 만들어내는 Token의 일종이다.
> JSON Web Tokens are an open, industry standard [RFC 7519]
method for representing claims securely between two parties.

<br>

## 구성 요소

JWT는 `.` 을 구분자로 3가지의 문자열로 구성되어 있다.

aaaa.bbbbb.ccccc 의 구조로 앞부터 헤더(header), 내용(payload), 서명(signature)로 구성된다.

<br>

![image](https://user-images.githubusercontent.com/59171154/135726617-96974506-66dc-4024-b4aa-1fad339170fd.png)


<br>

### 헤더(Header)

헤더는 typ와 alg 두가지의 정보를 지니고 있습니다.

- typ는 토큰의 타입을 지정
  - JWT이기에 "JWT"라는 값이 들어간다.

- alg : 해싱 알고리즘을 지정
  -  기본적으로 HMAC, SHA256, RSA가 사용되면 토큰을 검증 할 때 사용되는 signature부분에서 사용된다.

  <br>

### 내용(Payload)

- 토큰을 담을 정보를 담고 있다.
- 정보의 한 조각을 클레임(claim)이라고 부르고, 이는 name / value의 한 쌍으로 이뤄져있다. 
- 토큰에는 여러개의 클레임들을 넣을 수 있지만 너무 많아질경우 토큰의 길이가 길어질 수 있다.

  <br>

- 클레임에는 세 종류가 있다.
   1. 등록된(registered) 클레임
       - iss : 토큰 발급자 (issuer)
       - sub : 토큰 제목 (subject)
       - aud : 토큰 대상자 (audience)
       - exp : 토큰의 만료시간(expiration), 시간은 NumericDate 형식으로 되어있어야 하며 언제나 현재 시간보다 이후로 설정되어 있어야 함
       - nbf : Not before을 의미하며, 토큰의 활성 날짜와 비슷한 개념, NumericDate형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않음
       - iat : 토큰이 발급된 시간(issued at), 이 값을 사용하여 토큰의 age가 얼마나 되었는지 판단 가능
       - jti : JWT의 고유 식별자로서, 주로 중복적인 처리를 방지하기 위하여 사용, 일회용 토큰에 사용하면 유용

   2. 공개(public) 클레임  
   공개 클레임들은 충돌이 방지된(collision-resistant)이름을 가지고 있어야 한다. 충돌을 방지하기 위해서는, 클레임 이름을 URl형식으로 짓는다.
   3. 비공개(private) 클레임  
    클라이언트와 서버 사이 합의하에 사용되는 클레임 이름이다. 공개 클레임과는 달리 이름이 중복되어 충돌이 될 수 있으니 사용할때에 유의해야 한다.


  <br>


### 서명(Signature)
서명은 헤더의 인코딩값과 정보의 인코딩값을 합친후 주어진 비밀키로 해쉬를 하여 생성한다. 이렇게 만든 해쉬를 base64형태로 나타내게 된다.


<br>


### 최종 결과
> Encoded Header + "." + Encoded Payload + "." + Verify Signature


  <br>

Header, Payload는 인코딩될 뿐(16진수로 변경), 따로 암호화되지 않는다. 따라서 JWT 토큰에서 Header, Payload는 누구나 디코딩하여 확인할 수 있게 된다. 여기서 누구나 디코딩할 수 있다는 말은 Payload에는 유저의 중요한 정보(비밀번호)가 들어가면 쉽게 노출될 수 있다는 의미다.

하지만 Verify Signature는 SECRET KEY를 알지 못하면 복호화할 수 없다. 

A 사용자가 토큰을 조작하여 B 사용자의 데이터를 훔쳐보고 싶다고 가정해보자. 그래서 payload에 있던 A의 ID를 B의 ID로 바꿔서 다시 인코딩한 후 토큰을 서버로 보냈다. 그러면 서버는 처음에 암호화된 Verify Signature를 검사하게 된다. 여기서 Payload는 B사용자의 정보가 들어가 있으나 Verify Signature는 A의 Payload를 기반으로 암호화되었기 때문에 유효하지 않는 토큰으로 간주하게 됩니다. 여기서 A사용자는 SECRET KEY를 알지 못하는 이상 토큰을 조작할 수 없다는 걸 확인할 수 있습니다.

 <br>

### JWT 동작 과정
 
 <br>

![995EC2345B53368912](https://user-images.githubusercontent.com/59171154/135726975-28f97c0c-b2e1-4b7b-b694-626b6c3951a4.png)


1. 사용자가 로그인을 한다.
2. 서버에서는 계정정보를 읽어 사용자를 확인 후, 사용자의 고유한 ID값을 부여한 후, 기타 정보와 함께 Payload에 넣는다.
3. JWT 토큰의 유효기간을 설정한다.
4. 암호화할 SECRET KEY를 이용해 ACCESS TOKEN을 발급한다.
5. 사용자는 Access Token을 받아 저장한 후, 인증이 필요한 요청마다 토큰을 헤더에 실어 보낸다.
6. 서버에서는 해당 토큰의 Verify Signature를 SECRET KEY로 복호화한 후, 조작 여부, 유효기간을 확인한다.
7. 검증이 완료된다면, Payload를 디코딩하여 사용자의 ID에 맞는 데이터를 가져온다.

 <br>