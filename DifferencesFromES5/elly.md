# ECMAScript5 vs ECMAScript6(2015)
***
ECMAScript5에서 ECMAScript6로 업데이트되면서 달라진 점은 무엇인가에 대해서 알아보려고 합니다.


1. const와 let
   es5 - var
   es6 - const, let, var

   ● const(block scope)
   변수 재선언 X
   변수 재할당 X
   ex) const test = "ma,ba,sa"; //변수 선언하면서 값을 할당해야 에러 안남

   ● let(block scope)
   변수 재선언 X
   변수 재할당 O

   ● var(function scope)
   변수 재선언 O
   변수 재할당 O

   const, let은 block scope(if문, for문, while문 등) 내에서 선언하면 그 안에서만 사용 가능. 외부에 영향 주지 않음.
   var는 block scope 내에서 선언해도 전역 변수로 인식됨.

2. class
   prototype 기반

   class 선언 - 먼저 선언 후 사용
   ex)
   class band{
        constructor(te, st){
            this.te = te;
            this.st = st;
        }
   }

   class 표현식
   ex)
   //이름이 없을 때
   const apple = class{
        constructor(a, b){
            this.a = a;
            this.b = b;
        }
    }

    //이름이 있을 때
    const cherry = class cherry{
        constructor(c, d){
            this.c = c;
            this.d = d;
        }
    }

3. 화살표 함수(arrow fuction)
   IE 제공하지 않음(babel 필요).

   함수에 매개변수가 하나라면 괄호 생략가능.

   function을 생략해도 됨.
   ex)
    (function(){
        //es5
    }())

    (() => {
        //es6
    })()

    call, apply 사용할 수 없음.

    arguments 존재하지 않음.

    this를 바인딩하지 않음.