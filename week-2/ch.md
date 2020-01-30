# ES6 CLASS문법, this

1. CLASS문법

JavaScript **Class**는 ECMAScript 6을 통해 소개되었습니다. 
ES6의 Class는 기존 prototype 기반의 상속을 보다 명료하게 사용할 수 있도록 문법을 제공합니다. 
이를 Syntatic Sugar라고 부르기도 합니다. (Syntatic Sugar : 읽고 표현하는것을 더 쉽게 하기 위해서 고안된 프로그래밍 언어 문법을 말합니다.)

#### CLASS문법은 함수 선언과 달리 클래스 선언은 호이스팅이 일어나지 않기 때문에,
#### 클래스를 사용하기 위해서는 먼저 선언을 해야합니다. 그렇지 않으면 ReferenceError 가 발생합니다.
#### 클래스 선언과 클래스 표현식의 본문(body)은 strict mode 에서 실행됩니다.
#### 즉, 이 문서에 적힌 코드는 엄격한 문법이 적용되기 때문에 strict mode가 아닌 상태에서는 무시 되는 오류가 발생합니다.

클래스나 객체에 함수가 할당되면, 그것은 method라고 불립니다.
클래스에서 객체가 생성되면, 클래스의 인스턴스(instance)라고 불립니다.

```
    // Reference Error가 일어나는 경우
    const yun = new Student(); // Student클래스가 선언되지 않았는데 호출

    class Student {}
```

**여기서 알아야 할 것, 객체를 생성할 때는 "new"를 꼭 써야한다, constructor 메서드**
*constructor(){...} , 생성자 메서드는 객체 인스턴스를 생성하고 초기화할 수 있는 특수한 메서드다.*
*생략가능하지만 생략하면 자동으로 빈 constructor(){} 메서드가 삽입된다.*
*** 클래스의 멤버변수를 생성 및 초기화할 때는 반드시 constructor() 메서드에 작성해야 한다. ***

```
    //ES5
        var Person = (function () {
        // Constructor
        function Person(name) {
            this._name = name;
        }

        // method
        Person.prototype.sayHi = function () {
            console.log('Hi! ' + this._name);
        };

        // return constructor
        return Person;
    }());

    var me = new Person('Lee');
    me.sayHi(); // Hi! Lee.

    console.log(me instanceof Person); // true

    // 프로토타입 문법으로 객체를 정의할 때에는 함수(객체)를 만든 뒤에 그 함수의 이름으로 생성자를 만들고, 
    // 프로토타입을 설정하고, 객체의 생성자를 변수에 담았다. 
    //sayHi 함수를 하나만 만들어 객체의 인스턴스들이 재활용하기 위해서 프로토타입 안에 정의해 주었다.    
```
```
    //ES6
        class Person {
            constructor(name) {
                this._name = name;
            }

            sayHi() {
                console.log(`Hi! ${this._name}`);
            }
        }

        const me = new Person('Lee');
        me.sayHi(); // Hi! Lee

    console.log(me instanceof Person); // true
    //클래스 문법에는 constructor라는 생성자 메소드가 있고, 프로토타입 안에 설정되었던 sayHi 함수는 그냥 클래스의 scope에 정의되었다.
```

2. Class Get (Getter), Set(Setter)

    일반적으로 프로그래밍을 할 때,
    객체들의 데이터(필드)를 외부에서 직접적으로 접근하는 것을 막아놓습니다.

    필드들을 private 접근 제한자로 막아두고,
    각 필드의 Getter, Setter로 접근하는 방식을 사용합니다.

    이렇게 프로그래밍 하는 이유는 **객체의 무결성(캡슐화의 이점인 정보 은닉이 된다.)**을 보장하기 위함입니다.

```
// class Person { 
//     constructor(name, age) {
//          this._name = name;
//           this.age = age;
//         }
//         get name() {
//              return this._name.toUpperCase(); 
//             } 
//         set name(newName){
//             if(newName){
//                 this._name = newName; 
//                 } 
//             } 
//         } 
//     let man = new Person('John', 10); 
//     console.log(man.name, man.age); 
//     man.name = 'John Park'; 
//     man.age = 20; 
//     console.log(man.name, man.age);
```

```
    //변수의 직접적으로 접근
    class Time { 
        constructor(start, end) { 
            this._start = start;
            this._end = end; 
            this._duration = end - start;
            }
        } 

    const time = new Time(0, 20); 
    time._start = 5; 
    time._duration -= 5;
    console.log(time._duration)
```
```
    //getter, setter를 통해 접근
    class Time { 
        constructor(start, end) { 
            this._start = start; 
            this._end = end; 
            this._duration = end - start 
        } 
        setStart (newStart) { 
            this._start = newStart; 
            this._duration = this._end - this._start; 
        } 
        getStart() { 
            //return this._start; 
            return this._duration; 
            }
        } 
    const time = new Time(0, 20); 
    time.setStart(6); 
    console.log(time.getStart());    
```