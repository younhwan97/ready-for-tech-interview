## 정규화(Normalization)

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
|Oracle|Oracle is ...|높은 보안|

특징 컬럼은 콤마(,)를 기준으로 여러 값을 가져 제1 정규형을 만족하지 않는다.

왜 문제가 될까❓❓

```sql
SELECT * FROM table WHERE 특징 = '무료'
SELECT * FROM table ORDER BY 특징
```

위와 같은 SQL을 사용할 수 없게 된다.

#### 제1 정규형을 만족하는 경우

|이름|설명|특징|
|---|---|---|
|MySQL|MySQL is ...|무료|
|MySQL|MySQL is ...|표준 sql을 사용|
|MySQL|MySQL is ...|다양한 운영체제 사용 가능|
|MongoDB|MongoDB is ...|NoSQL|
|MongoDB|MongoDB is ...|JSON 구조|
|MongoDB|MongoDB is ...|Read/Write 성능 우수|
|Oracle|Oracle is ...|높은 보안|

위와 같이 컬럼을 분리해 제1 정규형을 만족시킬 수 있다. 하지만 이 경우 <strong>이상현상(Anomaly)</strong>이 발생한다.

MySQL의 특징을 하나 추가하기 위해서 설명도 같이 추가해야 하거나 설명이 바뀌면 모든 MySQL을 찾아서 바꿔줘야 한다.

#### 이상현상(Anomaly)

1. 삽입 이상: 새로운 데이터를 추가할 때 불필요한 데이터도 알아야한다. 
2. 삭제 이상: Oracle 데이터를 하나 제거하면, 해당 정보가 모두 사라진다.
3. 갱신 이상: MySQL의 설명이 바뀌면, 해당 값을 모두 바꿔줘야 한다.

<br/>

### 제2 정규화

제1 정규화를 통해 얻는 테이블에서 중복을 제거한다.

중복이 발생하는 이유❓

컬럼이 다른 컬럼에 의존적인 경우 발생한다. 

설명 컬럼은 특징 컬럼과는 관련없이 이름 컬럼에 의존적이다.

#### 제2 정규형을 만족하는 경우

|이름|설명|
|---|---|
|MySQL|MySQL is ...|
|MongoDB|MongoDB is ...|
|Oracle|Oracle is ...|

|이름|특징|
|---|---|
|MySQL|무료|
|MySQL|표준 sql을 사용|
|MySQL|다양한 운영체제 사용 가능|
|MongoDB|NoSQL|
|MongoDB|JSON 구조|
|MongoDB|Read/Write 성능 우수|
|Oracle|높은 보안|

위와 같이 <strong>부분 종속성</strong>을 제거함으로써 중복을 해결할 수 있다.

<br/>

### 제3 정규화

