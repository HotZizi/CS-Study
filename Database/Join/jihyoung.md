# Join


### Join이란?
  <br>

> 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법
  
  <br>
다른 테이블에 있을경우 주로 사용하며 여러개의 테이블을 마치 하나의 테이블인 것처럼 활용하는 방법이다. 보통 Primary key혹은 Foreign key로 두 테이블을 연결한다.

<br>

<br>

테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 하므로 이를 이용하여 데이터 검색에 활용한다.

<br>

### JOIN 종류


- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

<br>

<br>

### 1. INNER JOIN
  <br>
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F99799F3E5A8148D7036659">
  <br>

  교집합으로, 기준 테이블과 join 테이블의 중복된 값을 보여준다.
  결과값은 A의 테이블과 B테이블이 모두 가지고있는 데이터만 검색된다. 
    <br>

    
  ```sql
  SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
INNER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키....


  SELECT
  A.NAME, --A테이블의 NAME조회
B.AGE   --B테이블의 AGE조회
  FROM EX_TABLE A
  INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
  ```

  <br>

### 2. LEFT OUTER JOIN
  <br>

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F997E7F415A81490507F027">
  
  <br>

  기준테이블값과 조인테이블과 중복된 값을 보여준다.

  왼쪽테이블 기준으로 JOIN을 한다고 생각하면 편하다.

  A테이블의 모든 데이터와 A테이블과 B테이블의 중복되는 값이 검색된다.

  ```SQL
  SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
LEFT OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키

  SELECT
A.NAME, --A테이블의 NAME조회
B.AGE   --B테이블의 AGE조회
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
  ```

  <br>

### 3. RIGHT OUTER JOIN
  <br>
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F9984CE355A8149180ABD1D">

<br>

  LEFT OUTER JOIN과는 반대로 오른쪽 테이블 기준으로 JOIN하는 것이다.

  결과값은 B테이블의 모든 데이터와 A테이블과 B테이블의 중복되는 값이 검색된다.

  ```SQL
  SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
RIGHT OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키 .....

SELECT
A.NAME, --A테이블의 NAME조회
B.AGE   --B테이블의 AGE조회
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
  ```

  <br>

### 4. FULL OUTER JOIN
  <br>
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F99195F345A8149391BE0C3">
<br>
  합집합을 말한다. A와 B 테이블의 모든 데이터가 검색된다.
  실제로 기준 테이블의 의미가 없다.

<br>


  ```sql
  SELECT
  테이블별칭.조회할칼럼,
  테이블별칭.조회할칼럼
  FROM 기준테이블 별칭
  FULL OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키 .....

  SELECT
  A.NAME, --A테이블의 NAME조회
  B.AGE   --B테이블의 AGE조회
  FROM EX_TABLE A
  FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
  ```

  <br>

### 5. CROSS JOIN
  
  <br>

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F993F4E445A8A2D281AC66B">

  모든 경우의 수를 전부 표현해주는 방식이다.
  
  기준테이블이 A일경우 A의 데이터 한 ROW를 B테이블 전체와 JOIN하는 방식이다.

  A가 3개, B가 4개면 총 3*4 = 12개의 데이터가 검색된다.

  ```sql
  SELECT
  테이블별칭.조회할칼럼,
  테이블별칭.조회할칼럼
  FROM 기준테이블 별칭
  CROSS JOIN 조인테이블 별칭

  SELECT
  A.NAME, --A테이블의 NAME조회
  B.AGE   --B테이블의 AGE조회
  FROM EX_TABLE A
  CROSS JOIN JOIN_TABLE B
  ```

  ```sql
  SELECT
  테이블별칭.조회할칼럼,
  테이블별칭.조회할칼럼
  FROM 기준테이블 별칭,조인테이블 별칭

  SELECT
  A.NAME, --A테이블의 NAME조회
  B.AGE   --B테이블의 AGE조회
  FROM EX_TABLE A,JOIN_TABLE B
  ```

  <br>

  ### 6. SELF JOIN
    
  <br>

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F99341D335A8A363D0614E8">

  자기자신과 자기자신을 조인하는 것이다.

  하나의 테이블을 여러번 복사해서 조인한다고 생각하면 편하다.

  자신이 갖고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용한다.

  ``` sql
  SELECT
  테이블별칭.조회할칼럼,
  테이블별칭.조회할칼럼
  FROM 테이블 별칭,테이블 별칭2

  SELECT
  A.NAME, --A테이블의 NAME조회
  B.AGE   --B테이블의 AGE조회
  FROM EX_TABLE A,EX_TABLE B
  ```

  

<br>

<br>

##### [참고]
<https://coding-factory.tistory.com/87>