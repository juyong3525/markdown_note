# SQL TABLE

#### 테이블 생성은 이전 글 참조

### 테이블 조회

- 기본 문법 (SHOW TABLES)


<pre>
mysql> SHOW TABLES;
+----------------+
| Tables_in_yong |
+----------------+
| mytable        |
+----------------+
1 row in set (0.00 sec)
</pre>

<br>

- 기본 문법 (DESC 테이블명)

<pre>
mysql> desc mytable;
+-------------+------------------+------+-----+---------+----------------+
| Field       | Type             | Null | Key | Default | Extra          |
+-------------+------------------+------+-----+---------+----------------+
| id          | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| name        | varchar(50)      | NO   |     | NULL    |                |
| modelnumber | varchar(15)      | NO   |     | NULL    |                |
| series      | varchar(30)      | NO   |     | NULL    |                |
+-------------+------------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
</pre>

<br>

---

<br>

### 테이블 삭제

- 기본 문법 (DROP TABLE 테이블명)


<pre>
mysql> DROP TABLE [IF EXISTS] 테이블명;
</pre>

<br>
 
---

<br>

### 3.2.3 테이블 구조 수정

- 테이블에 새로운 컬럼 추가


<pre>
문법: ALTER TABLE [테이블명] ADD COLUMN [추가할 컬럼명][추가할 컬럼 데이터형] 
mysql> ALTER TABLE mytable ADD COLUMN model_type varchar(10) NOT NULL;
</pre>

- 테이블 컬럼 타입 변경<br>


<pre>
문법: ALTER TABLE [테이블명] MODIFY COLUMN [변경할 컬럼명][변경할 컬럼 타입]
mysql>ALTER TABLE mytable MODIFY COLUMN name varchar(20) NOT NULL; 
</pre>

- 테이블 컬럼 이름 변경<br>


<pre>
문법: ALTER TABLE [테이블명] CHANGE COLUMN [기존 컬럼 명][변경할 컬럼 명][변경할 컬럼 타입]
mysql>ALTER TABLE mytable CHANGE COLUMN modelnumber model_num varchar(10) NOT NULL;
</pre>

- 테이블 컬럼 삭제<br>


<pre>
문법: ALTER TABLE [테이블명] DROP COLUMN [삭제할 컬럼 명]
mysql>ALTER TABLE mytable DROP COLUMN series;
</pre>