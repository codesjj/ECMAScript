# ECMAScript

## 1. Arrow Function 사용법, this가 가르키는 것
### 기존의 This
기존의 this는 실행될 때 자신을 호출한 요소를 가르키는 this를 생성한다.

### Arrow Function의 This
arrow에서의 this는 자신만의 this를 생성하지 않는다.<br>
즉 상위에 존재하는 window를 가르킨다.

### Test Code
```html
    <button type="button" id="elly">elly</button>
    <button type="button" id="ch">ch</button>
```

```js
    function Fn(){
        // 함수 실행하면 Fn을 호출한 요소는 window이다
        console.log('*************');
        console.log('function에서의 this');
        console.log(this);
    }

    var obj = {
        self : function(){
            // 객체의 메서드를 실행하면 호출한 요소는 객체이다
            console.log('*************');
            console.log('객체에서의 this');
            console.log(this);
        }
    }

    Fn();
    //console.log(window.Fn);
    console.log('*************');

    obj.self();
    //console.log(window.obj.self)
    console.log('*************');
    // 즉 this는 실행될 때 자신을 호출한 요소를 가르키는 this를 생성한다.

    var arrow_obj = {
        self : () => {
            console.log('*************');
            console.log('객체에서 arrow function에서의 this');
            console.log(this);
        }
    }

    arrow_obj.self();
    //console.log(window.arrow_obj.self);
    // arrow에서의 this는 자신만의 this를 생성하지 않는다
    // 즉 상위에 존재하는 window를 가르킨다.
    console.log('*************');


    document.getElementById('elly').addEventListener('click', function(){
        // 자신을 호출한 요소인 button을 this로 생성한다.
        console.log(this);
    });

    document.getElementById('ch').addEventListener('click', () => {
        // 자신을 호출한 요소를 this로 생성하지 않고, 상위의 this를 가르킨다.
        console.log(this);
    });
```

## 2. Class
### Class란
Class란 함수라고 볼 수 있다. ( 관련된 함수들의 집합체 )

### Class 정의 방법
#### 선언식
```js

class testClass {
    ...
}

```
<br>

#### 표현식
```js
var testClass = class {
    ...
}

```
> 클래스는 호이스팅이 되지 않습니다.
<br>

### Constructor (생성자)
class에는 하나의 constructor를 가질 수 있습니다.<br>
constructor는 생성자 메소드로써 class 객체를 생성하고 초기화합니다.<br>
따라서 class 내에서 공통으로 사용하는 속성들을 객체에 저장시키는 것에 유용합니다.

```js
class testClass {
    constructor(a, b){
        // 공통으로 사용하는 속성들을 저장
        this.test = 'test';
        this.yo = b;
    }
}

var test = new testClass(4, 5);
console.log(test.yo);

```

### Static methods
static 키워드는 클래스를 위한 정적(static) 메소드를 정의합니다.<br>
클래스의 인스턴스화(instantiating) 없이 호출되며,<br>
인스턴스에서는 호출이 불가능합니다.

```js
class testClass {
    constructor(a, b){
        this.test = 'test';
        this.yo = b;
    }

    static testStatic(a, b){
        return a - b;
    }
}

var test = new testClass(4, 5);
// test라는 testClass 인스턴스 생성
console.log(test.testStatic());
// test라는 인스턴스에서는 호출 불가능
console.log(testClass.testStatic(4, 5));
// 인스턴스가 아닌 클래스에서 직접 호출
```

### Instance properties
인스턴스 속성은 반드시 클래스 메서드 내에 정의되어야 합니다.<br>
정적 (클래스사이드) 속성과 프로토타입 데이터 속성은 반드시 클래스 선언부 바깥쪽에서 정의되어야 합니다. 

```js
class testClass {
    constructor(height, width) {    
        this.height = height;
        this.width = width;
    }

    testFn(){
        console.log(this.staticWidth);
        console.log(this.prototypeWidth);
    }
}


var test = new testClass();

testClass.staticWidth = 20;
// ?? 
testClass.prototype.prototypeWidth = 25;

test.testFn();
```

### extends
class를 정의할 때 extends를 이용하여 다른 class의 메소드들을 상속받을 수 있습니다.

```js
class aClass {
    constructor(name) {    
        this.name = name;
    }

    Fn(){
        console.log(this.name + ' : aClass');
    }
}

class bClass extends aClass {
    Fn(){
        console.log(this.name + ' : bClass');
    }
}
var bC = new bClass('target');
bC.Fn();

// es5에서 사용되던 prototype 기반의 함수도 상속 가능
function Animal (name) {
  this.name = name;  
}
Animal.prototype.speak = function () {
  console.log(this.name + ' makes a noise.');
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}

var d = new Dog('Mitzie');
d.speak();

// 일반 객체의 경우 extends로는 상속이 불가능하며,
// Object.setPrototypeOf() 메소드를 통하여 상속을 할 수 있습니다.
var Animal = {
  speak() {
    console.log(this.name + ' makes a noise.');
  }
};

class Dog {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(this.name + ' barks.');
  }
}
Object.setPrototypeOf(Dog.prototype, Animal);

var d = new Dog('Mitzie');
d.speak();

```
### Species


### super
super를 이용하여 부모요소의 메소드를 실행할 수 있습니다.

```js
class aClass {
    constructor(name) {    
        this.name = name;
    }

    Fn(){
        console.log(this.name + ' : aClass');
    }
}

class bClass extends aClass {
    Fn(){
        super.Fn();
        console.log(this.name + ' : bClass');
    }
}
var bC = new bClass('target');
bC.Fn();
```
### Mix-ins

?..

## 3. set, get

> 메소드 축약 

```js

    //es5
    var test = {
        fn_1 : function(){
            console.log(1);
        },
        fn_2 : function(){
            console.log(1);
        }
    }

    //es6
    var test2 = {
        fn_1(){
            console.log(1);
        },
        fn_2(){
            console.log(1);
        }
    }

```

## 참고
<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes">https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes</a>
<a href="https://beomy.tistory.com/14">https://beomy.tistory.com/14</a>
<a href="https://beomy.tistory.com/15">https://beomy.tistory.com/15</a>