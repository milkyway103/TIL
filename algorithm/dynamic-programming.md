동적 계획법 (dynamic programming)
=================================

---

-	큰 의미에서 분할 정복과 같은 접근 방식
-	동적 계획법과 분학 정복의 차이 : 문제를 나누는 방식
-	어떤 부분 문제는 두 개 이상의 문제를 푸는 데 사용될 수 있기 때문에, 한 번 계산한 결과를 **재활용** -> 속도의 향상
-	캐시(cache) : 이미 계산한 값을 저장해 두는 메모리 장소
-	중복되는 부분 문제(overlapping subproblem) : 두 번 이상 계산되는 부분 문제
-	어떤 문제에 overlapping subproblem이 있으면 계싼의 중복 횟수는 분할의 깊이가 깊어질수록 지수적으로 증가 (조합 폭발; combinatorial explosion)<br>
-	이항 계수 문제 (binomial coefficient) : n개의 서로 다른 원소 중에서 r개의 원소를 순서없이 골라내는 방법의 수

**overlapping subproblem이 발생하는 코드**

```python
def bino(n, r):
  # 기저 사례 : n=r (모든 원소를 다 고르는 경우) 혹은 r=0 (고를 원소가 없는 경우)
  if (r==0 or n==r):
    return 1
  return bino(n-1, r-1) + bino(n-1, r)
```

-	이 문제를 동적 계획법으로 해결할 수 있는 이유 : 입력인 n과 r이 정해져 있을 때 `bino(n, r)`의 반환 값이 일정하다!
-	각 n,r 조합에 대해 답을 저장하는 캐시 배열을 만들어 각 입력에 대한 반환 값을 저장
-	함수는 매번 호출될 때마다 이 배열에 접근해 값이 저장되어 있는지 확인
-	저장되어 있다면 이를 즉시 반환
-	저장되어 있지 않다면 직접 계싼하여 배열에 써넣고 반환
-	**메모이제이션(memoization)** : 함수의 결과를 저장하는 장소를 마련해 두고, 한 번 계산한 값을 저장해 뒀다 재활용하는 최적화 기법

**동적 계획법으로 효율성을 높인 코드**

```python
cache = dict()
def bino2(n, r):
  # 기저 사례
  if (r==0 or n==r):
    return 1
  # 저장되어 있다면 한 번 계산했던 값이니 곧장 반환
  # 저장되어 있지 않다면 직접 계산한 뒤 배열에 저장
  return cache.get((n, r), bino2(n-1, r-1) + bino2(n-1, r))
  # 저장되어 있다면 한 번 계산했던 값이니 곧장 반환
```

-	수학에서는 입력이 같다면 출력도 항상 같음
-	프로그래밍에서는 그렇지 않음 : 함수의 입력 외에도 전역 변수, 입력 파일, 클래스의 멤버 변수 등 수많은 입력에 의해 작동
-	참조적 투명성(referential transparency) : 함수의 반환 값이 그 입력 값만으로 결정되는지의 여부
-	참조적 투명 함수(referential transparent function) : 입력이 고정되어 있을 때 그 결과가 항상 같은 함수들 (위의 `bino`, `bino2`는 참조적 투명 함수)

### 메모이제이션 구현 패턴

1.	기저 사례를 제일 먼저 처리 (입력이 범위를 벗어난 경우 등)
2.	cache를 특정 값으로 초기화 (아직 계산되지 않았음을 알려줌)
3.	cache에 접근할 때 참조형 변수를 사용

### 메모이제이션의 시간 복잡도

`존재하는 부분 문제의 수` :heavy_multiplication_x: `한 부분 문제를 풀 때 필요한 반복문의 수행 횟수`

References
----------

프로그래밍 대회에서 배우는 알고리즘 문제해결 전략