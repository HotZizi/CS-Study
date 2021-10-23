# Group by, Having

## Group by
GROUP BY 명령어를 통해 특정 컬럼을 기준으로 그룹화 할 수 있습니다.

```
--사원의 수를 성별로 조회
select gender, count(*) from employees group by gender;
+--------+----------+
| gender | count(*) |
+--------+----------+
| M      |   179973 |
| F      |   120051 |
+--------+----------+

--각 부서에 근무하고 있는 사원들의 수 (현재: to_date = '9999-01-01')
select dept_no, count(*)
from dept_emp
where to_date = '9999-01-01'
group by dept_no;
+---------+----------+
| dept_no | count(*) |
+---------+----------+
| d001    |    14842 |
| d002    |    12437 |
| d003    |    12898 |
| d004    |    53304 |
| d005    |    61386 |
| d006    |    14546 |
| d007    |    37701 |
| d008    |    15441 |
| d009    |    17569 |
+---------+----------+
```

## having
group by절을 이용하여 개발자가 정한 기준으로 그룹을 나눈 후
having절로 만든 조건에 맞는 그룹의 데이터만 가져올 수 있다

```
--10만명 이상이 사용하고 있는 직함의 이름과 사원의 수
select title, count(*)
from titles
group by title
having count(*) >= 100000;
+----------+----------+
| title    | count(*) |
+----------+----------+
| Staff    |   107391 |
| Engineer |   115003 |
+----------+----------+
```

### where 와 having의 차이점?
where은 기본적인 조건절로서 우선적으로 모든 필드를 조건에 둘 수 있다. 
하지만 **having은 group by 된 이후 특정한 필드로 그룹화 되어진 새로운 테이블에 조건을 줄 수 있다.**
