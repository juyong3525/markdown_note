# mongoDB CRUD - 2. 데이터 검색(읽기)

### Document 읽기(검색) - findOne, find
  - findOne : 매칭되는 한개의 document 검색
  - find : 매칭되는 list of document 검색

<br>
  
---
  
<br>
  
### Document 읽기(검색) 문법
  
<img src="https://www.fun-coding.org/00_Images/mongodb_find_structure.png" /> 

<br>
  
---
  
<br>

### find() / findOne 명령과 - SQL 문 비교

<pre>
db.people.find() - SELECT * FROM people
db.people.find({ }, { user_id: 1, status: 1 }) - SELECT _id, user_id, status FROM people
db.people.find({ },{ user_id: 1, status: 1, _id: 0 }) - SELECT user_id, status FROM people
db.people.find({ status: "A" }) - SELECT * FROM people WHERE status = "A"
db.people.find({ status: "A", age: 50 }) - SELECT * FROM people WHERE status = "A" AND age = 50
db.people.find({ $or: [ { status: "A" } , { age: 50 } ] }) - SELECT * FROM people WHERE status = "A" OR age = 50
</pre>

<br>
  
---
  
<br>

### 비교 문법

<pre>
$eq     =    Matches values that are equal to a specified value.
$gt     >    Matches values that are greater than a specified value.
$gte    >=   Matches values that are greater than or equal to a specified value.
$in          Matches any of the values specified in an array.
$lt     <    Matches values that are less than a specified value.
$lte    <=   Matches values that are less than or equal to a specified value.
$ne     !=   Matches all values that are not equal to a specified value.
$nin         Matches none of the values specified in an array.
</pre>

<br>
  
---
  
<br>

### 비교 문법 코드 예제

<pre>
db.people.find({ age: { $gt: 25 } }) - SELECT * FROM people WHERE age > 25
db.people.find({ age: { $lt: 25 } }) - SELECT * FROM people WHERE age < 25
db.people.find({ age: { $gt: 25, $lte: 50 } }) - SELECT * FROM people WHERE age > 25 AND age <= 50
db.people.find( { age: { $nin: [ 5, 15 ] } } )) - SELECT * FROM people WHERE age = 5 or age = 15
db.people.find( { user_id: /bc/ } )
db.people.find( { user_id: { $regex: /bc/ } } )
                                                  - SELECT * FROM people WHERE user_id like "%bc%"
db.people.find( { user_id: /^bc/ } )
db.people.find( { user_id: { $regex: /^bc/ } } )
                                                  - SELECT * FROM people WHERE user_id like "bc%"
db.people.find( { status: "A" } ).sort( { user_id: 1 } ) - SELECT * FROM people WHERE status = "A" ORDER BY user_id ASC 
db.people.find( { status: "A" } ).sort( { user_id: -1 } ) - SELECT * FROM people WHERE status = "A" ORDER BY user_id DESC
db.people.count()
db.people.find().count()
                                                  - SELECT COUNT(*) FROM people
db.people.count( { user_id: { $exists: true } } )
db.people.find( { user_id: { $exists: true } } ).count()
                                                  - SELECT COUNT(user_id) FROM people
db.people.count( { age: { $gt: 30 } } )
db.people.find( { age: { $gt: 30 } } ).count()
                                                  - SELECT COUNT(*) FROM people WHERE age > 30
db.people.distinct( "status" ) - SELECT DISTINCT(status) FROM people
db.people.findOne()
db.people.find().limit(1)
                                                  - SELECT * FROM people LIMIT 1
</pre>