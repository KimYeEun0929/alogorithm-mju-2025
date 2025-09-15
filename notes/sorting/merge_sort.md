### sort algorithm

![algorithm running time](image.png)

## 1. merge sort

# 1) 문제/목표: 무엇을 계산? 입력/출력 명세

- 입력: 길이가 n인 배열 A[1:n]
- 출력: 오름차순으로 정렬된 배열 A

# 2) 아이디어 한 줄: 핵심 직관(분할-정복/그리디/DP 등)

- 분할-정복: 배열을 반으로 나눠 각각 정렬 -> 두 정렬된 부분배열을 병합(merge)하며 전체를 정렬

# 3) 의사코드(5~15줄): 핵심만

```
Merge-Sort(A, p, r):
    if p>=r: return
    q = ⌊(p+r)/2⌋
    Merge-Sort(A, p, q)
    Merge-Sort(A, q+1, r)
    Merge(A, p, q, r)
```

```
Merge(A, p, q, r):  // A[p..q], A[q+1..r] 는 이미 정렬
    i ← p; j ← q+1
    B ← new array of length (r - p + 1)
    k ← 0
    while i ≤ q and j ≤ r:
        if A[i] ≤ A[j]: // 동률 시 왼쪽을 먼저 택해 "안정성" 보장
            B[k] ← A[i]; i ← i+1
        else:
            B[k] ← A[j]; j ← j+1
        k ← k+1
    while i ≤ q: B[k] ← A[i]; i ← i+1; k ← k+1
    while j ≤ r: B[k] ← A[j]; j ← j+1; k ← k+1
    copy B[0..k-1] back into A[p..r]
```

# 4) 정확성 스케치: 루프 불변식/귀납 증명 요지 3줄

- (분할) 길이 1은 자명하게 정렬
- (정복) 귀납가정: 길이 < n의 배열은 `Merge-Sort`가 올바르게 정렬
- (결합) `Merge`는 두 정렬된 배열을 안정적으로 하나의 정렬 배열로 만든다
- 따라서 길이 n도 정렬된다.

# 5) 복잡도: T(n) 점화식 → 해, 공간복잡도

- 점화식: $T(n) = 2T(n/2) + O(n) -> T(n) = O(nlogn)$ (최선/평균/최악 동일)
  ![running time](image-2.png)

- 추가 공간: O(n) (보조 배열)
  ![merge-sort](image-1.png)

# 6) 함정/엣지케이스: 3가지

    - 안정성: 병합에서 동률 시 왼쪽(≤) 을 먼저 복사해야 유지.

# 7) 연결 개념: 함께 보면 좋은 개념(예: 안정정렬, 하한)
