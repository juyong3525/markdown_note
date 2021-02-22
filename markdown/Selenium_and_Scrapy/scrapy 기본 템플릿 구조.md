# scrapy 기본 템플릿 구조

### spider 파일 (gmarket.py)

- 클래스 이름은 마음대로, 단 scrapy.Spider를 상속
- name이 크롤러(spider)의 이름
- allowed_domains는 옵션 (삭제해도 무방)
	- 별도 상세 설정으로 허용된 주소 이외의 주소는 크롤링 못하게끔 하는 기능을 위한 변수

- start_urls 가 중요. 크롤링할 페이지 주소를 나타냄
- parse 메소드는 response를 반드시 인자로 받아야 함
	- response에 start_urls 에 기록된 크롤링 결과가 담겨져 오기 때문

```
import scrapy

class GmarketSpider(scrapy.Spider):
	name = 'gmarket'
	allowed_domains = ['www.gmarket.co.kr']
	start_urls = ['http://www.gmarket.co.kr']
	
	def parse(self, response):
		print(response.text)    # response.text 에 크롤링된 데이터가 담겨져 있음
```

<br>

- start_urls 는 리스트로 크롤링할 주소를 여러개 써도 됨
- 동작 방식
	- start_urls 에서 주소를 하나씩 가져와서 (뒤에서 부터 작업됨) 크롤링 한 후,
	- response 에 넣고, parse 메소드를 호출함
	- parse 메소드에 response 에 담아져 있는 크롤링 결과를 원하는 대로 처리하면 됨

```
# 예
start_urls = ['http://coners.gmarket.co.kr/Bestsellers/', 'https://www.naver.com/']
```

<br>

---

<br>

### scrapy shell

> 터미널 환경에서 사용할 수 있음 <br>
> gmarket 베스트 상품 페이지

```
scrapy shell 'http://coners.gmarket.co.kr/Bestsellers'
```
> exit 로 scrapy  shell 을 종료

<br>

- view(response): 크롤링한 페이지를 웹브라우저를 통해 확인

```
view(response)
```

- response.url: 크롤링한 페이지 주소 확인

```
view(response.url)
```

<br>

---

<br>

### spider로 작성해보기

- 크롤링 데이터 출력하기
	- 터미널 환경에서, ecommerce 디렉토리에서 scrapy crawl gmarket 명령

```
import scrapy

class GmarketSpider(scrapy.Spider):
	name = 'gmarket'
	allowed_domains = ['www.gmarket.co.kr']
	start_urls = ['http://www.gmarket.co.kr']
	
	def parse(self, response):
		titles = response.css('div.best-list > ul > li > a::text').getall()
		for title in titles:
		print(title)
```

<br>

---

<br>

### 크롤링 데이터 다루기: 저장하기

- items.py를 작성
	- 크롤링하고자 하는 데이터를 아이템(item)으로 선언해줘야 함
	- 클래스를 만들고, scrapy.Item을 상속, 아이템의 이름을 만들고, scrapy.Field() 를 넣어줘야 함

```
# Define here the models for your scraped items
#
# See documentation in:
# https://docs.scrapy.org/en/latest/topics/items.html

import scrapy


class ReEcommerceItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()
    title = scrapy.Field()
```

<br>

- gmarket.py 수정
	- yield 명령어로 item에 저장할 수 있다.
	- 아이템 클래스 생성 및 아이템 저장
		- 선언: from 프로젝트이름.items import 아이템클래스명
		- 클래스 생성: item = 아이템클래스명()
		- 아이템 저장
			- item['아이템명'] = 아이템데이터
			- yield item

```
import scrapy
from ecommerce.items import EcommerceItem


class GmarketSpider(scrapy.Spider):
    name = 'gmarket'
    allowed_domains = ['corners.gmarket.co.kr/Bestsellers']
    start_urls = ['http://corners.gmarket.co.kr/Bestsellers/']

    def parse(self, response):
        titles = response.css('div.best-list > ul > li > a::text').getall()

        for title in titles:
            item = EcommerceItem()
            item['title'] = title
            yield item
```

<br>

---

<br>

### 다양한 데이터 포멧으로 아이템 저장

- csv, xml, json 포멧
- 터미널 환경에서, ecommerce 폴더에서 다음 명령

```
scrapy crawl 크롤러명 -o 저장할파일명 -t 저장포멧
# 예
scrapy crawl gmarket -o gmarket.csv -t csv
scrapy crawl gmarket -o gmarket.xml -t xml
```

> json 파일을 확인하면, 한글 문자가 깨져 나옴

```
scrapy crawl gmarket -o gmarket.json -t json
```

> settings.py 에서 문자를 유니코드로 설정해 준다.

```
# setting.py 에서 아래 커맨드를 추가함
FEED_EXPORT_ENCODING = 'utf-8'
```

<br>

---

<br>


### pipeline (아이템 후처리)

- 아이템 데이터 후처리하기
	- 일부 아이템은 저장하지 않거나,
	- 중복되는 아이템을 저장하지 않거나,
	- 데이터베이스등에 저장하거나,
	- 특별한 포멧으로 아이템을 저장하고 싶거나

> framework 스타일로 구조화시키기 위해 별도 파일에 작성할 수 있도록 하였음 (parse 메소드에서 작성해도 됨)

- navernews/navernews/pipelines.py
	- 아이템이 저장되려 할 때마다, pipelines.py의 process_item 함수를 호출한다.

<br>

> 우선 gmarket.py 에서 상품과 가격을 모두 가져와보도록 코드를 수정

```
import scrapy
from ecommerce.items import EcommerceItem


class GmarketSpider(scrapy.Spider):
    name = 'gmarket_best'
    allowed_domains = ['corners.gmarket.co.kr/Bestsellers']
    start_urls = ['http://corners.gmarket.co.kr/Bestsellers/']

    def parse(self, response):
        titles = response.css('div.best-list > ul > li > a::text').getall()
        prices = response.css(
            'div.best-list > ul > li > .item_price > .s-price > strong > span > span::text').getall()

        for num, title in enumerate(titles):
            item = EcommerceItem()
            item['title'] = title
            item['price'] = prices[num].strip().replace(
                '원', '').replace(',', '')
            yield item
```

<br>

> pipelines.py 사용을 위해 settings.py를 수정해야 함

- settings.py 수정

```
ITEM_PIPELINES = {
    'ecommerce.pipelines.EcommercePipeline': 300,
}
```

> 기존에 있는 데이터임. 주석만 제거하면 됨

<br>

> 각 아이템 생성 시, pipeline.py 에 있는 process_item 함수를 거쳐가게 되어 있음. <br>
> 필요한 아이템만 return 해주고, 필터링할 아이템은 DropItem 을 통해, 더이상의 아이템 처리를 멈추게 해줘야 함

```
from itemadapter import ItemAdapter
from scrapy.exceptions import DropItem


class ReEcommercePipeline:
    def process_item(self, item, spider):
        if int(item['price']) > 10000:
            return item
        else:
            raise DropItem("drop item having lower price than 10000", item)

```

> 가격이 10000 초과인 아이템만 return 하고, 10000 이하인 아이템은 drop 처리