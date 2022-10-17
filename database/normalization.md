## 정규화

### 정규화란?

정제되지 않은 데이터를 관계형 데이터베이스에 어울리는 데이터로 만들어주는 방법

👉 다루기 편한 <strong>표</strong>를 만드는 방법

<br/>

### 제1 정규화

각 컬럼은 하나의 값만 가져야 한다.

#### 제1 정규형을 만족하지 않은 경우

|이름|설명|특징|
|---|---|---|
|MySQL|MySQL is ...|무료, 표준 sql을 사용, 다양한 운영체제 사용 가능|
|MongoDB|MongoDB is ...|NoSQL, JSON 구조, Read/Write 성능 우수|

특징 컬럼은 콤마(,)를 기준으로 여러 값을 가져 제1 정규형을 만족하지 않음.

왜 문제가 될까❓❓

```sql
SELECT * FROM table WHERE 특징 = '무료'
SELECT * FROM table ORDER BY 특징
```

위와 같은 SQL을 사용할 수 없음.

#### 제1 정규형을 만족하는 경우

|이름|설명|특징|
|---|---|---|
|MySQL|MySQL is ...|무료|
|MySQL|MySQL is ...|표준 sql을 사용|
|MySQL|MySQL is ...|다양한 운영체제 사용 가능|
|MongoDB|MongoDB is ...|NoSQL|
|MongoDB|MongoDB is ...|JSON 구조|
|MongoDB|MongoDB is ...|Read/Write 성능 우수||

컬럼의 값을 분리하여 테이블에 데이터를 나눠 저장