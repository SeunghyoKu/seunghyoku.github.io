---
title: "Git 초보 적응기"
date: 2020-05-25
categories: Git Hanium
---


깃을 공부해봐야지, 그래 해봐야지 말을 해도 혼자나 학과 친구들과 팀 프로젝트를 진행하다 보면 다른 방법으로 코드를 교환할 방법이 많다보니 배울 기회가 잘 없었습니다.
한이음 ICT 멘토링에서 관련 프로젝트를 진행하게 되었는데, 한이음 쪽에서는 `GitLab`을 사용할 것을 권장해주었습니다.
나를 포함한 멘티가 4명, 멘토님이 1명이니 총 5명이 확인하고 관리해야 하다보니 Git 사용은 필수적이었습니다.


한 번도 뵌 적 없는 분이지만 어째서인지 자주 들어가게 되어 혼자만의 친밀도가 형성된 [초보몽키님의 개발 블로그](https://wayhome25.github.io/git/2017/07/08/git-first-pull-request-story/)
글을 멘토님께서 추천해주셔서 참고하게 되었습니다!
자세하게 설명되어 있으니 Github 사용법을 알고 싶으신 분들은 이 글을 확인해주세요.


이렇게 여러 사람이 하나의 프로젝트를 진행하는 경우, 바로 pull request를 하기 보다는,
개인 계정에 fork를 해온 후 로컬에서 작업한 후 그 작업물을 pull request 해주어야 합니다.
한 번 기본 파일에 작성되어 있는 print("Hello World")를 실행하여 출력해보겠습니다.


> Gitlab 실 사용기


- fork 버튼을 눌러줍니다.


fork는 한글 뜻으로 식기인 포크 외에도, '갈라지다'라는 뜻을 가지고 있습니다.
다른 사람의 코드를 변경하고 싶을 때, 해당 repository를 내 저장소의 repository로 동일하게 복사해옵니다.

  
![fork버튼](https://user-images.githubusercontent.com/43411599/82769374-3ff80a00-9e6f-11ea-89c7-3900d6cd8f21.png)


아래의 사진처럼 제 저장소에 잘 복사된 것을 확인할 수 있죠?


![fork후내저장소](https://user-images.githubusercontent.com/43411599/82770377-4e482500-9e73-11ea-8c21-641e33b6a28a.png)


- clone 버튼을 눌러줍니다.


![clone버튼](https://user-images.githubusercontent.com/43411599/82770772-b2b7b400-9e74-11ea-9b76-5b3138536d70.png)


clone with HTTPS의 주소를 복사한 후, 터미널을 켜고 아래와 같이 입력해주세요. (Mac 기준)


```git clone 복사한주소```


![clone되는중](https://user-images.githubusercontent.com/43411599/82770884-2c4fa200-9e75-11ea-9bba-2d183156284a.png)


해당 주소를 새롭게 원격 remote를 지정하려 했으나 아래와 같은 오류가 발생했습니다.


`fatal: not a git repository (or any of the parent directories): .git`


> 프로필에 SSH 추가하기


위에 뜬 안내 메세지를 확인하니 GitLab의 경우 개인 프로필에 SSH 코드를 등록하지 않을 경우, 해당 링크를 제대로 사용할 수 없다고 합니다.
만약 저와 같은 오류가 뜨지 않는 분은 스크롤을 내려서 계속 진행해주시면 됩니다.
캡처 상에 보이는 `generate one`을 클릭해주었습니다.


![프로필에서 SSH 만들기](https://user-images.githubusercontent.com/43411599/82772339-d6312d80-9e79-11ea-94e6-962431be9c9c.png)


맥의 경우엔 terminal을 켜고, 아래와 같이 입력해주세요. 키를 먼저 만들게 됩니다.


`ssh-keygen -t ed25519 -C "email@example.com`


그 다음엔 만든 키를 프로필에 등록해주면 됩니다. 저와 같은 경우는 아래 명령어를 입력해 나온 결과를 직접 프로필에 복붙해주었습니다.


`cat /.ssh/id_ㅇㅇ.pub`


> 원본 프로젝트 remote repository로 추가하기


`git remote add 별명 주소`


설정이 잘 되었는지 확인하려면 다음과 같은 명령어를 입력하여 확인하실 수 있습니다.


`git remote -v`


> 로컬에서 branch 생성하기


branch 즉 가지를 만들어서 코드를 작성하게 되면 원본 파일에는 영향을 끼치지 않고 수정 작업을 할 수 있습니다.
로컬에서 작업하게 되기 때문입니다.
아래와 같이 입력하게 되면 해당 이름을 가진 branch 가 만들어지는 것을 확인할 수 있습니다.
git checkout -b 명령어는 해당 branch를 생성한 후, 전환하는 기능까지 포함합니다.


`git checout 브랜치이름` 


`git checkout -b 브랜치이름`


만약 만들어진 branch가 궁금하다면, `git branch`를 입력해 어느 branch가 있는지 확인할 수 있습니다.


> 직접 실행해보기


![직접 실행해보기](https://user-images.githubusercontent.com/43411599/82781740-95471200-9e95-11ea-9521-4c6f7cd85676.png)


가져온 파일과 똑같이 hello world가 잘 출력되었습니다.


> 수정한 파일 Staging에 추가하기


이 과정을 제하고 push를 진행하게 되면, 아무 변동 사항 없이 내 저장소에 업데이트 되게 됩니다.
git add 함수를 사용하여 스테이징 영역에 추가한 후 push, 그 후 pull하는 과정을 진행하면 됩니다.
저는 하나의 파일만을 수정하여 해당 파일 명 만을 입력하여 staging 영역에 추가하였습니다.


`git add 해당파일`


만약 수정된 모든 파일을 추가하고 싶다면, -A를 붙여서 사용하시면 됩니다.


`git add -A`


현재 add 내용을 확인하고 싶다면 `git status` 명령어를 사용합니다.


참고로 staging을 취소하고 싶을 때는 `git reset` 명령어를 사용한다고 합니다.


> Commit 진행해보기


깃헙에 글을 올리면서도.. 버튼이 아닌 터미널로 commit은 진행해본 적이 적습니다.
해당 수정사항에 대해 commit 을 진행하고 싶을 때는 git commit 명령어를 사용합니다.
-m은 메세지의 약자입니다.


`git commit -m "수정한 내용들"`


> 내 저장소에 push 하기


git push 명령어를 사용하여 저장소에 push할 수 있습니다.
저는 아래의 명령어를 통해 origin이라는 원격 저장소에 master 브랜치에 push 하였습니다.


`git push origin master`
`git push 저장소 브랜치이름`


> 머지 리퀘스트 해보기


![merge 시도](https://user-images.githubusercontent.com/43411599/82782951-726a2d00-9e98-11ea-8a1f-02961d8e6f4b.png)


자 이제 이 값을 merge request 해보도록 하겠습니다.
첫 번째 request가 되겠군요!
많이 헤맸는데 캡처에 보이는 부분을 작성한 후 완료해보겠습니다.


![작성](https://user-images.githubusercontent.com/43411599/82783038-a5142580-9e98-11ea-9fb7-1b025720a37c.png)


작성이 완료되었습니다.


> 머지가 끝난 후 branch 삭제하기


merge가 끝난 branch를 삭제하려면 git branch -d 명령어를 작성하면됩니다.
참고로 현재 선택되어있는 branch의 경우 삭제가 불가능하니, 다른 branch로 전환해주신 후 삭제를 진행해야 됩니다.


`git branch -d 삭제할브랜치이름`


만약, 완전히 merge되지 않은 branch를 삭제하고 싶은 경우에는 대문자 D로 치환하여 작성해주시면 됩니다.

`git branch -D 삭제할브랜치이름`


