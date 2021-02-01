# pymongo 기본, CRUD

### pymongo 파이썬에서 사용하기

<pre>
import pymongo
conn = pymongo.MongoClient()    # connect local mongodb
knowledge = conn.knowledge    # db
knowledge_it = knowledge.it    # collection
</pre>

<br>

---

</br>

### pymongo - Create

- insert_one()
- insert_many()

<pre>
# insert_one
post = {"author": "Mike", "text": "My first blog post!", "tags": ["mongodb", "python", "pymongo"] }
knowledge_it.insert_one(post)
</pre>

<br>

<pre>
knowledge_it.insert_many(
    [
        { "author":"Yong Pong", "age":25 },
        { "author":"Yong", "age":35 }
    ]
)
</pre>

<br>

---

<br>

### pymongo - Read

- find_one()
- find()

<pre>
# find_one
print(knowledge_it.find_one({"author": "Yong"}))
</pre>

<br>

<pre>
# find
docs = knowledge_it.find()
for doc in docs:
    print(doc)
</pre>

<br>

---

<br>

### pymongo - Update

- update_one()
- update_many()

<pre>
# update_one
knowledge_it.update_one(
    {"author": "Yong"},
    {"$set":
        {"age": 40}
     }
)
</pre>

<br>

<pre>
# update_many
knowledge_it.update_many(
    {"author": "Yong"},
    {"$set": {"age": 25}}
)
</pre>

<br>

---

<br>

### pymongo - Delete

- delete_one()
- delete_many()

<pre>
# Delete_one
knowledge_it.delete_one({"author": "Yong"})
</pre>

<br>

<pre>
# Delete_many
knowledge_it.delete_many({"author": "Yong"})
</pre>