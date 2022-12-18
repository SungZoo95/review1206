# 선형대수학 

---

``` 
a1x1 + a2x2 +a3x3 = 4 - 선형
a1x1 + a2y1 + a3z3 = 5 - 선형
```
스칼라를 2개이상 엮으면 백터
백터를 모으면 매트릭스
매트릭스를 모으면 텐서 
```
3 *스칼라
(3,4) * 2차원벡터
(3,4,5) * 3차원 벡터 
[[3,4,5], [6,7,8]] = 1R3 x 1R3 (3차원과 3차원이 결합된 매트릭스)
```
---

## 벡터 

- 행백터와 열백터 

- 벡터의 거리 측정방법
```
p = 1 v = (3,4,5)
|v| = (3**1+4**1+5**1)
p = 2 
|v| = (3**2+4**2+5**2)**1/2
```
p = 1 이면 마름모로 거리가 측정 

- L1 norm
    - 절대값으로 두 벡터 간의 거리를 구한다.
    - 맨해튼 거리 (밑변*높이)
- L2 norm
    - 유클리드 거리 (대각)
- 유사도 
    - 코사인 유사도
        - 두 벡터가 이루는 각도를 통해 유사도 측청
        - 최대1,최소 -1의 값을 갖는다
        - 같은 방향일수록 유사하다. 
  
---

## 행렬 
R은 실수를 의미함. 
- 주요 용도 
    - 연립 방적식의 해법 
    - 병렬로 연산가능하다.
매트릭스는 문장의 유사도를 측정가능하다.
- 주의사항 
    -행렬 곱하기는 행과 열의 개수가 맞아야함 
- 단위행렬
    - 대각선으로 1이되는 행렬
- 전치 행렬 
    -  행과 열을 바꾼다.

