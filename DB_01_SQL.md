# DB 01 SQL

> INDEX

- Database
  - RDB - 관계형 데이터베이스
- SQL - Structured Query Language
- DDL : 데이터 정의 언어
  - CREATE TABLE
  - ALTER TABLE
  - DROP TABLE
- CSV -> SQLite 테이블로 가져오기
- DML : 데이터 조작 언어
  - SELECT : 특정 테이블에서 데이터를 조회하기 위해 사용
  - ORDER BY : 컬럼을 기준으로 오름차순, 내림차순으로 정렬
  - WHERE : 특정 검색 조건을 지정하여 조회
  - LIMIT, OFFSET
  - GROUP BY : 특정 그룹으로 묶인 결과 생성
  - INSERT / UPDATE / DELETE


# Database
> 자료 파일을 조직적으로 통합하여 자료 항목의 중복을 없애고 자료를 구조화하여 기억시켜 놓은 자료의 집합체

- 데이터 중복 최소화
- 데이터 무결성
- 데이터 일관성
- 데이터 독립성
- 데이터 표준화
- 데이터 보안 유지

## RDB - 관계형 데이터베이스
> 관계형 데이터베이스\
> 키와 값들의 간단한 관계를 표 형태로 정리한 데이터 베이스

- 스키마(schema) : 자료의 구조, 표현 방법, 관계 등 전반적인 명세
- 테이블(table) : 열과 행의 모델을 사용해 조직된 데이터 요소들의 집합
- 열(column) : 고유한 데이터 형식 지정
- 행(row) : 데이터가 저장되는 형태
- 기본키(primary key) : 레코드의 고유 값, 반드시 설정


# SQL - Structured Query Language
> 관계형 데이터베이스 관리시스템의 데이터 관리를 위해 설계된 프로그래밍 언어.\
> 데이터 베이스 스키마 생성 및 수정, 자료의 검색 및 관리, 데이터베이스 객체 접근 조정 관리

- DDL(Data Definition Language)
  - 데이터 정의 언어
  - 관계형 데이터베이스 구조(테이블, 스키마)를 정의하기 위한 명령어
  - CREATE, DROP, ALTER
- DML(Data Manipulation Language)
  - 데이터 조작 언어
  - 데이터를 저장, 조회, 수정, 삭제 등을 하기 위한 명령어
  - INSERT, SELECT, UPDATE, DELETE


# DDL - Data Definition Language
> 데이터 정의 언어

## CREATE TABLE
```sql
-- DDL.sql

CREATE TABLE contacts (
  name TEXT NOT NULL,
  age INTEGER NOT NULL,
  email TEXT NOT NULL UNIQUE
);
```
- Data Type : 데이터 타입
  - NULL
    - NULL value
    - missing or unknown
  - INTEGER : 정수
  - REAL : 실수
  - TEXT : 문자
  - BLOB : 이미지 데이터 등 입력된 그대로 저장된 데이터 덩어리
  - Boolean은 별도로 없고 정수 0과 1로 저장됨
- Constraints : 제약 조건
  - 데이터의 정확성, 일관성을 나타낸다
    - 무결성을 보장, 상태를 일관되게 유지
  - NOT NULL
    - 테이블의 모든 컬럼의 기본 값은 NULL을 사용한다.
    - NOT NULL 제약 조건을 명시하면 NULL을 사용할 수 없다.
  - UNIQUE : 컬럼의 모든 값이 고유한 값으로 서로 구별되도록 함
  - PRIMARY KEY
    - 테이블에서 행의 고유성 식별을 위해 사용되는 컬럼
    - 각 테이블에는 하나의 기본 키만 있음
    - 암묵적 NOT NULL
    - INTEGER 타입에만 사용 가능
  - AUTOINCREMENT
    - 사용되지 않은 값이나 이전에 삭제된 행의 값 재사용 방지
    ```sql
    CREATE TABLE table_name (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      ...
    );
    ```
    - 해당 rowid를 다시 재사용할 수 없음
    - id 컬럼에서 기본적으로 사용하는 제약 조건
  - 그 외

## ALTER TABLE
- Rename a table
- Rename a column
- Add a new column to a table
- Delete a column : DROP
  - 컬럼을 삭제하지 못하는 경우
    - 컬럼이 다른 부분에서 참조되는 경우
    - PK인 경우
    - UNIQUE 제약 조건이 있는 경우
```sql
-- DDL.sql

ALTER TABLE contacts RENAME TO new_contacts;

ALTER TABLE new_contacts RENAME COLUMN name TO last_name;

-- 테이블에 기존 데이터가 있을 경우 해당 컬럼에 NULL이 작성되지만 NOT NULL 제약 조건으로 에러가 발생
ALTER TABLE new_contacts ADD COLUMN address TEXT NOT NULL;

-- DEFAULT 제약 조건을 사용하여 해결
ALTER TABLE new_contacts ADD COLUMN address TEXT NOT NULL DEFAULT 'no address';

ALTER TABLE new_contacts DROP COLUMN address;
```

## DROP TABLE
- 한번에 하나의 테이블만 삭제 가능
- 여러 테이블을 삭제하려면 여러 DROP TABLE문을 실행
- 실행 취소나 복구 불가

```sql
DROP TABLE new_contacts;
```

# CSV -> SQLite 테이블로 가져오기
- DML.sql 파일 생성
- 테이블 생성

```sql
-- DML.sql

CREATE TABLE users (
  first_name TEXT NOT NULL,
  last_name TEXT NOT NULL,
  age INTEGER NOT NULL,
  country TEXT NOT NULL,
  phone TEXT NOT NULL,
  balance INTEGER NOT NULL
);
```
- 데이터베이스 파일 열기
- 모드를 csv로 설정
- csv 데이터를 테이블로 import

```bash
sqlite3 mydb.sqlite3
sqlite> .mode csv
sqlite> .import users.csv users
```

# DML : 데이터 조작 언어

## SELECT
- 특정 테이블에서 데이터를 조회하기 위해 사용

```sql
SELECT col1, col2 FROM table_name;
```

- ORDER BY
- DISTINCT
- WHERE
- LIMIT
- LIKE
- GROUP BY

```
-- DML.sql

SELECT first_name, age FROM users;
SELECT * FROM users;
SELECT rowid, first_name FROM users;
```
- SELECT DISTINCT : 조회 결과에서 중복된 행을 제거
  - NULL값을 중복으로 간주

```sql
SELECT DISTINCT country FROM users;
```

## ORDER BY
- 컬럼을 기준을 오름차순, 내림차순으로 정렬
- SELECT문에 추가
- ASC : 오름차순(기본값)
- DESC : 내림차순
- NULL은 가장 작은 값으로 간주

```sql
-- DML.sql

-- age DESC
SELECT first_name, age FROM users ORDER BY age DESC;
