# SQL DCL 간단 정리

### 터미널 환경에서 mysql 제어하기

<br><br>

#### mysql 사용자 확인, 추가, 비밀번호 변경, 삭제

- mysql 사용자 확인
	- 터미널에서 <b>/usr/local/mysql/bin</b> 으로 이동
	- mysql 사용자 확인
	- ./mysql -u root -p
	- mysql> use mysql;
	- select * from user;

<br>

- 사용자 추가
	- ./mysql -u root -p
	-  mysql> use mysql;
		- 로컬에서만 접속 가능한 userid 생성
			- mysql> create user 'userid'@localhost identified by '비밀번호';
		- 모든 호스트에서 접속 가능한 userid 생성
			- mysql> create user 'userid'@'%' identified by '비밀번호';

<br>

- 사용자 비밀번호 변경
	- mysql> SET PASSWORD FOR 'userid'@'%' = '신규비밀번호';

<br>
		
- 사용자 삭제
	- ./mysql -u root -p
		- mysql> use mysql;
		- mysql> drop user 'userid'@'%';


<br>

---

<br>

#### mysql 권한 설정

- 현재 부여된 권한 확인하기
	- mysql> SHOW GRANTS for 아이디;
	- 예) SHOW GRANTS for 'yong'@'%'

<br>

- 로컬에서만 접속 허용
	- mysql> GRANT ALL ON DATABASE.TABLE to 'root'@localhost;

<br>

- 특정 권한만 허용
	- mysql> GRANT SELECT, UPDATE ON DATABASE.TABLE to 'root'@localhost;


<br>

##### 옵션 상세 (참고)

- ALL – 모든 권한 / SELECT, UPDATE – 조회, 수정 권한등으로 권한 제한 가능
	- 예) GRANT INSERT,UPDATE,SELECT ON \*.\* TO 'username'@'localhost';

<br>

- DATABASE.TABLE – 특정 데이터베이스에 특정 테이블에만 권한을 줄 수 있음
- \*.\* – 모든 데이터베이스에 모든 테이블 권한을 가짐