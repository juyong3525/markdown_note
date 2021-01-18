# SQL DDL(Data Definition Language) 이해


## 데이터베이스

- 데이터베이스 안에는 여러 개의 데이터베이스 이름이 존재한다.
- 각 데이터베이스 이름 안에는 여러 개의 테이블이 존재한다.
	1. 데이터베이스 생성 <br>-> CREATE DATABASE dbname;
	2. 데이터베이스 목록 보기 <br>-> SHOW DATABASES;
	3. dbname 데이터베이스 사용 시 <br>-> USE dbname;
	4. dbname 데이터베이스 삭제 <br>-> DROP DATABASE [IF EXISTS] dbname;
		* IF EXITSTS: 해당 데이터베이스 이름이 없더라도 오류를 발생시키지 마라는 의미

<br>

---

<br>

## 테이블

- 기본 문법 (CREATE TABLE 구문)
	-  테이블을 생성할 DB를 사용하겠다고 명령

		```
		CREATE DATABASE dbname;
		USE dbname;
		```
<br>

	- 테이블 생성

		```
		CREATE TABLE 테이블명 (
			컬럼명 데이터형,
			컬럼명 데이터형,
				.
				.
			Primary Key 가 될 필드 지정
		);
		```
		
<br>

---

<br>

### Tip.

- NOT NULL: 널 값 방지
- AUTO_INCREMENT: 자동 증가 옵션