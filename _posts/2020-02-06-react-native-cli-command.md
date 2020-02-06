---
title: "Mac 맥 환경에서 React Native cli 시작하기"
date: 2020-02-06
categories: React-Native
---

리액트 네이티브 공부를 짬내서 하고 있습니다. 설치와 관련된 글은 많이 올라와있어서 참고하시면 되는데 저의 경우 
[이 글](https://dev-yakuza.github.io/ko/react-native/install-on-mac/)을 주로 참고하였습니다.

저는 리액트 네이티브에서 기본으로 제공하는 api 외에 다른 api를 함께 사용하기 위해서 react native cli를 사용하기로 결정하였습니다.
이 글은 그래서 react native cli 기준으로 작성되었습니다.

1. 맥북에서 리액트 네이티브 프로젝트 시작하기
```
npm start
react-native init 프로젝트 이름
```

2. ios 디바이스 실행하기 (일단 해당 프로젝트 폴더로 cd 명령어를 이용해 이동)
```
npx react-native run-ios
```

3. Android 디바이스 실행하기
일단, 안드로이드 스튜디오 실행후 Configure -> AVD Manager를 이용해 에뮬레이터 실행 후 명령어 입력
AVD는 Android Virtual Device를 의미한다.
```
npx react-native run-android
```

+) 실행이 잘 된다면, App.js 파일을 수정하며 코드를 확인할 수 있게 된다! R+R을 누르면 된다고 했는데 나의 경우, 디폴트 값이
저장후 자동 적용으로 되어있는지 그냥 수정 후 저장하니 바로 적용되었다.
아직 아는 것이 많이 없어 일단은 docs에서 예제를 보면서 따라하고 있다.

<img width="397" alt="스크린샷 2020-02-06 오후 5 50 33" src="https://user-images.githubusercontent.com/43411599/73920921-b77a4b80-4909-11ea-8cbb-2f481cf2dc30.png">
