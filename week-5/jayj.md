# ECMAScript

## html 에서 왜 script type module을 불러올 수 없는가에 대하여 조사
- 질문자체가 Error 호출 가능<br>
- 다만 로컬에서 호출 시에만 CORS Error 발생<br>

<br>

## 개인과제
<br>

### prototype
```js
// prototype은 쉽게 설명하여 내부에 빈 객체를 하나 만드는 것입니다.

var a =['a', 'b', 'c', 'd'];
console.log(a);
// prototype 존재하지않음.

a.prototype = {}
// prototype 생성, a내부에 빈 객체 생성

a.prototype.name = 'name';
console.log(a);

// 함수의 경우에는 내부에 constructor를 생성하고 prototype도 같이 생성합니다.
function b(){
    console.log(2);
}

console.log(b.prototype);

// https://www.glocaldn.com/common/js/tab_module.js
```


<br>
<br>

## 참고
<a href="https://velog.io/@takeknowledge/%EB%A1%9C%EC%BB%AC%EC%97%90%EC%84%9C-CORS-policy-%EA%B4%80%EB%A0%A8-%EC%97%90%EB%9F%AC%EA%B0%80-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-3gk4gyhreu">https://velog.io/@takeknowledge/%EB%A1%9C%EC%BB%AC%EC%97%90%EC%84%9C-CORS-policy-%EA%B4%80%EB%A0%A8-%EC%97%90%EB%9F%AC%EA%B0%80-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-3gk4gyhreu</a><br>
