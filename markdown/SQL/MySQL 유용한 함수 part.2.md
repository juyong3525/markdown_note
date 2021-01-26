# MySQL 유용한 함수 part.2

#### HAVING


- HAVING 절은 집계함수를 가지고 조건비교를 할 때 사용한다.
- HAVING절은 GROUP BY절과 함께 사용
- 예

```sql
SELECT provider FROM items GROUP BY provider HAVING COUNT(*) >= 100;
```

<br>

#### HAVING절을 포함한 복합 검색

```mysql
SELECT provider, COUNT(*) 
  FROM items  
 WHERE provider != '스마일배송'    -- 스마일배송은 제외
 GROUP BY provider              -- 판매처별로 그룹
HAVING COUNT(*) > 100           -- 베스트상품이 100개 이상 등록된 경우만 검색
 ORDER BY COUNT(*) DESC;        -- 베스트상품 등록갯수 순으로 검색
```

<br>

---

<br>

## JOIN 구문 익히기

* JOIN은 두 개 이상의 테이블로부터 필요한 데이터를 연결해 하나의 포괄적인 구조로 결합시키는 연산

* JOIN은 다음과 같이 세분화될 수 있지만, 보통은 **INNER JOIN**을 많이 사용함
  - INNER JOIN (일반적인 JOIN): 두 테이블에 해당 필드값이 매칭되는 (두 테이블의 모든 필드로 구성된) 레코드만 가져옴
  - OUTER JOIN (참고)
    	- LEFT OUTER JOIN: 왼쪽 테이블에서 모든 레코드와 함께, 오른쪽 테이블에 왼쪽 테이블 레코드와 매칭되는 레코드를 붙여서 가져옴
   	 - RIGHT OUTER JOIN: 오른쪽 테이블에서 모든 레코드와 함께, 왼쪽 테이블에 왼쪽 테이블 레코드와 매칭되는 레코드를 붙여서 가져옴

<br>

### JOIN (INNER JOIN)
* INNER JOIN은 조인하는 테이블의 ON 절의 조건이 일치하는 결과만 출력
* 사용법: FROM 테이블1 **INNER JOIN** 테이블2 **ON** 테이블1과 테이블2의 매칭조건

```mysql
SELECT * FROM items INNER JOIN ranking ON ranking.item_code = items.item_code WHERE ranking.main_category = "ALL" 
```

* 테이블 이름 다음에 한칸 띄고 새로운 이름을 쓰면, SQL구문 안에서 해당 이름으로 해당 테이블을 가리킬 수 있음 (AS 용법과 동일함)
	- 일반적으로 이와 같이 많이 사용됨

```mysql
SELECT * FROM items a INNER JOIN ranking b ON a.item_code = b.item_code WHERE b.main_category = "ALL" 
```