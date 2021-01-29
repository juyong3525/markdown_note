# mongoDB CRUD - 1. 데이터 입력

### Document 입력 - insertOne, insertMany
  - insertOne : 한개의 document 생성
  - insertMany : list of document 생성

  <br>
  
  ---

<br>
  
#### Document 입력 문법

<img src="https://www.fun-coding.org/00_Images/mongodb_insert_structure.png" /> 


<br>

---

<br>

#### SQL INSERT 문법과 비교

<img src="https://www.fun-coding.org/00_Images/mongodb_insert.png" /> 

<br>

---

<br>

* insertOne 예제

<pre>
db.articles.insertOne(
     { subject: "coffee", author: "xyz", views: 50 }
)
</pre>

<br>

* insertMany 예제

<pre>
db.articles.insertMany(
   [
     { subject: "coffee", author: "xyz", views: 50 },
     { subject: "Coffee Shopping", author: "efg", views: 5 },
     { subject: "Baking a cake", author: "abc", views: 90  },
     { subject: "baking", author: "xyz", views: 100 },
     { subject: "Café Con Leche", author: "abc", views: 200 },
     { subject: "Сырники", author: "jkl", views: 80 },
     { subject: "coffee and cream", author: "efg", views: 10 },
     { subject: "Cafe con Leche", author: "xyz", views: 10 },
     { subject: "coffees", author: "xyz", views: 10 },
     { subject: "coffee1", author: "xyz", views: 10 }
   ]
)
</pre>
