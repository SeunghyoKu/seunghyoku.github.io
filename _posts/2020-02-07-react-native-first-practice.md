---
title: "React Native 첫번째 실습: 버튼과 텍스트 만져보기"
date: 2020-02-07
categories: React-Native
---

리액트 네이티브 docs를 읽으면서 이것저것 만져 보면서 학습한 결과물을 올립니다.
간단하게 버튼과 텍스트를 이용해보았습니다.
리액트 네이티브로 만든 첫번째 앱이 되겠네요!

<img width="395" alt="스크린샷 2020-02-06 오후 7 49 05" src="https://user-images.githubusercontent.com/43411599/73930526-fc0de300-4919-11ea-9d81-026a2021d227.png">

버튼을 클릭하면 alert 메세지가 뜨는 간단한 어플입니다.


### 1. bold 체 적용하기 
평소에도 **굵은** 글씨를 좋아하기 때문에 이것부터 먼저 적용해보았습니다.

```react
<Text style=`{{fontWeight:'bold'}} > 단번에 </Text>
```

fontWeight를 이용해서 적용해주면 됩니다.
텍스트 안에 새로운 텍스트를 넣고, 거기에 스타일을 적용하는 형식입니다.


### 2. italic 체 적용하기
강조를 위해 *기울인* 글씨를 적용하고 싶을 때 사용하면 됩니다.
```react
<Text style=`{{`fontStyle:'italic'`}}`>당신은 행운아입니다. {'\n'}</Text>
```

위와 똑같이 적용하나, fontStyle을 이용해서 italic으로 지정해주면 됩니다.
참고로 엔터 효과를 내고 싶다면 {“\n”}을 삽입해주면 됩니다.


### 3. 버튼에 동작 넣기

```react
_onPressButton() {
    alert('지금 당장요!')
  }
  _onPressButton2() {
    alert('그럴리가요!')
}
```

위처럼 render() 위에서 한 번 함수를 정해놓은 다음 아래와 같이 사용해주면 됩니다.

```react
<Button
  onPress={this._onPressButton2}
  title="집에 가고 싶지 않나요?"
  color="steelblue"
/>
```

여기서의 styles는 아래와 같이 자바스크립트를 이용하며, 스타일 적용을 편하게 해준다고 합니다.
하나하나 적용할 수 있지만, 이렇게 작성하면 확실히 더 편할 것 같습니다.

```react
const styles = StyleSheet.create({
  container: {
   flex: 1,
   justifyContent: 'center',
  },
  buttonContainer: {
    margin: 20
  }
}
```
