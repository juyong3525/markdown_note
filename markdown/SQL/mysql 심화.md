# mysql 심화

### file.sql 파일로 SQL 실행하기
* Mysql Workbench
  - File -> Open SQL Script -> file.sql

<br>

* Mysql 터미널 명령 
  - SOURCE file.sql
  - file.sql 파일 위치는 터미널 명령을 실행하는 동일 디렉토리에 있거나, 해당 디렉토리까지 명시해줘야 함

  <br>
  
  ---
  
  <br>
  
### 테이블에 데이터 한번에 입력하기
  
* mysql CLI로 CSV 파일 LOAD 하기

	<pre>
  	mysql> LOAD DATA INFILE 'CSV 데이터 파일' INTO TABLE dbname.tablename (col1, col2, col3, ...);
	</pre>
  
  <br>
  
- Mysql Workbench
  - Go to Schemas -> Find dbname database (만약 없으면, Schemas 메뉴의 refresh 버튼) -> Go to Tables -> Go to tablename -> Table Data Import Wizard -> filename.csv File 선택 -> Source Column / Dest Column 설정 -> Import

<br>

---

<br>

## pandas 라이브러리와 pymysql   

<br>

### read_sql()
* pandas 라이브러리의 기능 중, read_sql() 메서드로 SQL 바로바로 확인하기
 
#### 데이터베이스 접속

<pre>
import pymysql
import pandas as pd
</pre>

<pre>
host_name = 'localhost'
host_port = 3306
username = 'root'
password = '?????'  
database_name = 'dbname'
</pre>

<pre>
db = pymysql.connect(
    host=host_name,     # MySQL Server Address
    port=host_port,     # MySQL Server Port
    user=username,      # MySQL username
    passwd=password,    # password for MySQL username
    db=database_name,   # Database name
    charset='utf8'
)
</pre>

<br>

#### pandas.read_sql(쿼리, 연결된 db connection 객체)

<pre>
SQL = "SHOW TABLES"
df = pd.read_sql(SQL, db)
</pre>

- df를 출력해보면 db 내에 존재하는 테이블들이 출력된다.

<br>
<br>

#### to_csv()
* pandas 라이브러리의 기능 중, to_csv() 메서드로 검색 결과 파일로 저장하기
<pre>
SQL = "SELECT * FROM tablename"
df = pd.read_sql(SQL, db)
df.to_csv('csvfile.csv', sep=',', index=False, encoding='utf-8')
</pre>

- 실행 결과, 동일한 디렉토리 내에 csvfile.csv 파일이 생성된다.

