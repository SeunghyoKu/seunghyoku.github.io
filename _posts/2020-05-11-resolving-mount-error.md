---
title: "구글 드라이브 Mount가 되지 않을 때"
date: 2020-05-11
categories: Colab Keras
---

오늘 하루도 열심히 코딩해볼까? 하면서 코랩을 켠 당신 !!
그러나 실행하자 보이는 것은 아래와 같은 오류일 수가 있습니다.


``` ValueError: mount failed: timeout during initial read of root folder; ```

바로 제 얘기입니다. :(


![mount_error](https://user-images.githubusercontent.com/43411599/81518653-b417b580-9379-11ea-9ced-43803ca834ab.png)


화면에도 보이는 링크를 따라 들어가보았습니다. 구글 코랩 측에서 작성한 해결 방법이 적혀있습니다.
저의 경우 새로운 폴더를 만들어 실행했음에도 해결이 되지 않았습니다.


![link](https://user-images.githubusercontent.com/43411599/81518982-a4e53780-937a-11ea-8a09-aafb5e0eb581.png)


그 중에서 많은 하위폴더가 있는 곳에 mount 하면.. 이란 글자가 눈에 띄었습니다.
지난번 코딩중 npy를 jpg로 만들며 다운받았던 수만개의 `example_cat_n.jpg`의 이미지 파일이 남아있었습니다.
깜빡하고 지우지 않아 이런 일이 발생했습니다.


![example_cats](https://user-images.githubusercontent.com/43411599/81518722-e9240800-9379-11ea-8a4a-6c130b2b3418.png)


개수가 많아 쉽지는 않았지만 (..) 모두 지워줬습니다. 지워도 지워도 끝이 나지 않지만 몽땅 지워줍니다.
심지어 별도 폴더에 저장하지 않고 My Drive 폴더에 저장하였으므로.. 일일이 하나하나 지워줬습니다. 적어도 폴더에 넣었다면 이런 일은 없었을 텐데..


~~부디 여러분은 이런 일이 일어나지 않기를.. 폴더에 넣는 것을 생활화합시다~~


중간에 다 삭제된 줄 알고 코랩을 실행하였으나, 되지 않아 다시 확인해보니 로딩이 덜 되어.. 안 뜬 것이었으므로 남은 고양이 사진을 삭제했습니다.
코랩 문서에 적힌대로 깔끔하게 휴지통까지 비워줬습니다.
일정 파일 이상 삭제하고 나면 정상적으로 구글 드라이브에 마운트 됨을 확인하실 수 있습니다.

그럼 열공하시길 바랍니다!

