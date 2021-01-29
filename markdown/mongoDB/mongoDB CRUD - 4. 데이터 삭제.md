# mongoDB CRUD - 4. 데이터 삭제

### Document 삭제 - removeOne, removeMany

  - removeOne - 매칭되는 한개의 document 삭제
  - removeMany - 매칭되는 list of document 삭제

<br>
  
---
  
<br>

### Document 삭제 문법

<img src="https://www.fun-coding.org/00_Images/mongodb_delete_structure.png" /> 

- db.people.deleteMany( { status: "D" } )
	- SQL로 변환하면,
		- DELETE FROM people WHERE status = "D"

<br>

- db.people.deleteMany({})
	- SQL로 변환하면,
		- DELETE FROM people  
