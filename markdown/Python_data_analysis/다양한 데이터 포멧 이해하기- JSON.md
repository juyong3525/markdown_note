# 다양한 데이터 포멧 이해하기: JSON

### JSON 데이터 포멧 이해하기

 - **J**avaScript **Ob**ject **N**otation 줄임말
 - JSON은 서버와 클라이언트 또는 컴퓨터/프로그램 사이에 데이터를 주고 받을 때 사용하는 데이터 포멧
 - 키와 값을 괄호와 세미콜론과 같이 간단한 기호로 구성하여 표현할 수 있고, 언어나 운영체제에 구애받지 않기 때문에 많이 사용됨
 - 특히 웹/앱 환경에서 Rest API를 사용하여, 서버와 클라이언트 사이에 데이터를 주고 받을때 많이 사용
 - JSON 포멧 예 <br>
 { "id":"01", "language": "Java", "edition": "third", "author": "Herbert Schildt" }
 
<br>
 
---
 
<br>

### JSON 데이터 포멧 읽기

- json 라이브러리 제공

<br>

### json 형식 문자열 <---> 파이썬 사전 데이터 변환

#### json.loads() 함수로 문자열로된 json 데이터를 사전처럼 다룰 수 있음

<pre>
import json

# 변수에 문자열로 된 JSON 포멧의 데이터가 있을 경우
data = '{ "id":"01", "language": "Java", "edition": "third", "author": "Herbert Schildt" }' 

jsondata = json.loads(data)    # json 포멧의 문자열을 dict 타입으로 변환
print (jsondata['id'], jsondata['language'], jsondata['edition'], jsondata['author'], type(jsondata))
</pre>

<br>

#### json.dumps() 함수로 파이썬 사전 데이터를 JSON 문자열 데이터로 변환할 수 있음

<pre>
import json

# 변수에 문자열로 된 JSON 포멧의 데이터가 있을 경우
data = { "id":"01", "language": {"Java":"basic", "Java":"advance"}, "edition": "third", "author": "Herbert Schildt" }

jsondata = json.dumps(data)    # dict 타입 데이터를 json 문자열로 변환
print (jsondata, type(jsondata))
jsondata = json.dumps(data, indent=2) # 들여쓰기
print (jsondata, type(jsondata)) 
</pre>

<br>

### json 파일 <---> 파이썬 사전 데이터 변환

#### json.dump() 함수로 파이썬 사전 데이터를 JSON 파일로 쓰기

<pre>
import json

# 변수에 문자열로 된 JSON 포멧의 데이터가 있을 경우
data = { "id":"01", "language": "Java", "edition": "third", "author": "Herbert Schildt" }
data['language'] = ['Java', 'C']

with open('00_data/test.json', 'w', encoding='utf-8-sig') as json_file:
    json_string = json.dump(data, json_file, indent=2)
</pre>

<br>

#### json.load() 함수로 파일로된 json 데이터를 사전처럼 다룰 수 있음

- JSON 파일 예: 유투브 카테고리 (미국)

```
{
    "kind": "youtube#videoCategoryListResponse",
    "etag": "\"m2yskBQFythfE4irbTIeOgYYfBU/S730Ilt-Fi-emsQJvJAAShlR6hM\"",
    "items": [
        {
            "kind": "youtube#videoCategory",
            "etag": "\"m2yskBQFythfE4irbTIeOgYYfBU/Xy1mB4_yLrHy_BmKmPBggty2mZQ\"",
            "id": "1",
            "snippet": {
                "channelId": "UCBR8-60-B28hp2BmDPdntcQ",
                "title": "Film & Animation",
                "assignable": true
            }
        },
        {
            "kind": "youtube#videoCategory",
            "etag": "\"m2yskBQFythfE4irbTIeOgYYfBU/UZ1oLIIz2dxIhO45ZTFR3a3NyTA\"",
            "id": "2",
            "snippet": {
                "channelId": "UCBR8-60-B28hp2BmDPdntcQ",
                "title": "Autos & Vehicles",
                "assignable": true
            }
        }
    ]
}
```

<pre>
import json

with open('00_data/US_category_id.json', 'r', encoding='utf-8-sig') as json_file:
    json_data = json.load(json_file)
    print (json_data.keys())
</pre>

<pre>
# 출력:
	dict_keys(['kind', 'etag', 'items'])
</pre>

<br>

- items 데이터만 뽑기
  - JSON 데이터에 리스트도 포함될 수 있음 (사전 데이터에 키값이 리스트인 경우와 동일)

<pre>
import json

with open('00_data/US_category_id.json', 'r', encoding='utf-8-sig') as json_file:
json_data = json.load(json_file)
for item in json_data['items']:
    print (item['kind'], item['snippet']['title'])
</pre>

<pre>
# 출력 예:
	youtube#videoCategory Film & Animation
	youtube#videoCategory Autos & Vehicles
	youtube#videoCategory Music
				...
</pre>
 