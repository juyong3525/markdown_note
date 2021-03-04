# pandas 라이브러리와 탐색적 데이터 분석 과정 익히기

### 탐색적 데이터 분석 과정  

- EDA (Exploratory Data Analysis) 라고 함
- 데이터 분석을 위해 raw data를 다양한 각도에서 관찰하여, 데이터를 이해하는 과정
  - 데이터 분석 주제마다 EDA를 통해 진행하는 과정은 각양각색이므로, 정형화된 패턴은 없지만,
  - 크게 다음과 같은 3가지 과정은 기본이 될 수 있으므로 다음 3가지 과정을 기본으로 이해하기로 함

    1. 데이터의 출처와 주제에 대해 이해
    2. 데이터의 크기 확인
    3. 데이터 구성 요소(feature)의 속성(특징) 확인
       - feature: 데이터 구성 요소를 위미함
       - 예: 어떤 초등학교에 학생 성적을 기록한 데이터가 있다면, 학생 이름, 과목별 성적등을 feature로 볼 수 있음 (가볍게 field/column 이라고 봐도 무방함)
       
       
> 존 튜키라는 미국 통계학자가 제안한 분석 방법론 <br>
> 기존 통계학이 가설을 세우고, 가설을 검정하는 방법론에 치우쳐, 데이터 본래의 정보를 파악하기 어려우므로, 본연의 데이터 탐색에 집중하자는 방법론

<br>

---

<br>

### 실제 데이터로 pandas 라이브러리와 탐색적 분석 과정 익히기

#### 코로나 바이러스 데이터와 함께 pandas 라이브러리 익히기

- COVID-19-master 폴더 확인
  - 데이터 다운로드: https://github.com/CSSEGISandData/COVID-19
  - 데이터 압축 풀고 COVID-19-master 폴더를 통째로 pandas_eda 주피터 노트북이 있는 폴더 안에 하위폴더로 이동

<br>

#### pandas 라이브러리로 csv 파일 읽기

- csv 파일을 pandas dataframe 으로 읽기 위해 read_csv() 함수를 사용함
- csv 구분자는 quotechar=구분자 옵션을 넣어서 구분자가 다른 경우도 읽기 가능

```
doc = pd.read_csv("파일명", encoding='utf-8-sig', quotechar=',')
```

- 에러 나는 데이터는 항상 있을 수 있음, 해당 데이터는 생략하는 것이 일반적임

```
doc = pd.read_csv("파일명", encoding='utf-8-sig', error_bad_lines=False)
```

<br>

<pre>
import pandas as pd
doc = pd.read_csv("COVID-19-master/csse_covid_19_data/csse_covid_19_daily_reports/04-01-2020.csv", encoding = 'utf-8-sig', error_bad_lines=False)
</pre>

<br>

---

<br>

<div class="alert alert-block" style="border: 1px solid #FFB300;background-color:#F9FBE7;padding:5px">
<font size="3em" style="font-weight:bold;color:#3f8dbf;">탐색적 데이터 분석: 1. 데이터의 출처와 주제에 대해 이해</font><br>

- 국가별 코로나 바이러스 daily 현황 자료 <br>
- Johns Hopkins University Center for Systems Science and Engineering (JHU CSSE) 에서 작성<br>
- 데이터 소스는 https://github.com/CSSEGISandData/COVID-19/tree/master/who_covid_19_situation_reports 에 명시<br>
   - 실제 데이터 분석에서는 raw data를 어떻게 가져왔는지에 대해서도 세세히 알필요가 있을 때가 있음<br>
    - PDF로 만들어진 공식 문서에서 추출한 데이터와 공식 웹페이지를 크롤링해서 얻은 자료를 CSV 파일로 생성한 것으로 보임<br>
  - 위 데이터는 테스트용 데이터이므로 출처에 대해서는 이 정도만 파악하기로 함<br>
</div>

<br>
<br>

<div class="alert alert-block" style="border: 1px solid #FFB300;background-color:#F9FBE7;padding:5px">
<font size="3em" style="font-weight:bold;color:#3f8dbf;">탐색적 데이터 분석: 2. 데이터의 크기 확인</font><br>
</div>

<br>

#### 1. 데이터를 pandas로 읽은 후, 가장 먼저 하는 일

- 데이터 일부 확인하기
  - head(): 처음 5개(디폴트)의 데이터 확인하기
    - head(n=10): 처음 10개(조정 가능)의 데이터 확인하기 
  - tail(): 마지막 5개의 데이터 확인하기
    - tail(n=10): 마지막 10개(조정 가능)의 데이터 확인하기 

<pre>
doc.head()
</pre>

출력 예:

![](photo/EDA/1.png)

<pre>
doc.tail()
</pre>

출력 예:

![](photo/EDA/2.png)

<br>

#### 2. 보다 다양한 데이터 정보 확인하기

- shape: 데이터의 row, column 사이즈 확인
- info(): column별 데이터 타입과 실제 데이터가 있는 사이즈 확인
  - raw data는 일부 데이터가 없는 경우가 많기 때문에, 실제 데이터의 사이즈 확인이 필요함

<pre>
doc.shape
</pre>

<pre>
출력 예:
	(2483, 12)	# row, column 사이즈
</pre>

<br>

<pre>
doc.info()
</pre>

<pre>
출력 예:
	< class 'pandas.core.frame.DataFrame' >
	RangeIndex: 2483 entries, 0 to 2482
	Data columns (total 12 columns):
	 #   Column          Non-Null Count  Dtype  
	---  ------          --------------  -----  
	 0   FIPS            2171 non-null   float64
	 1   Admin2          2221 non-null   object 
	 2   Province_State  2307 non-null   object 
	 3   Country_Region  2483 non-null   object 
	 4   Last_Update     2483 non-null   object 
	 5   Lat             2482 non-null   float64
	 6   Long_           2482 non-null   float64
	 7   Confirmed       2483 non-null   int64  
	 8   Deaths          2483 non-null   int64  
	 9   Recovered       2483 non-null   int64  
	 10  Active          2483 non-null   int64  
	 11  Combined_Key    2483 non-null   object 
	dtypes: float64(3), int64(4), object(5)
	memory usage: 232.9+ KB
</pre>

<br>
<br>

<div class="alert alert-block" style="border: 1px solid #FFB300;background-color:#F9FBE7;padding:5px">
<font size="3em" style="font-weight:bold;color:#3f8dbf;">탐색적 데이터 분석: 3. 데이터 구성 요소(feature)의 속성(특징) 확인</font><br>
</div>

<br>

#### 1. 각 column 이해하기

- raw data에는 다양한 column 이 있는 경우가 많고, 이 중에서 내가 사용할 column 에 대해서는 확실히 이해하고 있어야 함
- Country_Region: 국가, Lat/Long: 위도/경도, Confirmed: 확진, Deaths: 사망, Recovered: 회복, Active: 확진 중인 사람(사망자/회복자 제외)

<pre>
doc.columns
</pre>

<pre>
출력 예:
	Index(['FIPS', 'Admin2', 'Province_State', 'Country_Region', 'Last_Update',
	       'Lat', 'Long_', 'Confirmed', 'Deaths', 'Recovered', 'Active',
	       'Combined_Key'],
	      dtype='object')
</pre>

<br>

#### 2. 속성이 숫자라면, 평균, 표준편차, 4분위 수, 최소/최대값 확인하기

- describe(): 숫자 데이터의 기본 통계치를 한번에 확인할 수 있음

<pre>
doc.describe()
# count: 갯수, mean: 평균, std: 표준편차, min: 최소값, max: 최대값
# 25%/50%/75%: 4분위수로 전체 데이터 중, 25%/50%/75% 각각에 해당하는 수치가 몇 인지를 알려줌
</pre>

출력 예:

![](photo/EDA/3.png)

<br>

#### 3. 속성간 상관관계 이해하기

- corr(method=상관계수): 각 속성간 상관 관계 확인하기 (피어슨 상관계수가 디폴트임)
- 피어슨 상관계수는 선형 상관 관계를 조사하며, 일반적으로
  - +1에 가까우면, 양의 선형 상관 관계 (1에 가까울 수록 선에 가까운 데이터가 많고, 한 변수값이 증가하면, 다른 변수값도 증가)
  - 0에 가까우면 상관관계가 없고
  - -1에 가까우면 음의 선형 상관 관계를 가진다 (-1에 가까울 수록 선에 가까운 데이터가 많고, 한 변수값이 증가하면, 다른 변수값은 감소) 라고
  해석됨
  
  
> 참고: 피어슨 상관계수 관계   <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/34/Correlation_coefficient.png/600px-Correlation_coefficient.png">
> 출처: [위키피디아]( https://ko.wikipedia.org/wiki/%ED%94%BC%EC%96%B4%EC%8A%A8_%EC%83%81%EA%B4%80_%EA%B3%84%EC%88%98)

<br>

<pre>
doc.corr()
</pre>

출력 예:

![](photo/EDA/4.png)

<br>

---

<br>

#### 참고: 데이터 시각화를 통한 데이터 이해

- 데이터를 보다 깊게 이해하기 위해, 데이터를 시각화할 수 있음
- 방대한 데이터를 숫자로 보는 것보다, 눈으로 보면 보다 명확히 이해할 수 있음
- 다양한 데이터 시각화 라이브러리가 존재하므로, 이 중에서 데이터 탐색의 상관관계 분석을 위해, 바로 사용할 수 있는 라이브러리를 이해하기로 함

<br>

#### 참고

- matplotlib: 파이썬에서 가장 기본적으로 사용하는 자료를 그래프로 보여주는 시각화 라이브러리
  - 가장 좋기 때문에, 많이 사용된 것이 아니라, 이전부터 사용해왔기 때문에 사용된다고 하는 편이 맞음
- seaborn: matplotlib을 기반으로 다양한 통계 차트 및 색상 테마를 추가한 라이브러리
  - matplotlib 라이브러리로만은 이쁘지 않았고, 다양한 차트에 대한 요구가 많아서 개발된 라이브러리

<br>

#### 보통 다음과 같이 임포트하고 as로 변경된 이름을 사용함

<pre>
import matplotlib.pyplot as plt
import seaborn as sns
</pre>

- 주피터 노트북을 사용할 때, 그래프를 표현하기 위해 특별한 명령을 해주어야 함

<pre>
%matplotlib inline
</pre>

#### 화면에 표시될 그래프 사이즈 조정

<pre>
plt.figure(figsize=(5,5))
</pre>

<pre>
출력 예:
	< Figure size 360x360 with 0 Axes >
	< Figure size 360x360 with 0 Axes >
</pre> 

<br>

#### 화면에 표시될 그래프 사이즈 조정

```
sns.heatmap(data = doc.corr(), annot=True, fmt = '.2f', linewidths=0.5, cmap='Blues')
```

- data=테이블형: 데이터셋(데이터프레임)
- annot=True: 박스 안에 값 표시
- fmt='0.2f': 박스 안에 표시될 값의 표시 형식 설정 (0.2f 는 소숫점 두자릿수를 의미함)
- linewidths=0.5: 박스와 박스 사이의 간격 설정
- cmap='Blues': 색상 선택 (https://matplotlib.org/3.1.0/tutorials/colors/colormaps.html)

<br>

<pre>
%matplotlib inline
import matplotlib.pyplot as plt 
import seaborn as sns

plt.figure(figsize=(5,5))
sns.heatmap(data = doc.corr(), annot=True, fmt = '.2f', linewidths=0.5, cmap='Greens')
</pre>

출력 예:

<img src="photo/EDA/5.png" width="400" height="400">