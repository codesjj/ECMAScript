# ECMAScript

1. var를 사용하면 안되는 이유.

다른 개발자가 같은 변수명을 의도치 않게 중복해서 사용할 수 있기 때문에 큰 어플리케이션을 만들거나 협업을 할 경우 문제가 생길 수 있다(중복된 var 변수는 나중에 선언된 것으로 덮어쓰게 됨).


2. Arrow Function 사용법, this에 변화

● Arrow Function
//함수 표현식
function(){}

//화살표 함수 표현식
()=>{}


● this
화살표 함수는 this를 정의하지 않음.
함수의 내부함수에 사용되는 this는 window.

3. Default parameter values

function multiply(a, b){
    return a*b;
}

multiply(5, 2); //10
a, b 값이 다 제공됐을 경우 제대로 나오지만

multiply(5); //NaN !
b 값이 제공되지 않았을 경우 NaN이 반환됨.

이걸 방지하기 위해

function multiply(a, b){
    b = (typeof b !== 'undefined') ? b:1;
    return a*b;
}
multiply(5, 2); // 10
multiply(5); // 5

multiply 함수가 한 개의 인수만 있을 경우 b를 1로 설정하는 방식을 사용했었는데, ES6에서는 기본 매개변수가 생겼음.

function multiply(a, b = 1){
    return a*b;
}

multiply(5, 2); //10
multiply(5); //5
multiply(5, undefined); //5

4. Template Literals

