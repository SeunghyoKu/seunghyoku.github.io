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
+) 사실 이 단계에서 뻘짓을 굉장히 오래했는데, 안드로이드 에뮬레이터가 안되서.. 계속 헤매다가.. 독스를 읽어보니 28 버전을 써야 한다고
적혀있었다. --; 맥을 처음 쓰다보니.. path 설정을 잘못했나 해서 zshrc파일 계속 고치고 있었는데 애초에 avd 부터 잘못 사용하고 있던 것..
혹시 안되시는 분들은 저처럼 헤매지 말고 docs부터 읽고 하시길 강력 추천해드립니다.

