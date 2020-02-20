##### 모듈
- 모듈이란 애플리케이션을 구성하는 개별적 요소로서 재사용 가능한 코드 조각을 말한다. 모듈은 세부 사항을 캡슐화하고 공개가 필요한 API만을 외부에 노출한다.
- ** 클라이언트 사이드 자바스크립트는 script 태그를 사용하여 외부의 스크립트 파일을 가져올 수는 있지만, 파일마다 독립적인 파일 스코프를 갖지 않고 하나의 전역 객체(Global Object)를 공유한다 **

### 1. 모듈 사용문법

<pre>
    <script type="module" src="test_01.js"></script>
    <script type="module" src="test_02.js"></script>
</pre>

- EX.01 스코프예제 
<pre>
    <script type="" src="test_01.js"></script>
    <script type="" src="test_02.js"></script>   
    
    // test_01.js
    var wit = 'plus';

    // 변수 wit는 전역 변수이다.
    console.log(window.wit); // plus
    
    //--------------------------------------------
    
    // test_02.js
    // test_01.js에서 선언한 전역 변수 wit와 중복된 선언이다.
    var wit = '...연봉많이주세요.';

    // 변수 wit는 전역 변수이다.
    // test_01.js에서 선언한 전역 변수 wit의 값이 재할당되었다.
    console.log(window.wit); // ...연봉많이주세요.    
</pre>

- EX.02 모듈을 사용한 스코프예제 
<pre>
    <script type="module" src="test_01.js"></script>
    <script type="module" src="test_02.js"></script>   
    
    // test_01.js
    var wit = 'plus';

    console.log(wit); // plus
    // 변수 wit는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.
    console.log(window.wit); // undefined
    
    //--------------------------------------------
    
    // test_02.js
    // 변수 wit는 foo.mjs에서 선언한 변수 wit와 스코프가 다른 변수이다.
    var wit = '...연봉많이주세요.';

    console.log(wit); // ...연봉많이주세요.
    // 변수 x는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.
    console.log(window.wit); // undefined   
</pre>

- 모듈 내에서 선언한 변수는 모듈 외부에서 참조할 수 없다. 스코프가 다르기 때문이다.

### 2. 모듈 - export

- 모듈은 독자적인 모듈 스코프를 갖기 때문에 모듈 안에 선언한 모든 식별자는 기본적으로 해당 모듈 내부에서만 참조할 수 있다. 
- 만약 모듈 안에 선언한 식별자를 외부에 공개하여 다른 모듈들이 참조할 수 있게 하고 싶다면 export 키워드를 사용한다. 
- 선언된 변수, 함수, 클래스 모두 export할 수 있다.
- ( CLASS의 가져오기, 내보내기 동일하게 생각하면 이해가 편합니다. )

<pre>
    // test_01.js
    
    // 변수의 공개 ( 변수앞의 export 키워드 )
    export const pi = Math.PI; 

    // 함수의 공개 ( 함수앞의 export 키워드 )
    export function square(x) {
      return x * x;
    }

    // 클래스의 공개 ( 클래스 앞의 export 키워드 )
    export class Person {
      constructor(name) {
        this.name = name;
      }
    }
    
    // 만약 export의 개수가 많아진다면, 하나로 묶어서 사용이 가능합니다.
    // 예 ) export { pi, square, Person };
</pre>

### 3. 모듈 - import

- 모듈에서 공개(export)한 대상을 로드하려면 import 키워드를 사용한다.
- 모듈이 export한 식별자로 import하며 **ES6 모듈의 파일 확장자를 생략할 수 없다.**

<pre>
    // app.mjs
    
    // 같은 폴더 내의 test_01.js 모듈을 로드.
    // test_01.js 모듈이 export한 식별자로 import한다.
    // ES6 모듈의 파일 확장자를 생략할 수 없다.
    
    import { pi, square, Person } from './test_01.js';

    console.log(pi);         // 3.141592653589793
    console.log(square(10)); // 100
    console.log(new Person('Lee')); // Person { name: 'Lee' }
</pre>

- 마찬가지로, import도 한줄로 하나로 묶어서 사용이 가능합니다.

<pre>
    // app.mjs
    
    import * as wit from './test_01.js';
    //모듈이 export한 식별자를 각각 지정하지 않고 하나의 이름으로 한꺼번에 import할 수도 있다. 
    //이때 import되는 식별자는 as 뒤에 지정한 이름의 객체에 프로퍼티로 할당된다.

    console.log(wit.pi);         // 3.141592653589793
    console.log(wit.square(10)); // 100
    console.log(new wit.Person('Lee')); // Person { name: 'Lee' }
</pre>

- 모듈에서는 총 두가지의 키워드가 있으며, export(내보내기) / import(가져오기) 이 두개만 기억하면 될 거 같습니다!
- 사용목적 코드의 비밀성(?), 모듈 js 페이지 안에서 하나하나씩 꺼내 사용함이 있기때문에 아무래도 접근성에 도움이 될 거 같습니다.
- 이 두가지말고, Default Export 라는 키워드가 하나 더있습니다. ( 모듈 당 단 한번 만 할 수 있는 Export 입니다. ) 은재시가 알아올 거 같습니다! 

