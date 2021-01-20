# SQL DML - CRUD

## CRUD [Create, Read, Update, Delete]

- 데이터 관리는 결국 데이터 생성, 읽기(검색), 수정(갱신), 삭제를 한다는 의미

<br>

---

<br>

### Create (데이터 생성)

- 테이블의 컬럼에 맞추어 데이터를 넣는 작업
- 기본 문법 (INSERT)
	1. 테이블 전체 컬럼에 대응하는 값을 모두 넣기 <br> --> INSERT INTO 테이블명 VALUES (값1, 값2, ...); 


	
	2. 테이블 특정 컬럼에 대응하는 값만 넣기 (지정되지 않은 컬럼은 디폴트값 또는 NULL 값이 들어감) <br> --> INSERT INTO 테이블명 (col1, col2, ...) VALUES(값1, 값2, ...);

<br>

---

<br>


### Read (데이터 검색)

- 테이블에 저장된 데이터를 읽는 작업
- 기본 문법 (SELECT)
	1. <b>테이블 전체 컬럼의 데이터 모두 읽기</b> <br> --> SELECT * FROM 테이블명;
		
		<br>
	
	2. <b>테이블 특정 컬럼의 데이터만 읽기</b> <br> --> SELECT 컬럼1, 컬럼2, ... FROM 테이블명;
	
		<br>
	
	3.  <b>테이블 특정 컬럼의 데이터를 검색하되, 표시할 컬럼명도 다르게 하기</b> <br> --> SELECT 컬럼1 AS 바꿀컬럼이름, 컬럼2 AS 바꿀컬럼이름 FROM 테이블명;

		<br>

	4. <b>데이터 정렬해서 읽기</b> <br> --> ORDER BY 정렬할기준컬럼명 DESC | ASC

		<br>

	5. <b>조건에 맞는 데이터만 검색하기 (비교)</b> <br> --> WHERE 조건문으로 조건 검색 <br> --> 예) SELECT * FROM 테이블명 WHERE 필드명 = '값';

		<br>

	6. <b>조건에 맞는 데이터만 검색하기 (논리 연산자)</b> <br> --> WHERE 조건문으로 조건 검색 <br> --> 논리 연산자 사용 <br> --> 예) SELECT * FROM 테이블명 WHERE (필드명='값') OR (필드명='값');

		<br>

	7. <b>조건에 맞는 데이터만 검색하기 (LIKE를 활용한 부분 일치)</b> <br> --> WHERE 조건문으로 조건 검색 <br> --> LIKE 활용 <br> --> 예) 용으로 시작되는 값을 모두 찾을 경우 <br><br> ------> SELECT * FROM 테이블명 WHERE 필드명 LIKE ' 용% '; <br><br> --> 예) 용이 들어간 값을 모두 찾을 경우 <br><br> ------> SELECT * FROM 테이블명 WHERE 필드명 LIKE ' %용% '; <br><br> --> 예) 용으로 시작되고 뒤에 2글자가 붙을 경우 <br><br> ------> SELECT * FROM 테이블명 WHERE 필드명 LIKE ' 용__ ';

		<br>

	8. <b>결과 중 일부만 데이터 가져오기 (LIMIT)</b> <br> --> 예) 결과 중 처음부터 10개만 가져오기 <br><br> ------> SELECT * FROM 필드명 LIMIT 10; <br><br> --> 예) 결과 중 100번째 부터, 10개만 가져오기 <br><br> ------> SELECT * FROM 필드명 LIMIT 100, 10

		<br>
	
	9. <b>조건 조합</b> <br> --> 위에서 나열한 조건을 조합해서 다양한 Query를 작성할 수 있음 <br> --> 조합 순서 SELECT FROM WHERE ORDER BY LIMIT

<br>

---

<br>

### Update (데이터 수정)

- 테이블에 저장된 데이터를 수정하는 작업
- 기본 문법 (UPDATE)

	1. <b>보통 WHERE 조건문과 함께 쓰여서, 특정한 조건에 맞는 데이터만 수정하는 경우가 많음</b> <br> --> UPDATE 테이블명 SET 수정하고 싶은 컬럼명1 = '수정하고 싶은 값1', 수정하고 싶은 컬럼명2 = '수정하고 싶은 값2'    WHERE 특정 컬럼 <  '값'; 

<br>

---

<br>

### Delete (데이터 삭제)

- 테이블에 저장된 데이터를 삭제하는 작업
- 기본 문법 (DELETE)
	
	1. <b>보통 WHERE 조건문과 함께 쓰여서, 특정한 조건에 맞는 데이터만 삭제하는 경우가 많음</b> <br><br> --> DELETE FROM 테이블명 WHERE 특정 컬럼 = '값';

		<br>
	
	2. <b>테이블에 저장된 모든 데이터를 삭제할 수도 있음</b> <br><br> --> DELETE FROM 테이블명;
