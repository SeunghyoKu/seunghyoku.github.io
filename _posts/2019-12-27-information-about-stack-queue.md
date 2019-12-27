---
title: "스택(Stack)과 큐(Queue) 파이썬으로 생각해보기"
date: 2019-12-27
categories: Python DataStructure
---

- 스택(Stack): LIFO(Last In First Out) 구조
데이터의 입력(Push), 출력(Pop)이 가능합니다.

예시) 접시를 쌓는다고 생각했을 때, "처음 쌓은 것은 가장 나중에" "마지막에 쌓은 것은 가장 먼저" 꺼낼 수 있습니다.
사용 방법)

```py
# 스택을 쌓을 리스트 선언
stack_list= []

# 리스트에 1, 2, 3을 차례로 입력(push)
stack_list.append(1)
stack_list.append(2)
stack_list.append(3)

# 마지막에 넣은 값을 반환하면서 삭제(pop) = 하나씩 빼는 과정
stack_list.pop()
```

- 큐(Queue): FIFO(First In First Out) 구조
데이터의 입력(Push), 사용(Get)이 가능합니다.

예시) 놀이공원 줄을 먼저 선 사람이 먼저 놀이기구를 타게 됩니다.
사용방법)

```py
# 큐를 넣을 리스트 선언
queue_list = []

# 리스트에 1, 2, 3을 차례로 입력
queue_list.append(1)
queue_list.append(2)
queue_list.append(3)

# 리스트에 처음으로 넣은 값 출력
# 리스트의 0번째를 출력한다는 뜻
queue_list.pop(0)
```

