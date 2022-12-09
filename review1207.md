# 그래프와 시각화 

## 기본설정 

```python
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt 

plt.rc('figure', figsize=(10,6)) # 그림 크기 설정 
```

## matplotlib.pyplot의 시각화 도구 API

* 이차원 그래프를 그리는 함수이다.
*  y축 좌표들의 리스트 또는 어레이만 인자로 넣어줄 떄마다.
                                                      
   x측 좌표는 해당 값들의 인덱스로 사용됨


### Figure 객체와 서브플로(subplot0000

- 모든 그래프는 Figure 객체 내에 존재 
- matplotlib.pyplot.figure()함수에 의해 생성 
  
### 참고 

* 서브플롯 
    * Figure객체 내에 그래프를 그리기 위헤 서브플롯을 지정
    * add_subplot()함수를 이용하여 지정된 Figure 객체안에 그래프를 그릴 공간을 만들어본다.

```python
fig = plt.figure()
fig.add_subplot(2,2,1) 
```
- 나의 이해: plt.figure()을 통해 백지 생성 
   - fig.add_subplot(x,y,z) 
   - xy: 총 만들 그래프의 개수 
   - z: xy중 몇 번째 그래프인지 정하는 값 

### 그래프 삽입 
- 마지막에 선언된 서브플롯에 그래프를 그린다.
- 예시)
```py
from numpy.random import randn
data = randn(100).cumsum()
fig = plt.figure()
ax_1 = fig.add_subplot(2,2,1)
plt.plot(data)

ax_2 = fig.add_subplot(2,2,2)
plt.plot(data, "k--")

ax_3 = fig.add_subplot(2,2,3)
plt.plot(data, "k-")


data
```
* 나의 이해 : 랜덤 함수를 호출 
   * 2x2로된 1번그래프에 랜덤난수로 구성된 값을 집어넣는다 
   * 2x2로된 2번그래프에 랜덤난수로 구성된 값을 집어넣고 점선으로 라인스타일을 바꿔 표시한다.
   * 2x2로된 3번 그래프에 랜덤난수로 구성된 값을 집어넣고 검은색 라인스타일로 바꿔 표시한다. 

- 예시2)
- 다른방식으로 함수 호출 
```py
fig = plt.figure()
ax_1 = fig.add_subplot(2,2,1)
ax_2 = fig.add_subplot(2,2,2)
ax_3 = fig.add_subplot(2,2,3)

ax_1.plot(data, "k--")
ax_2.plot(data)
ax_3.plot(data, "k-")
```
* 나의 이해 : 차이점을 알아보자 
    * 예시1번은 각각의 그래프 아래에 입력값을 올려줘야 그래프에 적용이 가능했지만 예시2번처럼 plt를 지우고 몇번째 플롯인지 정의한다면 하단에 깔끔하게 모아주는게 가능하다.
  
### 문제풀이 
```py
# 2x2 인 subplot을 만들고
# 임의의 데이터를 만들어서 예) cumsum, np.arange(30)+ 4*np.random.rand(100) ( = 기울기 1인 직선 + noise)
# 첫번째에는 scatter  
# 두번째에는 histo 
# 세번째는 plot 
# 을 그려보세요
```

---

```py
fig = plt.figure()
ax_1 = fig.add_subplot(2,2,1)
ax_2 = fig.add_subplot(2,2,2)
ax_3 = fig.add_subplot(2,2,3)

data_1 = np.arange(50)+ 10*np.random.rand(50)
data_3 = np.random.rand(100)
data_2 = randn(100).cumsum()

ax_1.scatter(np.arange(50), data_1)
ax_2.hist(data_2)
ax_3.plot(data_3, "k-")
```
* 나의 이해 : 서브플롯 지정까지는 이해완료 
    * data_1을 먼저 이해하자
      * 50까지 카운트 + 난수50개 발생 곱하기 10 
      * x의 값은 1~50까지 세어주는동안
      * y의 값은 x에 값에 난수*10을 더해주는 값이 되겠다 (산점도생성)
    * data_2를 이해해보자 
      * 아까 이해함 (완벽) 
    * data_3를 이해해보자 
      * 난수를 계속 더하는 거구나! 별거없다! 

### 서브플롯 관리 

* matplotlib.pyplot.subplots()
    * 여러 개의 서브플롯을 포함하는 figure 객체를 관리해준다.
    * 아까랑 다르게 s가 붙고 단체관리를 한다고 생각하면 편할듯 
* plt.subplots_adjust()
    * 서브플롯 사이의 여백을 조절한다.
    * 여백의 크기는 그래프의 크기와 숫자에 의존한다.
    * 비어있으면 웬만하면 예쁘게 나오는걸로 확인된다. 

#### 예시 
* 여백이 0인 경우 
```py
fig, axes = plt.subplots(2,3)

plt.subplots_adjust(wspace=0, hspace=0)
```
* 나의 이해 : 간격이 없다 촘촘하다.

```py
fig, axes = plt.subplots(2,3)
for i in range(2):
    for j in range(2):
        axes[i, j].hist(np.random.rand(300), bins = 100)
plt.subplots_adjust(wspace=0, hspace=0)
```

* 나의 이해 : 그래프를 6개 만든다 여기서 주의할점은 우리가 수학을 배웠을 때 알던 (x,y)로 생각하여 (2,3)의 그래프로 생각하면 안된다. 넘파이 차원처럼 3개로 된 2묶음으로 보는게 나을지도... 
    * i 레인지 밑 j레인지 까지 하면 (1,1) (1,2) (2,1) (2,2) 가 되겠습니다. 
    * 저 4개의 칸에 랜덤난수 300개를 집어 넣습니다. 
    * bins 는 막대기 개수라고 합니다 히스토그램이니 개수가 많을 수록 보기 편할거로 예상됩니다.

```py
fig, axes = plt.subplots(2,3)
# subplots_adjust() : 기본 값만 사용해도 보기 좋게 출력 된다. 
plt.subplots_adjust()
```

*여백이 1인 경우 

```py
fig, axes = plt.subplots(2,3)
# subplots_adjust() : 기본 값만 사용해도 보기 좋게 출력 된다. 
# plt.figure(figsize=(20,10)) 추후에 변경
# https://matplotlib.org/stable/api/figure_api.html
plt.subplots_adjust(wspace=1, hspace=1)
```
* 그래프에 따라 다르지만 ()만 줘도 간격은 거의 맞아 떨어집니다.
  
### 색상, 마커, 선 스타일

- 그래프의 속성을 변경하면 스타일이 변경된다.
#### 방법1:문자열 방식
- [예쁜라인](https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html#linestyles)
- [예쁜색상](https://matplotlib.org/stable/api/markers_api.html#module-matplotlib.markers)
```py
ax.plot(x, y, 'g--')
import numpy as np
import matplotlib.pyplot as plt

linestyle_str = [
     ('solid', 'solid'),      # Same as (0, ()) or '-'
     ('dotted', 'dotted'),    # Same as (0, (1, 1)) or ':'
     ('dashed', 'dashed'),    # Same as '--'
     ('dashdot', 'dashdot')]  # Same as '-.'

linestyle_tuple = [
     ('loosely dotted',        (0, (1, 10))),
     ('dotted',                (0, (1, 1))),
     ('densely dotted',        (0, (1, 1))),
     ('long dash with offset', (5, (10, 3))),
     ('loosely dashed',        (0, (5, 10))),
     ('dashed',                (0, (5, 5))),
     ('densely dashed',        (0, (5, 1))),

     ('loosely dashdotted',    (0, (3, 10, 1, 10))),
     ('dashdotted',            (0, (3, 5, 1, 5))),
     ('densely dashdotted',    (0, (3, 1, 1, 1))),

     ('dashdotdotted',         (0, (3, 5, 1, 5, 1, 5))),
     ('loosely dashdotdotted', (0, (3, 10, 1, 10, 1, 10))),
     ('densely dashdotdotted', (0, (3, 1, 1, 1, 1, 1)))]


def plot_linestyles(ax, linestyles, title):
    X, Y = np.linspace(0, 100, 10), np.zeros(10)
    yticklabels = []

    for i, (name, linestyle) in enumerate(linestyles):
        ax.plot(X, Y+i, linestyle=linestyle, linewidth=1.5, color='black')
        yticklabels.append(name)

    ax.set_title(title)
    ax.set(ylim=(-0.5, len(linestyles)-0.5),
           yticks=np.arange(len(linestyles)),
           yticklabels=yticklabels)
    ax.tick_params(left=False, bottom=False, labelbottom=False)
    ax.spines[:].set_visible(False)

    # For each line style, add a text annotation with a small offset from
    # the reference point (0 in Axes coords, y tick value in Data coords).
    for i, (name, linestyle) in enumerate(linestyles):
        ax.annotate(repr(linestyle),
                    xy=(0.0, i), xycoords=ax.get_yaxis_transform(),
                    xytext=(-6, -12), textcoords='offset points',
                    color="blue", fontsize=8, ha="right", family="monospace")


fig, (ax0, ax1) = plt.subplots(2, 1, figsize=(10, 8), height_ratios=[1, 3])

plot_linestyles(ax0, linestyle_str[::-1], title='Named linestyles')
plot_linestyles(ax1, linestyle_tuple[::-1], title='Parametrized linestyles')

plt.tight_layout()
plt.show()
```
- 이해는 아니고 나중에 한번 해보기 

#### 방법2:키워드 인자 지정 방식

```py
ax.plot(x, y, linestyle='--', color='g')

plt.plot(randn(100).cumsum(), "g--")
# 칼라 g에 점선 

plt.plot(randn(100).cumsum(), marker="o", linestyle="dashed")
plt.plot(randn(100).cumsum(), marker="o")
# 대쉬드 라인 스타일 마커o로 찍기

plt.plot(randn(100).cumsum(), marker="o", linestyle="dashed", color = "#16deff")
#라인 색상 바꾸기
```
[RGB 색상코드](https://www.w3schools.com/colors/colors_rgb.asp)


### 여러 그래프 하나의 서브플롯에 그리기 

* 여러 스타일의 그래프를 하나의 서브플롯에 그려 다양한 정보를 동시에 전달 
  
```py 
data_1 = 난수 
plt.plot(data_1, "k--", label= "Default")
plt.plot(data_1, "k-", drawstyle = "steps-post", label="steps")
# label의 범례 위치를 지정하여, 가장 적절한 위치로 지정하여 자동으로 생성
plt.legend(loc = "best")
```
* 나의 이해 : 라벨 설정 drawstyle 그림 그리는 선 변형 
  
#### 범례 표기 
- plt.legend()
- loc='best' : 범례 위치 지정. 기본값은 auto 
- 