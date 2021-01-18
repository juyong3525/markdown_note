#type casting (형 변환)

###1.  int -> float (정수 -> 소수)
- float (변환할 정수형 변수)

```
int_num = 10	# 정수형 변수
float_num = float(int_num)	# float() 소수로 변환
```
```
print(float_num)	# float_num 출력
10.0	# 소수로 출력됨
```
---
 <br>
 <br>
 
###2. str -> float (문자 -> 소수)
- float (변환할 문자형 변수)
- 문자형 변수는 소수로 변환 가능한 형태여야 함 
	- 예) 문자형 변수 = "10.11"

```
str_num = "10.11"  # 문자형 변수
float_num = float(str_num)    # float() 소수로 변환
```
```
print(float_num)		# float_num 출력
10.11	# 소수로 변환됨
```
```
print(type(float_num))	# float_num의 type 출력
<class 'float'>		# 소수형으로 잘 출력됨
```
---
 <br>
 <br>

###3. float -> int (소수 -> 정수)
- int (변환할 소수형 변수)

```
float_num = 9.99  # 소수형 변수
int_num = int(float_num)    # int() 정수로 변환
```
```
print(int_num)		# int_num 출력
9	# 소수점을 버리고 정수로 출력됨
```
---
 <br>
 <br>

###4. str -> int (문자 -> 정수)
- int (변환할 문자형 변수)
- 문자형 변수는 정수로 변환 가능한 형태여야 함 
	- 예) 문자형 변수 = "10"

```
str_num = "10"  # 문자형 변수
int_num = int(str_num)    # int() 정수로 변환
```
```
print(int_num)		# int_num 출력
10	# 정수로 변환됨
```
```
print(type(int_num))	# int_num의 type 출력
<class 'int'>	# 정수형으로 잘 출력됨
```