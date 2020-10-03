---
title: "matplotlib을 이용해 csv 파일의 그래프 그리기"
date: 2020-10-04
categories: Python
---

파이썬에서 그래프를 그리고자 할 때 matplotlib을 이용합니다.
그래프를 그릴 데이터는 csv 파일로 불러와서 그려보았습니다.

### 필요한 라이브러리 추가하기

필요한 라이브러리는 `matplotlib`, `pandas` 입니다.
아래와 같이 추가하면 되는데, 조금 더 사용하기 편리하도록 DataFrame을 추가하였습니다.

```py
import matplotlib.pyplot as plt
import pandas as pd
from pandas import DataFrame
```

### 데이터 불러오기

필요한 데이터를 `.readcsv()`를 이용하여 원하는 경로에서 불러옵니다.
저는 loss와 val_loss 그래프를 그려주기 위해서 데이터 값을 불러왔습니다.
물론.. 학습 중에 그릴 수도 있지만, 에포크 중간중간 서버 연결이 끊기기도 했어서 값을 저장한 후 따로 그려주었습니다.

```py
df = pd.read_csv('/content/gdrive/My Drive/Colab Notebooks/loss_graph.csv')
```

아래는 처음 데이터를 불러왔을 때의 모습입니다.

![df_init](https://user-images.githubusercontent.com/43411599/94995261-282c5180-05d8-11eb-9309-6901c8bcd093.png)

### 필요없는 데이터 열 삭제하기

첫 번째 열인 에포크 열이 필요없을 것 같아 삭제해주었습니다.
`drop`을 사용한다면 쉽게 해결됩니다.

```py
df = df.drop(columns=['epoch'])
```

### 그래프 그리기

`pyplot`을 이용해서 그림을 그려봅니다.

- `plot()`: 그래프 그리기
- `xlabel(), ylabel()`: x, y에 라벨 붙이기
- `title()`: 제목 달기
- `xticks(), yticks()`: x, y에 몇 칸 간격으로 표시할 건지 정하기
- `savefig()`: 그래프 저장하기

```py
# 해당 데이터프레임 그리기
plt.plot(df)

# x, y, 타이틀에 라벨 달기 
plt.xlabel('epoch')
plt.ylabel('amount of loss')
plt.title('loss and val_loss graph')

# 표시할 tick 설정하기
plt.xticks([i*10 for i in range(1,11)])
plt.yticks([i*10 for i in range(1,7)])

# 저장하기
plt.savefig('loss_graph.png')
```

![graph](https://user-images.githubusercontent.com/43411599/94995409-0bdce480-05d9-11eb-94d4-c7c85a941605.png)


