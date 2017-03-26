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
