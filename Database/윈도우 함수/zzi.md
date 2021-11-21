# 윈도우 함수

## 1. 윈도우 함수란?

- 윈도우 함수는 행과 행 간의 관계를 정의하기 위해서 제공되는 함수
- 윈도우 함수를 사용해서 순위, 합계, 평균, 행 위치 등을 조작할 수 있다.

## 2. 윈도우 함수의 구조

```
SELECT WINDOW_FUNCTION(ARGUMENTS)
  OVER (PARTITION BY 칼럼
     ORDER BY WINDOWING절)
FROM 테이블명;
```

<br/>

|구조|설명|
|------|---|
|ARGUMENTS(인수)|윈도우 함수에 따라서 0~N개의 인수를 설정한다.|
|PARTITION BY|전체 집합을 기준에 의해 소그룹으로 나눈다.|
|ORDER BY|어떤 항목에 대해서 정렬한다.|
|WINDOWING|행 기준 범위를 정한다. ROWS는 물리적 결과의 행 수이고 RANGE는 논리적인 값에 의한 범위이다.|

<br/>

### WINDOWING
|구조|설명|
|------|---|
|ROWS|부분집합인 윈도우 크기를 물리적 단위로 행의 집합을 지정한다.
|RANGE|논리적 주소에 의해 행 집합을 지정한다.|
|BETWEEN~AND|윈도우의 시작과 끝 위치를 지정한다.|
|UNBOUNDED PRECEDING|윈도우 시작 위치가 첫 번째 행임을 의미한다.|
|UNBOUNDED FOLLOWING|윈도우 마지막 위치가 마지막 행임을 의미한다.|
|CURRENT ROW|윈도우 시작 위치가 현재 행임을 의미한다.(데이터가 인출된 현재 행을 의미한다.)|

## 3. 윈도우 함수의 사용

<img width="598" alt="스크린샷 2021-11-21 오전 8 53 55" src="https://user-images.githubusercontent.com/62633444/142744260-32e727dc-945f-45a1-8b8c-a3fb2ebf4694.png">

### 3.1 순위 함수(RANK FUNCTION)

- RANK: 동일값인 경우 동일순위 부여, 공동 순위가 있는 경우 해당 순위를 건너뛰고 부여
- DENSE_RANK: 동일값인 경우 동일순위 부여, 공동 순위가 있는 경우 해당 순위를 연이어서 부여
- ROW_NUMBER: 항상 unique한 순위 부여(동일값이라고 하더라도 어떻게든 순위를 구분한다.)

<br/>

**개인별 salary 옆에, salary_rank 를 추가하기**
<img width="761" alt="스크린샷 2021-11-21 오전 8 54 48" src="https://user-images.githubusercontent.com/62633444/142744269-68e22d33-31cf-46cd-b6af-2a2742f01a07.png">

**개인별 salary 옆에, department별로 그룹핑해서 salary_rank를 추가하기**
<img width="762" alt="스크린샷 2021-11-21 오전 9 05 33" src="https://user-images.githubusercontent.com/62633444/142744434-23a0a245-992d-479d-951c-a6d36d7ed241.png">

### 3.2 집계 함수(AGGREGATE FUNCTION)

- SUM: 파티션 별로 합계를 계산한다.
- AVG: 파티션 별로 평균을 계산한다.
- COUNT:	파티션 별로 행 수를 계산한다.
- MAX,MIN:	파티션 별로 최댓값과 최솟값을 계산한다.

<br/>

**개인별 salary 옆에, 전체의 평균 salary 컬럼을 추가하기**
<img width="761" alt="스크린샷 2021-11-21 오전 9 02 25" src="https://user-images.githubusercontent.com/62633444/142744390-8a4cf438-0d02-4af6-9b2f-e8d8b646fdb7.png">

**개인별 salary 옆에, 각 개인이 속한 department의 평균 salary 컬럼을 추가하기**
<img width="761" alt="스크린샷 2021-11-21 오전 9 04 12" src="https://user-images.githubusercontent.com/62633444/142744409-359822c0-d33f-47f6-a612-3f8200343f17.png">

