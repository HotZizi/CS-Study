# 정규화(Normalization)

<br>

### 정규화란?

관계형 데이터베이스의 설계에서 `중복을 최소화`하게 데이터를 구조화하는 프로세스를 정규화라고 한다. 데이터베이스 정규화의 목표는 이상이 있는 관계를 재구성하여 작고 잘 조직된 관계를 생성하는 것에 있다. 중복을 줄여 무결성을 유지할 수 있고, DB 저장 용량 또한 효율적으로 관리가 가능하다.



<br>

### 목적

- 데이터의 중복을 없애면서 불필요한 데이터를 최소화시킨다.
  - 테이블 간에 FK(외래키)로 PK(기본키)를 연결해 사용하면 디스크 공간을 훨씬 효율적으로 사용 가능
- 무결성을 지키고, 이상 현상을 방지한다.
  - 삽입 이상 : 튜플 삽입시 지정하지 않은 속성값이 NULL을 갖거나, 원하지 않는 자료가 삽입되는 현상
  - 삭제 이상 : 튜플 삭제시 연쇄 삭제가 발생하는 현상
  - 갱신 이상 : 데이터 갱신시 일관성 유지가 안되는 현상 
- 테이블 구성을 논리적이고 직관적으로 할 수 있다.
- 데이터베이스 구조를 확장에 용이해진다.

<br>

### 정규화 과정

<br>

![](https://images.velog.io/images/hellojihyoung/post/72f806bb-d667-4264-88f2-0fd713b6fbe2/image.png)

정규화에는 여러가지 단계가 있지만, 대체적으로 1~3단계 정규화까지의 과정을 거친다.

<br>

### 제 1정규화(1NF)

테이블 컬럼이 원자값(하나의 값)을 갖도록 테이블을 분리시키는 것을 말한다.

만족해야 할 조건은 아래와 같다.

- 어떤 릴레이션에 속한 모든 도메인이 원자값만으로 되어 있어야한다.
- 모든 속성에 반복되는 그룹이 나타나지 않는다.
- 기본키를 사용하여 관련 데이터의 각 집합을 고유하게 식별할 수 있어야 한다.

<br>

![](https://images.velog.io/images/hellojihyoung/post/cc17e71b-47e6-478b-9772-d8e0ab59cd08/1.PNG)

<br>

위의 테이블은 전화번호를 여러개 가지고 있어 원자값이 아니다. (1을 만족하지 못함)

<br>

![](https://images.velog.io/images/hellojihyoung/post/b6113768-fa8c-4fe0-96fd-61dc5935e4e0/1-2.PNG)

<br>

또한 위의 테이블은 전화번호 그룹이 반복되는 경우이며 2번 조건를 위반한 사례이다.

따라서 1번과 2번의 조건을 만족시키기 위해서는 아래와 같이 분리할 수 있다.

<br>

![](https://images.velog.io/images/hellojihyoung/post/415420f7-0023-4c66-b6fb-40e6b2d5db6c/1-1.PNG)

<br>

그러나 위와 같이 분리하게 되면 3번 조건을 만족시키지 못한다. 따라서 아래와 같은 형태로 최종 수정이 가능하다.

<br>

![](https://images.velog.io/images/hellojihyoung/post/9b975e6c-1f63-4af2-825f-0b7efb83c2cb/1-3.png)

<br>
위의 디자인은 Customer Name과 Customer Telephone Number가 One-to-Many의 관계를 형성하게 된다. 

따라서 기본 키를 사용하여 관련 데이터의 각 집합을 고유하게 식별할 수 있게 되고 중복되는 데이터를 최소화 할 수 있게 되었다.
<br>

<br>

### 제 2정규화(2NF)

테이블의 모든 컬럼이 완전 함수적 종속을 만족해야 한다. (부분적 함수 종속 제거를 통해 완전 함수적 종속을 만족)

- 함수적 종속 : X의 값에 따라 Y값이 결정될 때 X -> Y로 표현하는데, 이를 Y는 X에 대해 함수적 종속 이라고 한다. 예를 들어 학번을 알면 이름을 알 수 있는데, 이 경우엔 학번이 X가 되고 이름이 Y가 된다. X를 결정자라고 하고, Y는 종속자라고 한다. 다른 말로 X가 바뀌었을 경우 Y가 바뀌어야만 한다는 것을 의미한다.
- 부분 함수적 종속 : 함수적 종속에서 X의 값이 여러 요소일 경우, 즉, {X1, X2} -> Y일 경우, X1와 X2가 Y의 값을 결정할 때 이를 완전 함수적 종속 이라고 하고, X1, X2 중 하나만 Y의 값을 결정할 때 이를 부분 함수적 종속 이라고 한다.


조금 쉽게 말하면, 테이블에서 기본키가 복합키(키1, 키2)로 묶여있을 때, 두 키 중 하나의 키만으로 다른 컬럼을 결정지을 수 있으면 안된다.

> 기본키의 부분집합 키가 결정자가 되어선 안된다는 것

<br>

![](https://images.velog.io/images/hellojihyoung/post/f18fad36-f62e-4dfa-9177-8aab1373f235/2.PNG)

<br>

`Manufacture`과 `Model`이 키가 되어 `Model Full Name`을 알 수 있다.

`Manufacturer Country`는 `Manufacturer`로 인해 결정된다. (부분 함수 종속)

따라서, `Model`과 `Manufacturer Country`는 아무런 연관관계가 없는 상황이다.

<br>

결국 완전 함수적 종속을 충족시키지 못하고 있는 테이블이다. 부분 함수 종속을 해결하기 위해 테이블을 아래와 같이 나눠서 2NF를 만족할 수 있다.

<br>

![](https://images.velog.io/images/hellojihyoung/post/9f93524a-b540-4e10-8016-442b9935832c/2-1.PNG)

<br>

<br>

### 제 3정규화(3NF)

2NF가 진행된 테이블에서 이행적 종속을 없애기 위해 테이블을 분리하는 것이다.

> 이행적 종속 : A → B, B → C면 A → C가 성립된다

아래 두가지 조건을 만족시켜야 한다.

- 릴레이션이 2NF에 만족한다.
- 기본 키(primary key)가 아닌 속성(Attribute)들은 기본 키에만 의존해야 한다.

<br>

![](https://images.velog.io/images/hellojihyoung/post/b3e34e04-39f1-47d4-ab56-d5063eda62d7/4.png)

<br>

현재 테이블에서는 `Tournament`와 `Year`이 기본키다.

`Winner`는 이 두 복합키를 통해 결정된다.

하지만 `Winner Date of Birth`는 기본키가 아닌 `Winner`에 의해 결정되고 있다. (2번 위반)

따라서 이는 3NF를 위반하고 있으므로 아래와 같이 분리해야 한다.

<br>

![](https://images.velog.io/images/hellojihyoung/post/925e3db5-adca-4e42-8ec6-90a8d8899fe6/3-2.png)

<br>

위와 같이 분리하게 되면 Winner Date of Birth가 Winner를 거쳐 { Tournament, Year }를 의존하게 되는 이행적 함수 종속 관계가 아닌 Date of Birth -> Winner가 되고, Winner -> { Tournament, Year }가 되면서 완전 함수적 종속 관계가 되게 된다.

<br>

#### 출처 : https://velog.io/@bsjp400/Database-DB-%EC%A0%95%EA%B7%9C%ED%99%94-%EB%B9%84%EC%A0%95%EA%B7%9C%ED%99%94%EB%9E%80