# 12 06일 복습

# Pandas 

## Time Series 
- "timeseries" 데이터는 DatetimeIndex 또는
PeriodIndex로 구성된 데이터 셋이다.

---

### to_datetime

```python
date_1 = pd.to_datetime("20221206")
print(date_1)
2022-12-06 00:00:00
```

```python
date_2 = pd.to_datetime("20221206".format = "%Y%m%d")
date_2
Timestamp('2022-12-06 00:00:00")
```

---

### sample data 생성 

```python
def random_series(dts):
    res = pd.Series(np.random.randn(len(dts)), index=dts)   
    return res
```  


- Timestamp를 이용해 시간 객체 생성 

```python
ts = pd.Timestamp("2022-01-01 00:00")
s_1 = pd.Series(100, index = [ts])
s_1
```
- 2022-01-01 100
- dtype: int 64
 
```python
random_series(s_1)
```
- 100 -0.103219
- dtype: float 64

### Time series의 함수들 
- date_range : 시작일과 종료일 또는 시작일과 기간을 입력하면 범위 내의 인덱스 생성 
  
```
s: 초
T: 분
H: 시간 
D: 일 
B: 주말이 아닌 평일 
W: 주(일요일)
W-MON: 주(월요일)
M: 각 달의 첫날 
BM: 주말이 아닌 평일 중에서 각 달의 마지막 날 
BMS: 주말이 아닌 평일 중에서 각 달의 첫날
WOM-2THU: 각달의 두번째 목요일
Q-JAN: 각 분기의 첫달의 마지막 날 
Q-DEC: 각 분기의 마지막 달의 마지막 날 
```

```
dts = pd.date_range 2023-01-01, 2023-12-31, freq="B"
print(dts)
주말이 아닌 평일이 출력된다
```

### 시계열 데이터에서의 indexing과 slicing
날짜 슬라이싱은 본인까지 포함함

- 후행
shift(1)

-선행
shift(-1)

---

### 간격 재조정 

- resample: 시간 간격을 재조정하는 resampling 가능 

```
xx .resample()
재조정 날짜 뒤에 .agg함수 가능합니다
```

### dt 접근자 
- datetime 자료형 시리즈에는 dt 접근자존재
- datetime 자료형이 가진 몇 가지 유용한 속성과 메서드를 사용할 수 있다.

```python 
'2022-01-01, 2022-01-02'

.strftime("%Y년 %m월 %d일 입니다")
'2022년 01월 01일 입니다. 2022년 01월 02일 입니다. 
```
  