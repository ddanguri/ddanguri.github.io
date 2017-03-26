---
layout: post
category: javascript
title: Javascript_더 안전한 자바스크립트 코딩
---

### 1. 재귀함수 사용 시 arguments.callee를 쓰자

```Javascript
function factorial(num){
  if(num <= 1) return 1;
  else return num * factorial(num-1);
}

var temp_factorial = factorial;
factorial = null;
temp_factorial(4); // Uncaught TypeError: factorial is not a function

```

코드를 보면 기존에 factorial 변수에 null을 할당했으므로 함수안에서 다시 factorial을 실행하려 하므로 오류가 발생합니다. arguments.callee는 현재 실행 중인 함수를 가리키는 포인터이므로 아래와 같이 바꾸면 올바르게 동작합니다.

```Javascript
function factorial(num){
  if(num <= 1) return 1;
  else return num * arguments.callee(num-1);
}
```

### 2. 배열의 length 속성은 최대 인덱스에 하나를 더한 값이다.

```Javascript
var a = ["dog","cat","rabbit"];
a[100] = "pig";
console.log(a.length); // 101

console.log(typeof a[5]); //"undefined"
console.log(typeof a[99]); //"undefined"
```
for문 사용 시 아래와 같이 사용하는 것이 효율적입니다.
반복문에서 거짓으로 취급되는 항목('undefined') 을 발견하면 루프는 멈춥니다. 따라서 위의 코드와 같이 undefined가 포함된 배열에서 사용하면 올바르게 작동하지 않습니다.

```javascript
for (var i = 0, item; item = a[i]; i++) {
    // item 으로 뭔가를 수행
}
```


배열에 항목을 추가할 때는 아래와 같이 추가 하는 것이 안전합니다.
```Javascript
array[array.length] = item;
```
