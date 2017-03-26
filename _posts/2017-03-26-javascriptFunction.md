---
layout: post
category : javascript
title: Javascript_Function 총정리
---

### 들어가기에 앞서
웹개발자에게 자바스크립트를 할 줄 아냐고 물어보면 100이면 100 할 줄 안다고 대답할 것 같습니다. 저 또한 그렇습니다. 하지만 정말 잘 아는 것이냐고 물어본다면 또 그렇지는 않습니다. 이 포스트는 다시 한번 저를 담금질하기 위함에 첫 번째 목적이 있고, 조금이라도 도움이 될 누군가를 위해 기록합니다.


### 1. 자바스크립트 함수는 객체다.

자바스크립트에서 함수는 가장 중요하면서도 흥미로운 존재이자, Java나 C를 주로 다루는 개발자에게는 생소한 존재이기도 합니다. 자바스크립트의 함수의 특징을 가장 간단하게 한 문장으로 표현하자면 아래와 같습니다.

```
자바스크립트에서 함수(Function)은 객체입니다.
```

처음 이 말을 접했을 때, 저는 '아, 그렇구나.' 했습니다. 이러한 개념을 바로 인정하고 받아들였다는 것이 아닙니다. 그때의 전 별 생각이 없었습니다. 아마 다른 똑똑한 분들은 의아해하거나, 어째서? 라는 의문을 가졌을지도 모르겠습니다.

자바스크립트의 함수가 객체라는 말은 앞으로 내가 만들 모든 함수가 Function 타입의 인스턴스라는 말이기도 합니다. 객체이므로 참조 타입이라고 할 수 있으며, 프로퍼티와 메서드를 가지고 있습니다. 함수 이름은 단순히 함수 객체를 가르키는 포인터 역할을 합니다.

아래는 일반적으로 볼 수 있는 기본적인 함수의 형태입니다. function 뒤에 함수이름을 사용하여 함수를 선언하는 방식입니다.

```js
function add(x,y){
  return x+y;
}
```

이 함수는 아래와 같이 사용할수도 있습니다. 코드를 보면 add라는 변수에 function을 할당하였습니다. 이는 다른 말로 함수는 객체이며 변수 add는 함수를 가르키는 포인터라고 할 수 있습니다. 이렇게 작성한 함수는 함수 객체 자체에 이름이 없어 익명 함수(anonymous function) 라고도 합니다.

```js
var add = function(x,y){
  return x+y;
};
```
이렇게 변수에 할당할 때는 보통 다른 값을 할당할 때와 마찬가지로 끝에 세미콜론을 추가합니다.

이렇게 함수에는 두 가지 리터럴 형태가 있지만 중요한 차이점이 있습니다. 처음 방식처럼 함수를 선언하는 방식은 코드가 실행될 시점에 [호이스팅](https://developer.mozilla.org/ko/docs/Glossary/Hoisting) 된다는 점입니다.
다시 한번 설명하자면, 자바스크립트 엔진은 코드를 평가할 때 제일 먼저 함수 선언을 찾은 다음 이들을 맨 위로 올립니다. 즉, 함수 선언이 소스코드에서 함수 실행부분보다 뒤에 있더라도 함수 선언부분을 끌어올립니다(hoisting). 호이스팅에 관해선 추후 따로 다시 정리할 예정입니다.

즉, 아래와 같은 코드가 있더라도 실행될 때 함수 선언부가 호이스팅되기 때문에 오류가 나지 않고 함수가 실행되게 됩니다.

```js
add(10+20); // 함수 실행, 결과값 : 30

function add(x+y){ //함수 선언부
  return x+y;
}
```


다시 함수이름이 단순히 포인터라는 이야기로 돌아오겠습니다.
아래 코드를 보면 방금 만든 add를 copy_add에 할당하였습니다. 그리고 add에 null을 할당하였지만, copy_add는 여전히 함수를 가리키고 있으므로 정상적으로 결과를 출력하게 됩니다.

```js
var copy_add = add;

add = null;

console.log(copy_add(10,20)); // 30
```

### 함수의 오버로딩은 없다.

대부분의 객체지향 언어에서는 이름이 같은 함수에 변수타입 및 개수에 따른 오버로딩을 지원합니다. 하지만 자바스크립트는 불가능합니다. 이를 이해하기 위해서는 함수의 매개변수가 실제로는 배열과 비슷한 객체인 arguments 에 저장된다는 사실을 알아야 합니다. 이 arguments는 함수 안에서 자동으로 만들어지며, 다시 얘기하면 이름이 있는 매개변수는 편의상 둔 것일 뿐 함수에 전달할 수 있는 인수의 개수는 제한이 없다는 뜻이기도 합니다.

```js
function add(x,y){
  return x+y;
}

console.log(add(5,3));   //8
console.log(add(5,3,1)); //8
console.log(add());      //NaN
```

위의 소스에서 확인할 수 있듯이, 매개변수를 몇 개를 넘겨도 에러가 나지 않습니다. 매개변수를 더 많이 넘겼을 때 1은 무시되었으며, 하나도 넘기지 않았을 때는 x와 y가 undefined로 설정되므로 더하기 연산에서 NaN을 출력하게 됩니다.

결국 이러한 특성은 모든 것이 arguments에 저장이 되기 때문인데요, 따라서 add 함수를 이렇게 표현할수도 있습니다.

```js
function add(){
  return arguments[0] + arguments[1];
}
```

이제 실제로 오버로딩이 되는지 확인해 볼 차례입니다.

```js
function printMsg(msg){
  console.log(msg);
}

function printMsg(){
  console.log('no message');
}

printMsg('message'); //no message
```

오버로딩이 지원되지 않으므로 printMsg라는 함수는 마지막에 정의된 함수가 처음 정의된 함수를 덮어썼습니다. 따라서 'no message'를 출력하게 됩니다.


### 참고자료 및 관련링크
- [프론트엔드 개발자를 위한 자바스크립트 프로그래밍](http://book.naver.com/product/go.nhn?bid=7204207&cpName=aladdin&url=http%3A%2F%2Fwww.aladin.co.kr%2Fpart%2Fwgate.aspx%3Fk%3DyX0iVru1r6MZd1dA4HlGejY2Ue8syl%26sk%3D641696%26u%3D%252Fshop%252Fwproduct.aspx%253FISBN%253D8966260764)
- [객체지향 자바스크립트의 원리](http://book.naver.com/product/go.nhn?bid=7204207&cpName=aladdin&url=http%3A%2F%2Fwww.aladin.co.kr%2Fpart%2Fwgate.aspx%3Fk%3DyX0iVru1r6MZd1dA4HlGejY2Ue8syl%26sk%3D641696%26u%3D%252Fshop%252Fwproduct.aspx%253FISBN%253D8966260764)
- [Javascript : 함수(function) 다시 보기](http://www.nextree.co.kr/p4150/)
