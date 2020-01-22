<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>ES6 두번째, 시간</title>
</head>
<body>
    ES6
    1. ES6에서, var를 사용하면 안되는 이유
    2. ES6에서 화살표함수의 사용법 (this 변화)
    3. Default parameter values
    4. ES6에서의 템플릿 리터럴

    1.
    - VAR같은 경우 함수레벨스코프, LET/CONST 같은경우 블록레벨스코프 
    - 함수 레벨 스코프(Function-level scope)
        함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, 함수 내부에서 선언한 변수는 지역 변수이며 함수 외부에서 선언한 변수는 모두 전역 변수이다.

      블록 레벨 스코프(Block-level scope)      
        모든 코드 블록(함수, if 문, for 문, while 문, try/catch 문 등) 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다. 즉, 코드 블록 내부에서 선언한 변수는 지역 변수이다.
        
    - let 블록스코프, 재할당 및 재선언 스코프
    EX ) 
        // var의 경우
        var a = 1
        a = 2
        console.log(a) // 2
        var a = 3
        console.log(a) // 3
        
        // let의 경우
        let b = 1
        b = 2
        console.log(b) // 2
        let b = 3 // SyntaxError: Identifier 'b' has already been declared
        
        // const의 경우
        const c = 1
        c = 2 // TypeError: Assignment to constant variable    
    - 상수의 사용법
    EX ) 
        // 10의 의미를 알기 어렵기 때문에 가독성이 좋지 않다.
        if (rows > 10) {
        }
        
        // 값의 의미를 명확히 기술하여 가독성이 향상되었다.
        const MAXROWS = 10;
        if (rows > MAXROWS) {
        }    

    2. 
    - 함수가 한줄로 표현이 가능할 때, 중괄호 생략가능하고, 리턴값이 없어도 자동리턴됌 (매개변수가 한개일때는 괄호생략가능)
    - ES5 this : 내부함수에서의 this는 window 바인딩한다.
    EX ) 
        ES5 this의 내부함수 바인딩
            function Person() {
                this.age = 0;
                console.log(this); // Person { age: 0 }
            
                setTimeout(function growUp() {    
                console.log(this); // window
                this.age++; // NaN
                }, 1000);
            }         
            var p = new Person();

        ES5 tihs의 내부함수 바인딩 해결법
            function Person() {
                var that = this;
                that.age = 0;
                console.log(this); // Person { age: 0 }
            
                setTimeout(function growUp() {
                that.age++; // age = 1
                console.log(that); // Person { age: 1 }
                }, 1000);
            }
            var p = new Person();

        ES6 this 바인딩
            const Person = () => {
                this.age = 0;
                console.log(this.age); // 0
            
                setTimeout(() => {
                this.age++; // 1
                console.log(this.age); // 1
                }, 1000);
            }
            Person();
        - 화살표함수를 사용하지 말아야 할 경우
        EX ) 
        객체의 메소드를 정의할 때
            const obj1 = {
                name : 'Lee',
                sayName : () => {console.log(`hi + ${this.name}`);}
            };
            obj1.sayName();
        위와 같이하면 객체의 this를 바인딩하지 않고 전역 객체가 바인딩된다.

        이런식으로 정의해줘야 한다.
            const obj = {
            name: 'Lee',
                sayHi() { // === sayHi: function() {
                    console.log(`Hi ${this.name}`);
                }
            };            
            obj.sayHi(); // Hi Lee
              
    3. default parameter은 함수에 전달된 파라미터의 값이 undefined이거나 전달된 값이 없을 때, 초기화 설정된 값을 말합니다.
    - API 같은 경우 필요한 파라미터만 전달하도록 만들어져있으므로 전달받은 값이 없을 경우 기본적으로 나머지는 0 으로 처리해서 연산하도록 해야한다. 이것을 기본 파라미터 설정이라 하는데, 아래와 같이 할 수 있다.
    EX ) 
        ES5 
            function addNum(a, b){
                console.log(a + b); // NaN
                console.log(a); // 5
                console.log(b); // undefined
            }
            addNum(5);    
        ES6 
            var addNum = (a = 0, b = 0 ) => { // 파라미터 기본값을 설정함.
                console.log(a + b);  // 5
                console.log(a); // 5
                console.log(b); // 0 기본값
            }
            addNum(5);    

    4.
    - 템블릿 리터럴(백틱)은 작은따옴표'', 큰따옴표""를 혼용할 수 있다.
    - +연산자를 따로 사용하지 않아도, 문자열을 삽입할 수 있다.  (인터폴레이션) ES5에서의 \n 을 따로 안해도 가능해진다.
    EX ) 
        const template = `<ul class="nav-items">
            <li><a href="#home">Home</a></li>
            <li><a href="#news">News</a></li>
            <li><a href="#contact">Contact</a></li>
            <li><a href="#about">About</a></li>
        </ul>`;    
    - 문자열 인터폴레이션은 ${...}으로 표현식을 감싼다.
    EX )
        const first = 'Ung-mo';
        const last = 'Lee';
        
        // ES5: 문자열 연결
        console.log('My name is ' + first + ' ' + last + '.');
        // "My name is Ung-mo Lee."
        
        // ES6: String Interpolation
        console.log(`My name is ${first} ${last}.`);
        // "My name is Ung-mo Lee."

    5. 디스트럭쳐링 (배열)
    - https://jeong-pro.tistory.com/118?category=799620
</body>
</html>