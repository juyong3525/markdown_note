# pandas 라이브러리 다루기: 데이터 타입

### pandas 데이터 타입
- pandas 데이터 타입은 파이썬과 다름
  - dtype 으로 불리우며, 주요 데이터 타입은 다음과 같음
    - object 는 파이썬의 str 또는 혼용 데이터 타입 (문자열)
    - int64 는 파이썬의 int (정수)
    - float64 는 파이썬의 float (부동소숫점)
    - bool 는 파이썬의 bool (True 또는 False 값을 가지는 boolean)
    - 이외에 datetime64 (날짜/시간), timedelta[ns] (두 datatime64 간의 차) 도 활용됨

> 가끔 data type 때문에 에러가 나는 경우가 있으므로, 데이터 타입에 대한 이해 및 데이터 타입 변경 기능을 알아둬야 함

<br>

<pre>
seriesdata = pd.Series(['yong', 'alex', 'amir'])
print(seriesdata)
</pre>

<pre>
출력 예:
	0    yong
	1    alex
	2    amir
	dtype: object
</pre>

<pre>
seriesdata = pd.Series([1, 1, 1])
print(seriesdata)
</pre>

<pre>
출력 예:
	0    1
	1    1
	2    1
	dtype: int64
</pre>

<br>

---

<br>

### 데이터 타입 변경: Series.astype(변경할 타입)

<pre>
print(seriesdata.astype('float'))
</pre>

<pre>
출력 예:
	0    1.0
	1    1.0
	2    1.0
	dtype: float64
</pre>

<pre>
seriesdata = pd.Series(['1.1', 1.1, 1.2])
print(seriesdata)
</pre>

<pre>
출력 예:
	0    1.1
	1    1.1
	2    1.2
	dtype: object
</pre>

<pre>
 print(seriesdata.astype('float'))
</pre>

<pre>
출력 예:
	0    1.1
	1    1.1
	2    1.2
	dtype: float64
</pre>

<pre>
seriesdata = pd.Series([True, True, False])
print(seriesdata)
</pre>

<pre>
출력 예:
	0     True
	1     True
	2    False
	dtype: bool
</pre>