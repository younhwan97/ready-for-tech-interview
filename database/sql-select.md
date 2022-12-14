## SQL - SELECT

> SQL❓ <br/> 
관계형 데이터베이스에서 <strong>C</strong>reate, <strong>R</strong>ead, <strong>U</strong>pdate, <strong>D</strong>elete를 수행하기 위한 구조화된 질의어 (Structured Query Language)

|이름|생일|대학|
|---|---|---|
|조윤환|09.03|전남대학교|
|정나영|05.18|전남대학교|

```SQL
SELECT 이름, 생일 FROM table_name
```

SELECT(조회)에서 반드시 필요한 키워드는 SELECT와 FROM이다. 

이외에 필요에 따라 다양한 키워드를 추가하여 다양한 결과를 얻을 수 있다.

<br/>

### WHERE

테이블에 조건을 걸어 해당 조건을 만족하는 데이터만 출력되도록 한다.

```SQL
SELECT * FROM table_name WHERE 이름 = '조윤환'
```

위 쿼리의 결과 이름 컬럼에서 '조윤환'이라는 값을 가진 데이터만 출력된다.

- LIKE: 문자열 패턴이 일치하는지 확인
    * WHERE 이름 LIEK '조%' 조건을 걸면 이름 컬럼에서 '조'로 시작하는 값을 갖는 컬럼은 모두 출력('%조', '%조%' 등)
- IN: 포함 여부를 확인
    * WHERE 이름 IN ('조윤환', '정나영') 조건을 걸면 이름 컬럼에서 '조윤환', '정나영'을 값을 갖는 컬럼은 모두 출력

이외에 다양한 연산자는 <a href="https://www.w3schools.com/sql/sql_operators.asp">https://www.w3schools.com/sql/sql_operators.asp</a>에서 확인 가능하다.

<br/>

### GROUP BY

특정 컬럼을 그룹화 한다.

|이름|타입|생일|소속|
|---|---|---|---|
|조윤환|1|09.03|전남대학교|
|정나영|1|05.18|전남대학교|
|홍길동|2|03.02||
|정다영|3|09.20||
|행복이|3|01.01|인사이드아웃|
|슬픔이|4|03.20|인사이드아웃|

```SQL
SELECT 이름, 타입, 소속 FROM table_name GROUP BY 타입
```

위와 같이 타입 컬럼을 기준으로 GROUP BY 연산을 수행시 같은 타입의 데이터끼리 그룹핑이 된다.

그룹 1 = {조윤환, 정나영} <br/>
그룹 2 = {홍길동} <br/>
그룹 3 = {정다영, 행복이} <br/>
그룹 4 = {슬픔이} <br/>

그리하여 쿼리 수행 결과또한 같은 그룹에 속한 데이터는 하나로 묶여 다음과 같이 출력된다. 

|이름|타입|소속|
|---|---|---|
|조윤환|1|전남대학교|
|홍길동|2||
|정다영|3||
|슬픔이|4|인사이드아웃|

각 그룹이 중복없이 출력된 것을 볼 수 있다. 하지만 위와 같은 사용은 의미가 없다. 해당 그룹을 대표하는 이름, 소속이 무엇이 나올지 알 수 없어서 GROUP BY 연산은 위와 같은 방식으로 사용하지 않는다.

#### 그룹 함수

GROUP BY 키워드는 그룹 함수와 함께 사용되는 것이 일반적이다. 

- COUNT: 각 그룹에 속한 데이터의 개수를 카운팅
- MAX: 각 그룹에 속한 데이터에서 최대값을 리턴
- MIN: 각 그룹에 속한 데이터에서 최소값을 리턴
- SUM: 각 그룹에 속한 데이터의 합을 리턴

```SQL
SELECT 타입, COUNT(*) AS 인원 FROM table_name GROUP BY 타입
```

위 쿼리의 수행은 타입을 기준으로 테이블에서 그룹핑이 이뤄지고, 해당 그룹에 속한 데이터의 개수를 타입과 함께 출력하는 방식이다.

그 결과 다음과 같은 출력을 얻을 수 있다.

|타입|인원|
|---|---|
|1|2|
|2|1|
|3|2|
|4|1|

<strong>각 그룹을 대상으로</strong> COUNT 함수(=그룹 함수)가 수행되고, 타입과 함께 그룹함수의 결과가 출력된 것을 볼 수 있다. 

그러므로 GROUP BY 키워드를 유의미하게 사용하기 위해서는 그룹함수가 필요하다.

> GROUP BY의 대상은 반드시 하나의 컬럼일 필요는 없다. <br/>
소속과 타입으로 GROUP BY가 이뤄졌을 경우 타입뿐만 아니라 소속까지 같은 대상을 기준으로 그룹핑이 이뤄진다.

<br/>

### HAVING 

SELECT 쿼리는 FROM ➡️ WHERE ➡️ GROUP BY ➡️ HAVING ➡️ SELECT ➡️ ORDER BY 순서로 실행된다.

위 실행 순서에서 알 수 있듯이 먼저 테이블을 대상으로 WHERE 조건을 걸었다면, 각 그룹을 대상으로 조건을 걸기위해 HAVING이 필요하다.

```SQL
SELECT 타입, COUNT(*) AS 개수 FROM table_name WHERE 소속 = '전남대학교' GROUP BY 타입 HAVING COUNT(*) <= 2
```

1. 테이블에서 소속이 전남대학교인 데이터만 고른다.
2. 데이터를 타입을 기준으로 그룹핑한다.
3. 각 그룹에 속한 데이터의 개수가 2보다 같거나 작은 그룹만 출력한다.

<br/>

### ORDER BY

SELECT 쿼리 수행의 마지막 단계로 선택된 컬럼에 따라 데이터를 정렬한다.

```SQL
SELECT * FROM table_name ORDER BY 생일 
```

위 쿼리의 결과 생일이 빠른 데이터가 상위에 오도록 오름차순 정렬된다. (DESC 키워드를 붙이면 내림차순 정렬)

만약 생일이 같은 데이터의 경우 정렬순서를 정해주기 위해 정렬기준을 2개로 설정할 수 있다. 

```SQL
SELECT * FROM table_name ORDER BY 생일, 타입
```

생일이 빠른 데이터를 기준으로 오름차순 정렬, 생일이 같은 경우 타입이 빠른 데이터가 먼저 오도록 출력한다.