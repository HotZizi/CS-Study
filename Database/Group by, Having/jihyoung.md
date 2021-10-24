# Group By, Having

### GROUP BY절이란?

테이블 SELECT시 조회 결과를 그룹으로 묶어서 그 결과를 가져오는 역할을 한다.

<br>

### DISTINCT절이란?

DISTINCT는 GROUP BY절과 마찬가지로 조회결과를 그룹으로 묶어서 그 결과를 가져온다.

주로 UNIQUE한 컬럼을 조회할 경우 사용되는 구절이다.

<br>

### GROUP BY절과 DISTINCT의 차이점

#### > 공통점
- 그룹을 지어줌

#### > 차이점

- GROUP BY : 결과물을 정렬해서 표현
- DISTINCT : 결과물을 정렬하지 않음


정렬이 필요하지않다면 DISTINCT절을 사용하는것이 속도면에서 GROUP BY절보다 빠르다.

<br>

### 문법

<br>

```sql
--GROUP BY
SELECT칼럼 FROM 테이블 GROUP BY 칼럼명
SELECT AGE FROM MY_TABLE GROUP BY AGE
SELECT AGE FROM MY_TABLE GROUP BY AGE WHERE HAVING AGE>=35
```
##### * HAVING : GROUP BY 절에는 조건문을 HAVING으로 준다.

<br>

```sql
--DISTINCT
SELECT DISTINCT 칼럼명 FROM 테이블명
SELECT DISTINCT AGE FROM MY_TABLE
```
