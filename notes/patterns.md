# 자주 쓰는 패턴 템플릿 모음

설명은 최소화하고, "복붙 가능한 템플릿" 중심으로만 기록한다.  
패턴은 내가 실제로 사용한 것만 남긴다.

---

## BFS (최단거리/레벨 탐색)
언제: 무가중치 최단거리, 격자 탐색

템플릿:
```python
from collections import deque

q = deque([(sx, sy)])
visited = [[False]*m for _ in range(n)]
visited[sx][sy] = True

dist = 0
while q:
    for _ in range(len(q)):
        x, y = q.popleft()

        # TODO: 목표 체크

        for dx, dy in dirs:
            nx, ny = x + dx, y + dy
            if not (0 <= nx < n and 0 <= ny < m):
                continue
            if visited[nx][ny]:
                continue
            if not can_go(nx, ny):
                continue

            visited[nx][ny] = True  # enqueue 시점
            q.append((nx, ny))
    dist += 1
````

주의:

* visited는 enqueue 시점에 처리
* 레벨(dist) 필요 없으면 dist 블록 제거

---

## DFS (백트래킹)

언제: 조합/순열/부분집합/경로탐색

템플릿:

```python
def dfs(idx):
    if idx == n:
        # TODO: 결과 처리
        return

    picked[idx] = True
    dfs(idx + 1)

    picked[idx] = False
    dfs(idx + 1)
```

주의:

* 깊이 크면 recursionlimit 또는 iterative 고려
* 전역 상태 되돌리기 누락 주의

---

## Two Pointers (투 포인터)

언제: 정렬/단조성을 이용해 구간 조건 만족

템플릿:

```python
arr.sort()
l = 0
s = 0

for r in range(len(arr)):
    s += arr[r]
    while l <= r and s > target:
        s -= arr[l]
        l += 1
    # TODO: 조건 만족 시 답 갱신
```

주의:

* 조건이 단조로워야 성립
* (>, >=) 경계값 정확히

---

## Prefix Sum (누적합)

언제: 구간합 다수 질의

템플릿:

```python
ps = [0]
for x in arr:
    ps.append(ps[-1] + x)

# [l, r] 구간합 (0-index)
range_sum = ps[r + 1] - ps[l]
```

주의:

* 인덱스 정책 확정(0/1-index)

---

## Binary Search (답 탐색)

언제: check(mid)가 단조성일 때

템플릿:

```python
lo, hi = 0, 10**9
ans = hi

while lo <= hi:
    mid = (lo + hi) // 2
    if check(mid):
        ans = mid
        hi = mid - 1
    else:
        lo = mid + 1
```

주의:

* 단조성(check가 True -> True로 유지되는지) 검증이 핵심

---

## Dijkstra (가중치 최단거리, 음수 X)

언제: 양의 가중치 최단거리

템플릿:

```python
import heapq

INF = 10**18
dist = [INF] * (n + 1)
dist[start] = 0
pq = [(0, start)]

while pq:
    d, v = heapq.heappop(pq)
    if d != dist[v]:
        continue
    for to, w in graph[v]:
        nd = d + w
        if nd < dist[to]:
            dist[to] = nd
            heapq.heappush(pq, (nd, to))
```

주의:

* 음수 가중치 있으면 사용 금지
* (d != dist[v]) 스킵 필수

---

## Counter / 빈도 카운팅

언제: 빈도 기반 문제(최빈값, 그룹핑, 아나그램 등)

템플릿:

```python
from collections import Counter
cnt = Counter(arr)
# cnt[x], cnt.most_common()
```

주의:

* 키가 없을 때 기본값 처리가 깔끔해짐