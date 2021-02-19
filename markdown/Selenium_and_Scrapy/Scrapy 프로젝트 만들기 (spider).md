# Scrapy 프로젝트 만들기 (spider)

### Scrapy 정의

-  Python으로 작성된 오픈소스 웹 크롤링 프레임워크

<br>

### Scrapy 특징

- 크롤링을 좀 더 안정적으로 할 수 있음
	- Scrapy 내부에서 다양한 안전장치가 있음
- 크롤링을 좀 더 빠르게 할 수 있음
	- 크롤링 병행 수행 가능 => 많은 양의 데이터 크롤링 시, 시간 단축
- 다양한 크롤링 관련 기능
	- 크롤링한 데이터를 다양한 포멧으로 저장도 가능

<br>

---

<br>

### 사용 방법

- 실제 크롤링할 스파이더(scrapy 기반 크롤링 프로그램) 생성
- 크롤링할 사이트(시작점)와 크롤링할 아이템(item)에 대한 selector 설정
- 크롤러 실행

<br>

---

<br>

### 설치

```
pip install scrapy
```

<br>

---

<br>

### 크롤링 프로젝트 생성

- 프로젝트를 생성할 디렉토리로 이동 후
- scrapy startproject <프로젝트 이름> 으로 생성

```
scrapy startproject ecommerce

```

<br>

---

<br>

### Spider(크롤러) 작성

> project 이름이 ecommerce일 때, ecommerce/ecommerce 폴더에서 다음 명령으로 작성

- 크롤러 이름: 크롤링 프로젝트 내에, 여러가지 크롤러(spider)가 있을 수 있으므로, 각 크롤러의 이름을 지정
- 크롤링 페이지 주소: 각 크롤러가 크롤링을 시작할 페이지 주소를 지정

```
scrapy genspider <크롤러 이름> <크롤링 페이지 주소>
scrapy genspider gmarket www.gmarket.co.kr    # https:// 생략 하는것을 권장
```

> ecommerce/ecommerce/spiders 디렉토리에 gmarket.py 파일(템플릿)이 생김
> <br> 직접 scrapy genspider 명령을 사용하지 않고, 만들어도 됨

<br>

---

<br>

### spider 실행

- 터미널 환경에서, ecommerce 디렉토리에서 scrapy crawl gmarket

<br>

---

<br>

### 정리

```
scrapy startproject ecommerce	# ecommerce 라는 scrapy 프로젝트 생성
scrapy genspider gmarket www.gmarket.co.kr	# gmarket 이라는 spider(크롤러) 생성 (ecommerce/ecommerce 디렉토리 에서 명령)
scrapy crawl gmarket	# gmarket 이라는 spider 실행 (ecommerce/ecommerce 디렉토리에서 명령)
```