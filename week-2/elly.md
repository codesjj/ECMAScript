# ECMAScript

### 1. Arrow Function 사용법, this가 가르키는 것
```js
*Aroow Function 사용법

//ES5
setTimeout(function(){
    console.log("No");
}, 1000);

function testFFn(i){
    console.log("es5 함수"+i);
}
testFFn(333); //es5 함수333

//ES6 화살표 함수
setTimeout(()=>{
    console.log("No");
}, 1000);

const testFn = i =>{
    console.log(`화살표 함수 ${i}`);
}
testFn(42729); //화살표 함수 42729

const zip = () => {...} //매개변수가 없을 때
const zip = x => {...} //매개변수가 하나일 때
const zip = (x, y) => {...} //매개변수가 여러 개일 때

const zip = x => { return x; }
const zip = x => x; // 함수의 블록이 한줄이라면 중괄호와 return을 생략

const sum = (x, y) => {
    return x + y;
}
console.log(sum(1, 2)); //3


*this가 가리키는 것
-화살표 함수에서는 this가 무조건 상위 스코프의 this를 가리킨다.
=> 정적인 방식으로 this 바인딩 (Lexical this)

//화살표 함수를 사용하면 안 되는 경우
-메소드 정의, 프로토 타입에 메소드 할당할 경우
=> 메소드를 소유한 객체가 아닌 전역객체 window에 바인딩.
-생성자 함수로 사용할 경우
=> 화살표 함수는 프로토타입 프로퍼티를 갖고 있지 않다(인스턴스 생성할 수 x).
-addEventListener 함수의 콜백 함수(탭모듈 같은 click 했을 때 해당 객체를 가져와야하는 경우)
=> 화살표 함수를 사용할 경우 전역 객체 window에 바인딩.
```

### 2. Class
함수. 함수를 함수 선언과 함수 표현식으로 정의할 수 있듯이 class 문법도 class 선언과 class 표현식 두가지 방법으로 정의 가능.

```js
//class 선언
class pepper{
    constructor(name){
        this.name=name;
    }

    say(){
        console.log(`my name is ${this.name}`);
    }
}

//class 표현식
const pepper = class pepper{
    constructor(name){
        this.name=name;
    }

    say(){
        console.log(`my name is ${this.name}`);
    }
}

이름을 가질 수도 있고,

const pepper = class{
    constructor(name){
        this.name=name;
    }

    say(){
        console.log(`my name is ${this.name}`);
    }
}

이름을 갖지 않을 수도 있음.
```

### 3. Class set, get
```js
*set(setter) - 어떤 프로퍼티에 **접근할 때마다** 프로퍼티를 조작하는 행위가 필요할 때 사용.

*get(getter) - 어떤 프로퍼티에 **값을 할당할 때마다** 프로퍼티를 조작하는 행위가 필요할 때 사용.

실제 데이터에 직접 접근하지 않고 정의된 오퍼레이션을 통해서만 접근함(캡슐화의 이점인 정보 은닉).
get, set을 통해 접근함으로써 변수 보호.
```

*set, get 참조링크<br>
http://guswnsxodlf.github.io/javascript-class-and-prototype-1<br>
https://mygumi.tistory.com/161