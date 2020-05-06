---
title: "[Python, JS]프린터 풀이(프로그래머스 Lv.2)"
date: 2020-05-06
categories: Python algorithm programmers JavaScript
---

제가 프로그래머스를 이용하면서 가장 많이 보는 메세지입니다. 바로 <b>틀렸습니다!</b>죠.
![fail](https://user-images.githubusercontent.com/43411599/81142611-1607a200-8fab-11ea-94c0-a9e89ca2b948.png)

왜 이 문제를 해결하는데 오래 걸렸을까요? 수정을 해나가며 변경된 과정을 작성해보았습니다.
아래는 처음에 생각했던 코드입니다.

```py
def solution(priorities, location):
    for i in range(len(priorities)):
        for j in range(len(priorities)):
            if priorities[i] < priorities[j]:
                popped = priorities.pop(0)
                priorities.append(popped)
                location += 1
                break

    if location > len(priorities):
        location %= len(priorities)
    return location
```

제공된 테스트 케이스의 경우 정상적으로 작동해서 자신있게 제출을 눌렀지만 결과는 <b>실패</b>였습니다.
총점 15%으로 찍어도 그것보단 더 많이 맞았겠다.. 정도의 결과가 나왔습니다....
제공된 테스트 케이스 만으로는 문제를 해결할 수 없다고 판단하고 새로운 예외를 찾기로 했습니다.
이럴 때는 프로그래머스 사이트에서 더 많은 테스트 케이스를 제공해주면 좋겠다는 생각을 하지만 직접 생각하면 성장할 거라 믿고 생각해보기로 했습니다.


일단은 주어진 priorities 배열이 모두 같은 우선 순위를 가질 때 였습니다.
![same_priorities](https://user-images.githubusercontent.com/43411599/81143569-1d2faf80-8fad-11ea-84c0-a917a8d698ba.png)
또한 먼저 프린트된 우선 순위의 경우, 제대로 출력되지 않는 문제를 발견했습니다.
![after_print](https://user-images.githubusercontent.com/43411599/81145018-574e8080-8fb0-11ea-9c18-753e9b9cf20f.png)

---
처음부터 다양한 테스트 케이스를 고려하여 작성을 하면 좋겠지만, 테스트 케이스만 보고 하다보면 거기에만 집중에서 이런 일이 일어나는 것 같습니다.
index를 고려하지 않아서 문제가 발생하는 것을 알게 되었고 다른 방법을 고민하였습니다.
처음엔 인덱스를 따로 튜플로 받아 저장하는 방법을 고려하다가 새로운 변수를 늘리지 않고 그냥 가지고 있는 location 함수를 살리게 되었습니다.
기존의 겹쳐진 for 문으로는 pop() 함수 이용시 사용 하기가 어려워 while문으로 변경하게 되었습니다.
배열 내 이동이 발생할 경우 location 함수를 업데이트 해주었습니다.
가장 큰 숫자는 반복문 1회당 1번씩 업데이트 하여 사용해보았습니다.

```py
def solution(priorities, location):
    answer = 0
    max_num = max(priorities)

    while len(priorities) > 0:      
        if priorities[0] == max_num:    # 첫번째 인자가 가장 큰 숫자라면
            answer += 1                 # 총 출력 횟수 +1
            priorities.pop(0)           # pop(0) 
            if location == 0:           # 그런데 그것이 원하는 숫자라면
                return answer           # answer를 반환
            else:
                location -= 1           # 그렇지 않으면 앞에 것이 사라졌으므로 location - 1
                
        elif priorities[0] < max_num:            # 만약 더 큰 숫자가 있다면
            priorities.append(priorities.pop(0)) # 가장 앞의 숫자를 맨 뒤에 삽입
            if location == 0:                    # 해당 숫자가 가장 앞에 위치했을 경우(원하는 숫자이고)
                location = len(priorities) - 1   # location을 새로 추가한 인자의 위치로 변환
            else:
                location -= 1                    # 만약 가장 앞에 있는 숫자가 원하는 숫자가 아니라면 location-1
        max_num = max(priorities)                # max_num 변수 업데이트를 위한 줄
    return answer
```

사실 처음에 코드를 작성할 때 별 생각않고 위의 코드를 조금만 변경하면 되지 않을까? 하면서 글을 작성하며 코드를 수정하기 시작했는데 끝이 너무 다르네요.
😅 화이팅..!
