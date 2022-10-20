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

이외에 필요에 따라 다양한 키워드를 추가하여 다양한 결과를 출력할 수 있다.

<br/>

### WHERE

테이블에 조건을 걸어 해당 조건을 만족하는 데이터만 출력되도록 한다.

```SQL
SELECT * FROM table_name WHERE 이름 = '조윤환'
```

위 쿼리의 결과 이름 컬럼에서 '조윤환'이라는 값을 가진 데이터만 출력된다.

- LIKE: 문자열 패턴이 일치하는지 확인
    * WHERE 이름 LIEK '조%' 조건을 걸면 이름 컬럼에서 '조'로 시작하는 값을 갖는 컬럼은 모두 출력
- IN: 포함 여부를 확인
    * WHERE 이름 IN ('조윤환', '정나영') 조건을 걸면 이름 컬럼에서 '조윤환', '정나영'을 값을 갖는 컬럼은 모두 출력

이외에 다양한 연산자는 <a href="https://www.w3schools.com/sql/sql_operators.asp">https://www.w3schools.com/sql/sql_operators.asp</a>에서 확인 가능

<br/>

### GROUP BY


