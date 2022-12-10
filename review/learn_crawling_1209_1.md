# 크롤링의 종류 

## 1. 정적 크롤링 
- 웹에 있는 정적인 데이터를 수집할 때 사용 
    * 정적인 데이터란 로그인과 같은 사전 작업 없이 바로 볼 수 있는 데이터
    * 새로고침을 하지 않는 이상 변하지 않는 데이터 
    * 주소를 통해 요청받고 결과를 전달해 주고 종료
---
## 2. 동적 크롤링 
- 웹에 있는 동적인 데이터를 수집할 때 사용
    - 동적인 데이터는 입력,클릭,로그인과 같이 페이지 이동시 얻을 수 있는 데이터
    - 단계적 접근이 필요하기 때문에 수집 속도가 느리지만 수집 대상에 한계가 거의 없다는게 큰 장점
    - 연속적인 접근이 가능, 페이지 이동이 필수적이거나 페이지 안에 정보가 은닉되어 있는 경우 사용

---

|           | 정적 크롤링            | 동적 크롤링                  |
|-----------|------------------------|----------------------------|
| 연속성    | 주소를 통한 단발적 접근  | 브라우저를 사용한 연속적 접근 |
| 속도      | 빠름                    | 느림                       |
| 수집 성능 | 수집 대상에 한계가 있음 | 수집 대상에 한계가 거의 없음  |
---

# 라이브러리 

## 1. time 라이브러리 
- time.time() : time.time()은 UTC를 사용해 현재 시간을 실수 형태로 돌려주는 함수이다.
- time.localtime() : 현재 시간을 년,월,일,시,분,초..의 형태로 출력한다.

```py
import time
print(time.time())

import time
print(time.localtime())
```

## 2. 정적 크롤링 도구 
- requests: 간편한 HTTP 요청 처리를 하는 라이브러리, 웹서비스와 연결하기 위해 사용
- beautifulsoup: html 태그를 처리하는 라이브러리, 웹에 있는 데이터 중 필요한 데이터만 추출하기 위해 사용
- pd.read_html: html 내의 table만 추출할 수 있는 도구 

## 3. 동적 크롤링 도구 
- selenium : 웹 드라이버를 사용해 자동화 기능을 실현하는 라이브러리
    - 웹에 접속해 클릭, 이동과 같은 action을 제어
    - driver를 설치하고 이를통해 제어가능

### 나의 실습과 이해
- 웹 페이지를 가져올때 
```py
from urllib.request import urlopen
import requests
from bs4 import BeautifulSoup as bs

html = urlopen("https://www.naver.com/")
soup = bs(html, "html.parser")
print(soup)

html = requests.get("https://www.naver.com")
soup = bs(html.text, "html.parser")
print(soup)
```

*나의 이해와 실습결과 : 첫 번쨰로 모듈을 불러온 뒤 html로 들어갈 사이트를 설정하고 html을 soup으로 묶어주는데 뒤에 parser은 꼭 필수로 넣어야 한다. 
단 requests를 사용할땐 텍스쳐 형태로 뽑아줘야 한다 (html.text)

# 웹페이지와 HTML
- HTML은 마크로 둘러쌓인 언어라는 뜻으로 구조에 대한 정보를 기반으로 작성된 언어 
- 각각의 구성 요소는 마크 역할을 하는 태그로 감싸져 있다. 

```py
- 기본형 
    - <태그>내용</태그>
    - 웹페이지의 시작과 끝을 의미하는
        - <html></html>
    - 문서의 제목을 의미하는
        -<title></title>
    - 웹에 실제로 표시되는 내용을 의미하는
        -<body></body>
```
* 나의 이해 : 열어주면 닫아주는건 필수 ! 

# HTML 태그의 종류 
- ul : unordered list
    - 순서가 없다 
- ol : ordered list
    - 순서가 있다 
- li : 리스트 아이템
    - 목록의 내용이 되는 실질적 태그
- a : 
    - 하이퍼 링크를 나타내는 태그 (a href 등)
- p : 
    - paragraph의 약자, 긴 글 뭉텅이 
- table : 
    - 표를 나타는 태그 (표로 보이는것들이 주로 쓰임 )
- soup을 이용한 html 태그 검색
    - find("태그") : 첫 번째 태그만 검색
    - find_all("태그") : 전체 태그 검색 후 list로 변환 (인덱싱 가능하다)

### 실습 

```py
find_div_class_group_nav = soup.find("div", class_= "group_nav")
find_div_class_group_nav.text

find_div_id_group_nav = soup.find("div", id= "NM_FAVORITE")
find_div_id_group_nav.text

find_all_div = soup.find_all("div")
find_all_div[3]
```
* 나의 이해 : 형식구조만 알면 될듯하다 앞에는 파일의 형식 ("div"등) 뒤는 id 와 클래스를 구분하여 적는다.

### 실습2 

```py
find_div = soup.find("div", class_="group_nav")
find_all_li = find_div.find_all("li")
for item in find_all_li:
    print(item.text)
    print(item.find("a")["href"])
```
* 나의 이해 : find_div 안 li형식을 모두 찾아네 반복문으로 출력하고 그 안에서 a형식으 하이퍼 링크를 찾아낸다고 이해된다.

# Selector
- 태그 중에는 동일한 태그가 존재할 수 있다.
- 선택자(Selector)는 동일한 태그 여러 개 중에서도 각 태그를 구별할 수 있는 일종의 주소이다.
```py
<div>    
    <div>
        <span> Python </span>
        <span> Hello world </span>
    </div>

    <div>
        <span> Java </span>
        <span> Coffee </span>
    </div>
<div>
```
* 나의 해설 : div안 span을 뽑게 될경우 파이썬과 자바의 스크립트가 둘다 나오게 된다.
하나만 뽑기 힘들다

---

```py 
<div id = "contents">    
    <div class = "metadata1">
        <span class = "language"> Python </span>
        <span class = "project" > Hello world </span>
    </div>

    <div class = "metadata2">
        <span class = "language"> Java </span>
        <span class = "project"> Coffee </span>
    </div>
<div>
```
* 나의 해설 : 클래스와 아이디의 구분이 생기니 원하는 것을 선택해 뽑을 수 있다.

## id와 class 
- id는 중복이 없다 무조건 하나이다
- class는 여러개가 가능하다.

## selector 사용법
- 선택자에 따라 데이터를 찾는 코드에 차이가 있다.
- id는 '#'를 붙이고, class는 '.'을 붙여준다.

- 태그만 사용해 데이터를 찾을 경우 -> 태그
  - div
- 태그와 id를 사용해 데이터를 찾을 경우 -> 태그#id
  - div#123
- 태그와 class를 사용해 데이터를 찾을 경우 -> 태그.class
  - div.456
- 태그, id, class 모두 사용해 데이터를 찾을 경우 -> 태그#id.class
  - div#123.456

- 참고 : class 이름에 공백이 포함될 경우가 종종 있는데, 이럴 경우 공백을 .으로 대체해서 작성하면 된다.

예시 
```py
css_soup = soup.select("div#NM_FAVORITE > div.group_nav > ul.list_nav.type_fix")
```
*나의 해설 : 꺽쇠로 파일 경로를 표현한 모습이다.
