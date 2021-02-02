# mongoDB 유용한 함수들

### 컬럼명 변경 

* 저장된 mongodb 데이터의 컬럼명을 변경하는 방법
* update_one(), update_many() 함수 활용

<pre>
예) collection.update_many ({}, { '$rename': {'다른 이름': '다른이름'} })
</pre>

<br>

---

<br>

### find의 다양한 문법

<br>

#### sort

<pre>
docs = actor_collection.find({}).sort('생년월일', pymongo.DESCENDING).limit(10)
</pre>

<br>

#### exists

<pre>
docs = actor.find({'특기': {'$exists':True}}).sort('흥행지수').limit(5)
</pre>

<br>

#### or

<pre>
docs = actor.find({'$or': [{'출연영화':'신세계'}, {'출연영화':'반도'}] }, {'배우이름':1, '출연영화':1, '_id':0})
</pre>

<pre>
docs = actor.find({ '흥행지수': {'$gte': 10000}, '$or': [{'출연영화':'신세계'}, {'출연영화':'반도'}] }, {'배우이름':1, '출연영화':1, '_id':0})
</pre>

<br>

#### nor

- not or

<pre>
docs = actor.find({'$nor': [{'흥행지수': { '$gte': 10000}}, {'흥행지수': { '$lte': 2000}}]}, {'배우이름':1, '흥행지수':1, '_id':0}).limit(3)
</pre>

<br>

#### in, nin

- in: 들어가 있다.
- nin: not in - 들어가 있지 않다.

<pre>
docs = actor.find({'흥행지수': { '$in': [9796, 8317]}}, {'배우이름':1, '흥행지수':1, '_id':0})
</pre>

<pre>
docs = actor.find({'흥행지수': { '$nin': [9796, 8317]}}, {'배우이름':1, '흥행지수':1, '_id':0}).limit(3)
</pre>

<br>

#### skip, limit

- skip(n): 검색 결과 n개만큼 건너뜀
- limit(n): 검색 결과 n개만 표시

<pre>
docs = actor.find({'흥행지수': {'$gte': 10000}}).skip(3).limit(3)
</pre>

<br>

#### list 검색

<pre>
docs = actor.find({'출연영화': '신세계'})
</pre>

<pre>
docs = actor.find({'$or': [{'출연영화': '신세계'}, {'출연영화': '국제시장'}]})
</pre>

<br>

- all
	- and와 비슷함 (출연영화 list에 신세계, 국제시장이 모두 있는 것)

<pre>
docs = actor.find({'출연영화': { '$all': ['신세계', '국제시장']}})
</pre>

<br>

- 리스트 index 번호로 검색하기

<pre>
docs = actor.find({'출연영화.0': '국제시장'})
</pre>

<br>

- 리스트 size로 검색하기

<pre>
docs = actor.find({'출연영화': {'$size': 5}})
</pre>

<br>

#### elemMatch

- 적어도 한 개 이상의 리스트 요소가 복수 개의 조건을 동시에 만족하는 경우
- 아래 코드는 results 라는 리스트에 있는 값들 중 75 이상, 80 미만인 값이 1개이상 있으면 매치됨


<pre>
docs = elemmatch_sample.find({'results': {'$elemMatch': {'$gte':75, '$lt':80}}})
</pre>