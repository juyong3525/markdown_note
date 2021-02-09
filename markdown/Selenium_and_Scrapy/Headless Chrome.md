# Headless Chrome

### Headless Chrome

- 브라우저를 열지 않고 원하는 데이터를 수집할 수 있음
- 기존의 chromedriver만 사용했을 때는 브라우저가 열리고 자동으로 진행되는 모습이 보였지만
- headless chrome을 사용하면 브라우저가 열리지 않고 내부적으로 동작함

> 예

<pre>
from selenuim import webdriver
from selenium.webdriver.common.keys import Keys
import time

# webdriver에 옵션을 줄 수 있음
options = webdriver.ChromeOptions()
options.add_argument('headless')
options.add_argument('window-size=1920x1080')
options.add_argument('disable-gpu')
options.add_argument('User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.102 Safari/537.36')
options.add_argument('lang=ko_KR')

chromedriver = '/usr/local/Cellar/chromedriver/chromedriver'
driver = webdriver.Chrome(chromedriver, options=options)

driver.get('http://www.python.org')
print(driver.title)
print(driver.current_url)

assert "Python" in driver.title

search = driver.find_element_by_id("id-search-field")
search.clear()
search.send_keys('python')
search.send_keys(Keys.RETURN)

time.sleep(2)

assert "No results found." not in driver.page_source

data = driver.find_elements_by_css_selector("#content > div > section > form > ul > li > h3 > a")
for item in data:
    print(item.text)
driver.quit()
</pre>