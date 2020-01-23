# ECMAScript
## 1. var를 사용하면 안되는 이유.
for문에서 var를 이용하여 변수를 만들 경우,
루프가 끝난 후에 변수가 유지되어 코드의 예측이 어렵고,
var를 이용하여 동일한 변수명으로 중복 선언할 수 있어서 중복 체크를 하지않으면,
미리 만들어 놓은 코드의 변수가 변경될 위험성도 가지고 있습니다.

## 2. Arrow Function 사용법, this에 변화

### 2-1. Arrow Function 사용법
```js
// 1. Arrow Function Default Type
const Default_Arrow_fx = () => {
    console.log('Default_Arrow_fx');
}
// 2. Arrow Function one Argument
const oneArgument = (a) => {
    console.log(a);
}
// 2. Arrow Function more than two Argument
const moreThanTwoArgument = (a, b) => {
    const c = a + b;
    console.log(c);
}
// 2. Arrow Function return
// 2-1. Multiple lines
const multiple_lines_fx = (a, b) => {
    const c = a - b;
    const d = a + b;
    console.log(c + d);
    return c + d;
}
// 2-1. one line
const one_line_fx = (a, b) => a + b;

Default_Arrow_fx();
oneArgument(1);
moreThanTwoArgument(1,3);
multiple_lines_fx(1,5);
one_line_fx(1,2);
```

### 2-2. this에 변화

자바스크립트의 경우 함수 호출 방식에 의해 this에 바인딩할 어떤 객체가 동적으로 결정됩니다. 
화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정됩니다.
동적으로 결정되는 일반 함수와는 달리 화살표 함수의 this 언제나 상위 스코프의 this를 가리킵니다.
이를 Lexical this라 합니다.

```js

var innerFunction = function(fn){
    fn();
}

// ES5 function에서는 `this` Scope가 function안에 들어가면 변하기 때문에 새로운 변수를 만들어 씁니다.
var outerFunction = function(){
    console.log(this);

    innerFunction(function(data) {
        console.log(this);
    });
}
new outerFunction();

// // ES6 Arrow Function에서는 `this` Scope의 변화가 없기 때문에 `this`를 그대로 사용하면 됩니다.
var outerFunction2 = function(){
    console.log(this);

    innerFunction((data) => {
        console.log(this);
    });
}
new outerFunction2();

```

### 2-3. 화살표 함수를 사용하면 안되는 경우.
#### 2-3-1. 메소드
* 화살표 함수의 경우 메소드를 호출한 객체를 가르키지 않기 때문에 화살표 함수로 메소드를 정의하는 것은 옳지않습니다.
```js
    var object_es5 = {
        to : 'es5',
        me : function(){
            console.log(this.to);
        }
    }

    object_es5.me();
    // es5

    var object_es6 = {
        to : 'es6',
        me : () => {
            console.log(this.to);
        }
    }

    object_es6.me();
    // undefined
```

#### 2-3-2. prototype
```js
    var object_es5 = {
        to : 'es5',
    }

    Object.prototype.es5 = function(){
        console.log(this.to);
    }

    object_es5.es5();
    // es5

    var object_es6 = {
        to : 'es6',
    }

    Object.prototype.es6 = () => {
        console.log(this.to);
    }

    object_es6.es6();
    // undefined
```

#### 2-3-3. 생성자 함수
생성자 함수는 prototype 프로퍼티를 가지며 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor를 사용합니다.
하지만 화살표 함수는 prototype 프로퍼티를 가지고 있지 않습니다.
```js
const Foo = () => {};

// 화살표 함수는 prototype 프로퍼티가 없다
console.log(Foo.hasOwnProperty('prototype')); // false

const foo = new Foo(); // TypeError: Foo is not a constructor
```

#### 2-3-4. addEventListener 함수의 콜백 함수
이벤트가 바인딩된 요소를 가르키지 않고 window를 가르킵니다.
```js
    const button = document.getElementById('mybutton');

    button.addEventListener('click', () => {
        console.log(this);
        // window
    });
```

## 3. Default parameter values
es5에서는 인자를 모두 사용하는 계산식이 있는데, 인자를 모두 전달하지않으면 계산을 할 수 없었습니다.
es6에서는 그러한 것을 방지하기 위하여 기본값을 설정할 수 있도록 추가되었고,
기본값을 설정함으로써 인자를 모두 던지지 않아도 기본값을 사용할 수 있게 변경되었습니다.

```js
    var defaultParameter_es5 = function(a, b){
        return a * b;
    }

    console.log(defaultParameter_es5(1));
    // b를 전달하지 않아 NaN 이 반환.

    const defaultParameter_es6 = (a, b=5) =>{
        return a * b;
    }

    console.log(defaultParameter_es6(1));
    console.log(defaultParameter_es6(1, 4));
```

## 4. Template Literals
백틱(` `)(grave accent) 을 이용하여 표현할 수 있습니다.

### 변수 사용
${}를 사용하여 변수를 바로 사용할 수 있습니다.
```js
    const a = 10;
    let b = 20;
    
    console.log(` 두 수의 합은 ${a + b}`);
```

### 여러줄 처리
es5에선 /n 을 통해 줄바꿈을 하였지만, 템플릿 리터널에서는 바로 줄바꿈을 할 수 있습니다.
```js
    const a = 10;
    let b = 20;
    
    console.log(` 두 수의 합은
    ${a + b}`);
```

### 템플릿 리터럴 안에서 백틱을 빠져나올 때
백슬러쉬(\)를 넣어서 빠져나올 수 있습니다.

```js
`\`` === "`" // --> true
```

### 백틱으로 함수전달

```js
    let name = 'jj';
    let age = 20;
    
    function templateFn(strings, _n, _a){
        console.log(strings);
        //strings은 띄어쓰기 마다 배열로 담겨집니다
        console.log(_n);
        console.log(_a);
    }

    templateFn`이렇게 ${name}과 ${age}를 보낼 수 있습니다`;
```

## 참고
<a href="https://poiemaweb.com/es6-arrow-function">https://poiemaweb.com/es6-arrow-function</a>
<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals">https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals</a>