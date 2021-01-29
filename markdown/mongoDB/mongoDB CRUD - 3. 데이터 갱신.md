# mongoDB CRUD - 3. 데이터 갱신

### Document 수정 - updateOne, updateMany

  - updateOne - 매칭되는 한개의 document 업데이트
  - updateMany - 매칭되는 list of document 업데이트

<br>

---

<br>

### Document 수정 문법

<img src="https://www.fun-coding.org/00_Images/mongodb_update_structure.png" />

<pre>
- $set: field 값 설정
- $inc: field 값을 증가시키거나, 감소시킴
  - 예: $inc: { age: 2 } - age 값을 본래의 값에서 2 증가
</pre>

<br>

---

<br>

### Document 수정 코드 예제

<pre>
- db.people.updateMany( { age: { $gt: 25 } }, { $set: { status: "C" } } )
- SQL 변환하면, 
  - UPDATE people SET status = "C" WHERE age > 25
- 한 Document만 수정하려면 updateOne을 사용함
- db.people.updateOne( { age: { $gt: 25 } }, { $set: { status: "C" } } )
- db.people.updateMany( { status: "A" } , { $inc: { age: 3 } } )
- SQL 변환하면,
  - UPDATE people SET age = age + 3 WHERE status = "A"
</pre>