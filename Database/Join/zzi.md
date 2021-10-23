# Join


## Join이란?
두 개 이상의 테이블이나 데이터베이스를 연결하는 것

## Join을 사용하는 이유
검색하고자 하는 컬럼이 한 개의 테이블에서 전부 조회되지 않는 경우, 즉 여러 개의 테이블을 연결시켜서 데이터를 가져오기 위함

## Join 종류
- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

### INNER JOIN

![image](https://user-images.githubusercontent.com/62633444/138554047-46cac238-1615-481d-98a2-536b03a091a9.png)

- 쉽게 말해 교집합이라고 생각하면 된다.
- 결과값은 A의 테이블과 B 테이블이 모두 가지고 있는 데이터만 검색된다.

```
SELECT <열 목록>
FROM <기준 테이블>
    INNER JOIN<참조할 테이블>
    ON <조인 조건>
[WHERE 검색조건]
```
* ON 대신 WHERE를 쓸 수 있다.

JOIN은 두 개 이상의 테이블을 결합하기 때문에 결합하는 테이블들이 동일한 열을 가지고 있다면 '테이블이름.열이름' 형식으로 테이블명을 명시해줘야 에러가 발생하지 않는다.

```
SELECT B.userID, B.prodID, B.amount, U.name, U.addr, U.phoneNumber
FROM buyTBL B
INNER JOIN userTBL U
ON B.userID = U.userID
```

### LEFT OUTER JOIN
![image](https://user-images.githubusercontent.com/62633444/138554088-8c0fe903-1fd6-427b-ae4d-e966b4a00df5.png)

- 기준 테이블의 값 + 테이블과 기준테이블의 중복된 값을 보여준다.
- 결과값은 A 테이블의 모든 값과 A 테이블과 B 테이블의 중복되는 값이 검색된다.

### RIGHT OUTER JOIN
![image](https://user-images.githubusercontent.com/62633444/138554110-0d93834a-d5f6-4648-bd47-1fa28717a361.png)

- LEFT OUTER JOIN의 반대이다.
- 결과값은 B 테이블의 모든 데이터와 A 테이블과 B 테이블에서 중복되는 값이 검색된다.

### FULL OUTER JOIN

![image](https://user-images.githubusercontent.com/62633444/138554185-7660ff12-126f-4bd3-99a9-e6a6cf904ea8.png)
- 쉽게 말해 합집합을 생각하면 된다.
- A 테이블이 가지고 있는 데이터, B 테이블이 가지고 있는 데이터 모두 검색된다.
- 사실상, 기준 테이블의 의미가 없다.


```
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT)>
    <LEFT | RIGHT | FULL> [OUTER] JOIN <두 번째 테이블(RIGHT)>
    ON <조인 조건>
[WHERE 검색조건];
```

### CROSS JOIN

![image](https://user-images.githubusercontent.com/62633444/138554205-9d313655-ed87-44e6-892f-b86361a20dd1.png)
- 모든 경우의 수를 전부 표현해주는 방식이다.
- 기준 테이블이 A일 경우, A의 데이터 한 ROW를 B 테이블 전체와 JOIN하는 방식이다.
- 위의 경우 A 테이블에 데이터가 3개, B 테이블에 데이터가 4개가 있으므로 총 12개가 검색된다.

```
SELECT * FROM ATable
CROSS JOIN BTable;
```
 INNER과 OUTER 조인과 달리 ON 구문은 사용하지 않는다.

### SELF JOIN

![image](https://user-images.githubusercontent.com/62633444/138554211-c5a40492-bd86-47dd-87dd-9a057003b553.png)
- 자기 자신과 자기 자신을 조인한다는 의미이다.
- 하나의 테이블을 여러번 복사해서 조인한다고 생각하면 된다.
- 자신이 가지고 있는 칼럼을 다양하게 변형시켜 활용할 경우에 자주 사용한다.

만약 '메뚜기'의 천적 곤충의 이름, 천적, 수명을 검색하려면 어떻게 해야 할까?
```
SELECT 이름, 천적, 수명
FROM 곤충테이블
WHERE 이름 = ( SELECT 천적
               FROM 곤충테이블
               WHERE 곤충 = '메뚜기');
```

SELF JOIN을 사용할 때는 반드시 별칭을 이용해서 논리적으로 두 개의 테이블을 분리시켜야 한다.

**이해 잘되는 글
->** https://futurists.tistory.com/17
