# 다양한 데이터 포멧 이해하기: Plain Text

### 파일 오픈

- 프로그래밍에서 파일은 다음과 같은 3가지 명령의 순서로 처리할 수 있음
  - 파일 오픈
  - 파일 읽기 또는 쓰기
  - 파일 닫기
  
- 파일디스크립터변수 = open(파일이름, 파일열기모드)

```
data_file = open('00_data/text_data.txt', 'r', encoding='utf-8-sig')
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

  ```
  data_file = open('00_data/text_data.txt', 'r', encoding='utf-8-sig')
  ```
  
<br>
  
---
  
<br>
  
### 파일 닫기
  
- 파일디스크립터변수.close() 함수로 파일을 닫을 수 있음
- 항상 오픈한 파일은 닫아야 함 (파일을 오픈한 채로 놔두면, 컴퓨터에서 관련 자원을 계속 사용중인 상태가 될 수 있음)

```
data_file = open('00_data/text_data.txt', 'r', encoding='utf-8-sig')
data_file.close()
```

<br>

- 자동으로 파일을 닫기 위해 with 구문을 사용활용할 수 있음
	- with open() 명령 as 파일디스크립터: 
	- with 구문 안에서 동작할 코드를 탭으로 들여쓰기 해서 사용하면, with 구문이 모두 끝난 후, 자동으로 해당 파일을 닫아줌

```
with open('00_data/text_data.txt', 'r', encoding='utf-8-sig') as file_desc:
    print ('test')
```

<br>
  
---
  
<br>

### 파일 읽기

> readlines() 함수 사용하기

- 오픈한 파일 디스크립터.readlines() 함수를 호출해서, 전체 데이터를 한줄씩 리스트타입으로 읽어올 수 있음

```
data_file = open('00_data/text_data.txt', 'r', encoding='utf-8-sig')
data_lines = data_file.readlines()
data_lines
```

```
출력 예)
['안녕하세요. Yong 입니다.\n', '본 예제는 Plain Text 파일 예제입니다.\n', '감사합니다.']
```

- 리스트 타입 변수는 항상 for 구문을 사용해서, 각 아이템을 가져오기

```
for data_line in data_lines:
    print (data_line)
data_file.close()
```

```
출력 예)
안녕하세요. Yong 입니다.

본 예제는 Plain Text 파일 예제입니다.

감사합니다.
```

<br>

> readline() 함수 사용하기

-  오픈한 파일 디스크립터.readline() 함수를 호출해서, 현재까지 읽은 파일 데이터의 다음 한 줄을 문자열 타입으로 읽을 수 있음

```
data_file = open('00_data/text_data.txt', 'r', encoding='utf-8-sig')
data_line = data_file.readline()
print (data_line)
```
```
출력 예)
안녕하세요. Yong 입니다.
```

<br>

```
data_line = data_file.readline()
print (data_line)
```
```
출력 예)
본 예제는 Plain Text 파일 예제입니다.
```

<br>

```
data_line = data_file.readline()
print (data_line)
```
```
출력 예)
감사합니다.
```
<br>

```
data_file.close()
```

<br>

> read() 함수 사용하기
 
- 오픈한 파일 디스크립터.read() 함수를 호출해서, 전체 파일 데이터를 문자열 타입으로 읽을 수 있음

```
data_file = open('00_data/text_data.txt', 'r', encoding='utf-8-sig')
data = data_file.read()
data
```
```
출력 예)
'안녕하세요. Yong 입니다.\n본 예제는 Plain Text 파일 예제입니다.\n감사합니다.'
```
```
data_file.close()
```

<br>
  
---
  
<br>

### 파일 쓰기

> write() 함수 사용하기
 
- open() 함수에 파일 열기 모드를 'w'로 해서, 파일 쓰기

##### 파일 써보기

```
data_file = open('00_data/text_data_write.txt', 'w', encoding='utf-8-sig')
data_file.write('안녕하세요\n')
data_file.write('Yong 입니다.\n')
data_file.close()
```

<br>
  
---
  
<br>

### 기존 파일에 데이터 추가하기

- open() 함수에 파일열기모드를 'a' 로 해서, 파일 쓰기

```
data_file = open('00_data/text_data_write.txt', 'a', encoding='utf-8-sig')
data_file.write('본 파일은 임시 파일입니다.')
data_file.close()
```
