---
title: "구글 드라이브에 단어 검색을 이용해 이미지 크롤링 하기"
date: 2020-04-27
categories: Crawling Python
---

친구와 코드를 공유하고, 부족한 노트북의 성능을 보완하기 위해 해당 코드는 Colab(코랩)으로 개발하였습니다.
[코랩](https://colab.research.google.com/notebooks/intro.ipynb#recent=true)은 구글에서 주피터 노트북 환경을 구글 서버에서 작동할 수 있도록 개발되었습니다.
구글 드라이브에서 간단히 연동하여 사용할 수 있고, 딥러닝 등 여러 자원이 필요한 개발을 진행할 때 사용되기도 합니다.

저는 구글 드라이브에 마운트해 사진을 편하게 크롤링 한 후, 클라우드 환경에서 다운로드 받아 활용하기 위해 해당 방법을 이용하였습니다.

### 1. 구글 드라이브에 마운트(mount)하기
사실 remount하는 코드를 작성하지 않아도 되는데, 자꾸 불필요한 오류가 마운트 과정 중 오류가 발생하여.. 다음과 같이 코드를 작성하였습니다.
구글 드라이브에 경로를 마운트할 수 있게 도와주는 코드입니다.

```py
from google.colab import drive
import os

if os.path.exists('/content/gdrive')==False:
  drive.mount('/content/gdrive')
  print('Google Drive is mounted\n')
else:
  # 자꾸 오류 나서 remount 하는 방향으로 진행 
  drive.mount('/content/gdrive', force_remount=True)
  print('Google Drive is remounted\n')
```


### 2. 다운받을 목록을 가져옵니다.
저의 경우 가져오고 싶은 목록이 존재하였기 때문에 따로 불러와서 배열에 저장해주는 작업을 거쳤습니다.
제가 불러온 categories.txt는 검색할 단어(=categories)가 300개 이상으로 꽤 배열이 길었기 때문에 해당 방법으로 불러왔습니다.
만약 불러올 검색어가 짧다면 해당 과정은 스킵해도 될 것 같습니다.

```py
f = open("categories.txt","r")
# And for reading use
classes = f.readlines()
f.close()

classes = [c.replace('\n','').replace(' ','_') for c in classes]
print(classes)
print('Number of classes: ' + str(len(classes)))
```


### 3. 크롤링 진행하기
저는 저작권 무료 이미지 사이트 중 하나인 [stocksnap](https://stocksnap.io/)에서 크롤링 하기로 했습니다.
stocksnap의 경우 검색어 결과 주소창이 stocksnap.io/search/검색어 의 형태로 보이는 것을 확인했습니다.
그래서 검색어에 아까 만든 class를 넣어 다운받는 방법으로 진행했습니다.


크롤링을 하려고 하던 중 403에러에 막혔는데, 간단히 header를 추가하여 해결할 수 있었습니다.
requests 요청을 하게 되면 비정상적 접근으로 생각하기 때문에 header를 사용하여 유저 정보로 정상적 접근을 시도하는 것이라 합니다.


개발자 도구로 들어가 분석한 결과 제가 원하는 그림 파일은 모두 photo-grid-item 클래스의 img src에 속해있는 것을 알 수 있었습니다.
그렇게 찾은 이미지 소스 주소를 urlretrieve 함수를 이용하여 몽땅 다운받아주었습니다!
함수를 이용해 크롤링을 진행하게 되므로, get(숫자)로 간단히 다운을 받을 수 있게 됩니다. 

```py
import urllib.request
import urllib.parse
import requests
from bs4 import BeautifulSoup
from urllib.error import URLError, HTTPError

def get(count = 1):
  try:
      # header : to avoid 403 error
      header = {'User-Agent': 'Mozilla/5.0'}
      base_url = 'https://stocksnap.io/search/'

      # colab의 categories 에서 뽑아와서 자동으로 검색 후 다운로드 하는 과정
      for i in range(345):
        plus_url = classes[i]
        url = base_url + urllib.parse.quote_plus(plus_url)
        
        print('Crawling starts..')
            
        req = urllib.request.Request(url, headers = header)
        html = urllib.request.urlopen(req).read()
            
        soup = BeautifulSoup(html, 'html.parser')
        img = soup.find_all(class_='photo-grid-item')

        # Getting and downloading images
        for i in range(count):
          try:
              print('--- %s no.%d ---'%(plus_url, i))
              img_src = img[i].find(('img'))['src']
              #print(img_src)
              urllib.request.urlretrieve(img_src, plus_url+'_'+str(i)+'.jpg')
          except IndexError as e:
            continue
        print('Crawling ends...')

  # Finding Errors
  except HTTPError as e:
    print(e)
```

저는 get(8)로 8개만 다운 받는 것을 진행하였고 다음과 같이 구글 드라이브에 다운이 되는 것을 확인할 수 있답니다.
[image](https://user-images.githubusercontent.com/43411599/80313705-aca7c680-8827-11ea-9904-43926b214fc0.png)


처음 크롤링을 도전해보는 것이었는데, beautifulSoup만을 이용하여 간단히 다운받아보았습니다.
곧 크롤링을 또 사용해볼 일이 있을 것 같은데.. 그땐 더 나은 코드를 짤 수 있기를..
