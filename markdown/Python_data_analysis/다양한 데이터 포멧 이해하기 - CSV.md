# 다양한 데이터 포멧 이해하기: CSV

### 파일 읽기 (Plain Text)

- 파일디스크립터변수 = open(파일이름, 파일열기모드)

```
data_file = open('00_data/USvideos.csv', 'r', encoding='utf-8-sig')
```
    
- 파일 디스크립터 (file descriptor) 변수: 오픈한 파일 객체를 가리키고 있는 변수
- 파일 이름 명시시, open 함수 실행 위치와 파일 이름이 저장된 위치를 파일 절대 경로 또는 상대 경로로 정확히 명시해야 함
- 파일 열기 모드

| 파일열기모드 | 설명                                                                 |
|:------------:|:----------------------------------------------------------------------|
|       r      | 읽기 모드: 파일을 읽기만 할 때 사용함                                |
|       w      | 쓰기 모드: 파일에 데이터를 쓸 때 사용함 (기존 파일 데이터는 삭제됨)  |
|       a      | 추가 모드: 파일의 기존 데이터 끝에서부터 데이터를 추가할 때 사용함   |

- encoding
  - open(파일이름, 파일열기모드, encoding='utf-8-sig') 와 같이 끝에 encoding 구문 추가 가능 (옵션)
  - 파일 오픈시, 해당 파일의 인코딩 방식을 명시해주는 것임

<br>
  
---
  
<br>

### csv 파일 읽기

* CSV(Comma-Separated Values): 스프레드시트 데이터를 저장할 때 가장 널리 쓰이는 파일 형식
* 엑셀등 여러 응용프로그램에서도 지원
* CSV 형식 (각 열은 콤마로 구분, 각 행은 줄바꿈 문자로 구분)
<pre>
  Yong, Hong
  apple, 2
  korea, japan, chian
</pre>

* 파이썬에서 CSV 파일로 저장/읽기 방법
  - csv 라이브러리 사용
 
<br>

### csv.reader(오픈한 파일 디스크립터, delimiter=',')

- open 함수를 통해 오픈한 파일 디스크립터
- delimiter=데이터구분자: csv 파일 내에 데이터 구분자를 명시할 수 있음 (옵션)

```
data_file = open('00_data/USvideos.csv', 'r', encoding='utf-8-sig')
data_lines = csv.reader(data_file, delimiter=',')
```

<br>

### 데이터 읽기

- 각 라인별 데이터를 읽기 위해, for 문을 사용하면 됨

```
data_lines = csv.reader(data_file, delimiter=',')
for data_line in data_lines:
    print (data_line)
```

<br>

### 예

<pre>
import csv

data_file = open('00_data/USvideos.csv', 'r', encoding='utf-8-sig')
data_lines = csv.reader(data_file, delimiter=',')
for data_line in data_lines:
    print (data_line[0])
    break
    
data_file.close()
</pre>

<br>

### csv 파일 읽기 다른 기법

- with 문법을 사용해서, 파일 데이터를 읽은 후, with 내부 구문 실행 완료 후, 자동으로 파일을 닫을 수 있음

<pre>
import csv
with open('00_data/USvideos.csv', 'r', encoding='utf-8-sig') as reader_csv:
    reader = csv.reader(reader_csv, delimiter=',')
    
    for row in reader:
        print (row)
        break

</pre>

<br>

---

<br>

### csv 파일 쓰기

- open 시 'w' 로 옵션을 설정
  - open() 함수에 newline='' 를 넣어주는 이유는 윈도우의 경우에만 csv 모듈에서 데이타를 쓸 때 각 라인 뒤에 빈 라인이 추가되는 문제가 있기 때문
  - 이를 없애기 위해 (파이썬 3 에서) 파일을 open 할 때 newline='' 와 같은 옵션을 지정

```
data_file = open('00_data/data.csv', 'w', encoding='utf-8-sig', newline='')
```
- csv.reader 대신, csv.writer 함수 사용

```
data_write = csv.writer(data_file, delimiter=',')
```
- writerow 함수에 리스트 형식으로 데이터를 넣으면, 한 라인씩 파일에 추가 됨
- 파일 close 는 파일 읽기와 동일함

<br>

### csv 파일 쓰기 다른 기법 (with)

- with 문법을 사용해서, with 내부 구문 실행 완료 후, 자동으로 파일을 닫을 수 있음

<pre>
import csv
with open('00_data/tmp_csv.csv', 'w', encoding='utf-8-sig', newline='') as writer_csv:
    writer = csv.writer(writer_csv, delimiter=',')
    writer.writerow(['love']*3 + ['banana'])   # ['love', 'love', 'love', 'banana'] 와 동일 
    writer.writerow(['apple', 2])   # 문자열 외에도 다양한 타입 데이터 쓰기 가능
    writer.writerow(['Spam', 'Lovely Spam', 'Wonderful Spam']) 
</pre>

<br>

### csv 파일 쓰기 다른 기법 (사전 타입으로 파일 쓰기)

- csv.writer 함수 대신에, csv.DictWriter 함수 사용
- field 이름 선언 후, 데이터 넣기

<pre>
import csv

with open('00_data/tmp_csv.csv', 'w', encoding='utf-8-sig', newline='') as writer_csv:
    field_name_list =['First Name', 'Last Name']  # 필드명 정의
    writer = csv.DictWriter(writer_csv, fieldnames=field_name_list)  # 필드명을 미리 선언할 수 있음
    writer.writeheader()  # 보통 csv 파일 상단에는 필드명을 넣기 때문에, 선언된 필드명을 writerheader() 함수로 넣을 수 있음
    writer.writerow({'First Name': 'Yong', 'Last Name': 'Hong'})  # 각 데이터는 사전 타입으로 저장 가능
    writer.writerow({'First Name': 'Pong', 'Last Name': 'Kim'})
    writer.writerow({'First Name': 'Robin', 'Last Name': 'Park'})
</pre>

<br>

### 사전 타입으로 읽기도 가능

<pre>
import csv

with open('00_data/tmp_csv.csv', 'r', encoding='utf-8-sig') as reader_csv:
    reader = csv.DictReader(reader_csv)
    for row in reader:
        print(row['First Name'], row['Last Name'])
</pre>