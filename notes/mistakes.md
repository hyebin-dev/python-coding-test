# 자주 틀리는 포인트(오답노트)

오답 노트는 "감정"이 아니라 "재발 방지 규칙"만 적는다.  
한 문제당 5줄 이내로 유지한다.

---

## 기록 템플릿(고정)
- 날짜:
- 문제ID:
- 링크:
- 원인(한 줄):
- 방지 규칙(한 줄):
- Tags: (2~4개)

---

## 자주 터지는 실수 예시(참고용)
- 원인: list로 큐 구현(pop(0))해서 시간초과
  방지: BFS/큐는 deque로 고정
  Tags: bfs, deque, tle

- 원인: visited를 pop 시점에 처리해서 중복 enqueue 폭발
  방지: visited는 enqueue 시점에 처리
  Tags: bfs, visited, queue

- 원인: dict key 없는데 바로 접근해서 KeyError
  방지: get() / defaultdict 사용
  Tags: dict, keyerror

- 원인: 슬라이싱을 반복문 안에서 과하게 사용해 시간초과
  방지: 인덱스로 처리하거나 누적합/투포인터로 변경
  Tags: slicing, complexity, tle
