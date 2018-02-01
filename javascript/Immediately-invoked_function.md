# 즉시 실행 함수

> 2018/02/01

```js
(function(a){
  console.log(a)
})('a')
// a
```

자바스크립트에서는 위와 같이 익명 함수를 선언하고 즉시 실행하는 것이 가능하다.

이 때 즉시 실행이 가능한 조건은, 함수가 값으로서 사용되는 것이다.

```js
function(a){
  console.log(a);
}('1');
// Syntax Error...

function(){

};
// Syntax Error...
```

위 두 경우에서 에러가 나는 이유는 익명 함수의 선언이 실패했기 때문이다.

익명 함수가 값으로서 참조되고 있지 않기 때문에 선언 자체에서 실패하는 것.

```js
!function(a){
  console.log(a);
}('1');
// 1
```

위 코드는 익명 함수를 unary 오퍼레이터 !의 인자로 줌으로써 값으로 사용하고 있다. 따라서 정상적으로 실행된다.

---

### Reference

> 함수형 자바스크립트 프로그래밍 - 유인동 저