# MySQL 유용한 함수

## GROUP BY, COUNT, SUM, AVG, MAX, MIN, DISTINCT, AS

<br>

#### COUNT 함수
- COUNT: 검색 결과의 row 수를 가져올 수 있는 SQL 문법
- SQL 예제: SELECT COUNT(*) FROM items

<br>

```python
sql = """SELECT COUNT(*) FROM items WHERE item_code = '""" + item_info['item_code'] + """';"""
cursor.execute(sql)
result = cursor.fetchone()
print (result[0])
```
<br>

- COUNT SQL 예제1: 
  ```mysql>
  SELECT COUNT(*) FROM people (전체 row 수)
  ```
  
- COUNT SQL 예제2: 
  ```mysql>
  SELECT COUNT(age) FROM people (age field 값이 있는 row 수)
  ```
  
  <br>
  
| num | name  | age |
|-----|-------|-----|
| 1   | Yong  | 12  |
| 2   | Pong | 43  |
| 3   | Jun  |     |

<br>

---

<br>

#### SUM, AVG, MAX, MIN 함수
* SUM(): 컬럼값의 합계
* AVG(): 컬럼값의 평균
* MAX(): 최대 컬럼값
* MIN(): 최소 컬럼값
* SQL 예제: 
  ```mysql>
  SELECT AVG(age) FROM people
  ```
  
  <br>
  
| num | name  | age | gender |
|-----|-------|-----|--------|
| 1   | Yonh  | 12  | man    |
| 2   | Pong | 43  | woman  |
| 3   | Jun  | 20  | man    |

<br>

---

<br>

#### GROUP BY
- GROUP BY: 그룹을 지어서, 데이터를 분석하고자 할 때 사용
- COUNT, SUM, AVG, MAX, MIN 함수와 함께 사용하면 각 그룹별 row 수, 합계, 평균, 최대, 최소값등을 알 수 있음
- SQL 예제: 
  ```mysql>
  SELECT AVG(age) FROM people GROUP BY gender
  ```
  
  <br>
  
| num | name  | age | gender |
|-----|-------|-----|--------|
| 1   | Yong  | 12  | man    |
| 2   | Pong | 43  | woman  |
| 3   | Jun  | 20  | man    |

<br>

---

<br>

#### DISTINCT 
- 특정 컬럼값 출력시 중복된 값을 출력하지 않음
- SQL 예제: 
  ```mysql>
  SELECT DISTINCT gender FROM people
  ```
  
<br>
  
| num | name  | age | gender |
|-----|-------|-----|--------|
| 1   | Yong  | 12  | man    |
| 2   | Pong | 43  | woman  |
| 3   | Jun  | 20  | man    |

<br>

---

<br>

#### AS 
- 특정 결과값의 이름을 변경하는 방법
- 예: COUNT(*) 를 total_count로 이름을 변경하기
  ```mysql>
  SELECT COUNT(*) AS total_count FROM people;
  ```

<br>

---

<br>

#### 복합검색
- WHERE, GROUP BY, ORDER BY등 다양한 SQL 문법을 복합적으로 사용하는 방법
- WHERE절, GROUP BY절, ORDER BY절 순으로 작성
- 예: 
  ```mysql>
  SELECT provider, COUNT(dis_price) FROM items GROUP BY provider ORDER BY COUNT(dis_price) DESC;
  ```