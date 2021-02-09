# Selenium

### 특정 사이트에서 검색 결과 가져오기


#### selenium 로드 

<pre>
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

# 드라이버 생성
chromedriver = '/usr/local/Cellar/chromedriver/chromedriver'
driver = webdriver.Chrome(chromedriver)
</pre>

<br>

#### 크롤링 사이트 호출 및 확인
<pre>
# 크롤링할 사이트 호출
driver.get("http://www.python.org")

# 타이틀에 "Python" 이라는 단어가 포함되어 있는지 확인
# assert 문을 충족하지 않으면 에러 발생
assert "Python" in driver.title
</pre>

<br>

#### 주요 함수들

- element, elements
	- find\_element\_by\_tag\_name(): 최초 발견한 태그만 가져오기
	- find\_elements\_by\_tag\_name(): 모든 태그 리스트로 가져오기

<br>

- 주요 함수
	- clear(): input 텍스트 초기화
	- send_keys(키워드): 키보드 입력 값 전달
		- Keys.RETURN - 엔터키
		- dir(Keys): 키에 대응되는 이름 찾기

<pre>
# input 텍스트 초기화
elem.clear()

# 키 이벤트 전송
elem.send_keys("python")

# 엔터 입력
elem.send_keys(Keys.RETURN)
</pre>

<br>

- 주요 함수
	- assert로 driver.page_source 에서 특정 키워드 확인
	- time.sleep() 함수로 일정 시간 대기
	- driver.quit() 함수로 브라우저 끝내기

<pre>
assert "No results found." not in driver.page_source

# 10초 대기
time.sleep(10)

# 브라우저 닫기
driver.quit()
</pre>