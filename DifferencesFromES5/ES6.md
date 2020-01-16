# ECMAScript5 vs ECMAScript6(2015)
***
ECMAScript5에서 ECMAScript6로 업데이트되면서 달라진 점은 무엇인가에 대해서 알아보려고 합니다.

## ES5 / ES6 비교
    
# 추가 및 바뀐점 

    1. let + const
    2. arrows
    3. classes
    4. enhanced object literals
    5. template strings
    6. destructuring
    7. default + rest + spread
    8. iterators + for…of
    9. generators
    10. unicode
    11. modules
    12. module loaders
    13. map + set + weakmap + weakset
    14. proxies
    15. symbols
    16. subclassable built-ins
    17. promises
    18. math + number + string + array + object APIs
    19. binary and octal literals
    20. reflect api
    21. tail calls    


    ES3 > ES4(불편한 단점들이 많으므로, 빠른폐기) > ES5 > ES6(ES5의 단점들을 보완해놓은 버전)

    1. 변수명의 변화 ( VAR / LET / CONST )
    기존에 ES5에서 사용하던 VAR를 대신하여 ES6에는 LET / CONST 라는 변수명이 추가되었는데, LET같은 경우 VAR와 같은 동일한 변수의 기능을 갖고있습니다.
    허나 여기서 흥미롭게 보게될 변수는 CONST이며, 어떻게 보면 변수가 아닌 상수라고 생각하면 됩니다. 상수는 수학적으로 절대값 혹은 변하지않는 값이라고 정의됩니다.
    이는 ES5에서 항상 문제되던 변수의 스코프를 겨냥하여 ES6에 새롭게 추가되었으며, 수많은 코드들을 작성할 때 변수명이 겹치게되어 엉뚱한 곳에서 오류가 나버리는 그러한 경우를 줄여주게 됍니다.

    2. Arrow Function의 추가 (this의 변화)
    ES6를 사용하게 되면 꼭 한번쯤은 사용해보게 될 Arrow Function(화살표함수) 입니다.
    이는 기존에 ES5에서 함수를 사용하려면 앞에 꼭 function 이라는 단어를 작성하여 사용하게 되었는데, ES6에서는 그러한 단어조차 없애버려 깔끔한코드형상을 유지시켜줍니다.

    기존의 함수의 코드
        var ES5 = function(e){
            return x*2;
        }
    새롭게 추가된 화살표함수의 코드
        const ES6 = (e) => {
            return x*2;
        }
    매개변수가 만약 1개의 코드라면, 괄호 생략이 가능해집니다.
        const ES6 = e =>{
            return x*2;
        }
    만약 함수가 한줄로 끝날 수 있는 코드라면, 한줄로도 가능해집니다.
        const ES6 = e =>{return x*2}

    3. Template Literal
         ES6 에서는 템플릿 리터럴을 사용하게되므로써, 코드에 특수문자로 감쌀 필요가 없어졌습니다.

        기존의 ES5
            var name = "위트플러스";
            var age = 27;
            console.log('저의 이름은 " ' + name + ' "이고, 나이는 ' + age + "살 입니다.');
            // 저의 이름은 "위트플러스"이고, 나이는 27살 입니다.    

        새롭게 추가된 ES6 (따옴표)
            let name = "위트플러스";
            let age = 27;
            console.log(`저의 이름은 ${name}이고, 나이는 ${age}살 입니다.`);
            // 저의 이름은 "위트플러스"이고, 나이는 "27"살 입니다.

    4. Class 선언
        ES5에서 클래스 선언은 프로토타입을 통해서 실현됐습니다. ES6에서는 class 키워드를 사용해서 선언할 수 있습니다.

        ES5의 코드
        var Add = function(arg1, arg2) {
            this.arg1 = arg1;
            this.arg2 = arg2;
        };
        
        Add.prototype.calc = function() {
            return this.arg1 + "+" + this.arg2 + "=" + (this.arg1 + this.arg2);
        };
        
        var num = new Add(5, 8);
        console.log(num.calc()); // 5 + 8 = 13

        ES6의 코드
        class Add {
        constructor(arg1, arg2) {
            this.arg1 = arg1;
            this.arg2 = arg2;
        }
        calc() {
            return this.arg1 + "+" + this.arg2 + "=" + (this.arg1 + this.arg2);
            }
        }
          
        var num = new Add(5, 8);
        console.log(num.calc()); // 5 + 8 = 13          

    5. 모듈시스템의 도입
        import / export의 도입, ES5에서는 모듈시스템이라는 개념이 따로 없어, 페이지가 1개일때는 괜찮지만, 페이지가 여러개로 나눠졌을대 각각 불러오는 JS파일들의 관리가 상당히 힘들었습니다.
        그러나 ES6에서는 모듈시스템이 도입이되어, 흔히 React나, Sass 같은 라이브러리등을 사용할때 볼 수 있는 import / export가 도입이 되었는데 각각 불러오다, 내보내다 라는 뜻을 갖고 있습니다.
    
        // 모듈 전체를 export, 파일내 한번만 사용가능하다.
            var module = {};
            export default module


        // 모든 속성을 export
            export *;


        // 함수를 직접 export
            export function moduleFunc() {};
            var property = "some property";
            export {property};

        // 모듈 전체를 import
            import module
            import module as myModule
            
            
        // 모든 속성 import
            import * from module
            
            
        // 특정 멤버(함수 등)만 import
            import {moduleFunc, moduleFunc2} from module            

        // 모듈 전체를 import
            var module = require('./someModule.js')
        
        // 모든 속성 import
        // (위의 module 객체에 모든 속성이 담아져 온다.)
            
        // 특정 멤버(함수 등)만 import, 위의 module을 이용한다.
            module.moduleFunc            

    6. for of의 도입
        ES6에 추가된 새로운 컬렉션 전용 반복 구문입니다


    최상단에 적어놓은것들이, 이번 ES5 ES6를 비교했을때, 변경되거나 추가된 내용이며
    도입되거나 변경된게 많지만, 제가 이해되는선에서만 작성한 내용입니다. 

    공부하고 알아야할게 너무많네요.