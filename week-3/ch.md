## Class 부족했던 부분
## ( Instance properties, extends, Species, Mix-ins 등 부족하다고 생각 드는 메서드 )

#### 1. Strict Mode

**클래스 몸통(body)는 strict mode로 실행됩니다.**
    _여기서 말하는 strict mode란?_
    - strict 모드는 문법과 런타임 동작을 모두 검사하여, 실수를 에러로 변환하고, 변수 사용을 단순화(Simplifying) 시켜줍니다.
    - 흔히 발생하는 코딩 실수를 잡아내서 예외를 발생시킵니다.
    - 상대적으로 안전하지 않은 액션이 발생하는 것을 방지하거나 그럴 때 예외를 발생시킵니다. 예를 들자면 전역객체들에 접근하려 한다거나 하는 것들입니다.
    - 혼란스럽거나 제대로 고려되지 않은 기능들을 비활성화시킵니다.

#### 2. extends (상속)

<pre>
    class Animal {
        constructor(name){
            this.name = name;
        }
    }

    class Duck extends Animal { //이런문법으로 사용해야 합니다. 
        
        // animal에 있는 name을 그대로 상속합니다.
        // 하지만 여기서 animal에 있는 메소드를 그대로 가져오고싶다 하면, super 키워드를 통해 사용해야합니다.
        
        flyTo(destination){
            console.log(`${this.name} is flying to the ${destination}`);
        }
        eat(food){
            console.log(`${this.name} is eating ${food}`);
        }
        swimAt(place){
            console.log(`${this.name} is swiming at the ${place}`)
        }
    };
    const duck = new Duck('Donald duck');
    duck.flyTo('home');   // Donald duck is flying to the home
    duck.eat('fish');     // Donald duck is eating fish
    duck.swimAt('river'); // Donald duck is swiming at the river
</pre>

**super 키워드는 객체의 부모가 가지고 있는 함수들을 호출하기 위해 사용됩니다.**

#### 3. static 키워드

- static 키워드는 클래스를 위한 정적(static) 메소드를 정의합니다. 
- 정적 메소드는 prototype에 연결되지 않고 클래스에 직접 연결되기 때문에 클래스의 인스턴스화(instantiating) 없이 호출되며, 클래스의 인스턴스에서는 호출할 수 없습니다. 
- 동일한 클래스 내의 다른 정적 메서드 내에서 정적 메서드를 호출하는 경우 키워드 this를 사용할 수 있다.

<pre>
    class Lion {
        static speak() {
            console.log('Noise~');
        }
    }

    Lion.speak();
    // [결과] Noise~
    // 곰곰히 생각을 해봤는데, 이건 아무래도 다른 클래스처럼 new없이 바로 접근을 할 수 있다 라고 설명을 하는 거 같습니다.
    // 하지만 클래스 내부에서는 사용 할 수 없다?
</pre>

#### 4. mixin

자바스크립트에서는 오직 한개의 object만 상속할 수 있다. 
한개의 object에는 한개의 prototype이 존재하기 때문이다. 
또한 class도 마찬가지로 오직 한개의 class만 상속할 수 있다. 하지만 이는 한계가 있다. 
대신 Mixin 패턴을 사용하여 이를 해결할 수 있다. 
Mixin은 다른 클래스의 부모2 클래스가 아니어도 다른 클래스에서 사용할 수있는 메서드가 포함 된 클래스이다.
다시 말해, Mixin은 특정 동작을 구현하는 메서드를 제공하지만 우리는이 메서드를 단독으로 사용하지 않고 다른 클래스에 동작을 추가하는 데 사용한다.
자바 스크립트에서 Mixin을 만드는 가장 간단한 방법은 유용한 메소드로 객체를 만드는 것이다. 
그 객체를 어떤 클래스의  prototype으로 쉽게 병합할 수 있다. 

<pre>
        // mixin은 좀 헷갈리니, 예제를 보면서 이해해 주시길 바랍니다. ( prototype 를 잘 확인해주세요. )
        
        // mixin
        let sayHiMixin = {
            sayHi() {
                console.log(`Hello ${this.name}`);
            },
            sayBye() {
                console.log(`Bye ${this.name}`);
            }
        };
        // usage: 
        class User {
            constructor(name) {
                this.name = name;
            }
        }
        // copy the methods
        Object.assign(User.prototype, sayHiMixin);
        // now User can say hi 
        new User("Dude").sayHi();
        // Hello Dude!
</pre>

여기서 mixin인 sayHiMixin은 User에 대한 "sayHi"와 "sayBye"와 같은 메소드를 추가하는 데 사용된다. 
상속은 없지만 간단한 방법으로 메소드를복사 할 수 있다. 
따라서 User는 다른 클래스를 상속 할 수 있으며  아래와 같은의미로 추가 메소드를 "혼합(mix)"하기 위해 mixin을 포함 할 수 있다.


_Mixins는 내부에서 상속을 사용할 수 있다._

<pre>
        let sayMixin = {
            say(phrase) {
                console.log(phrase);
            }
        };
        let sayHiMixin = {
            __proto__: sayMixin, // (or we could use Object.create to set the prototype here) 
            sayHi() {
                // call parent method super.say(`Hello ${this.name}`);
            },
            sayBye() {
                super.say(`Bye ${this.name}`);
            }
        };
        class User {
            constructor(name) {
                this.name = name;
            }
        }
        // copy the methods
        Object.assign(User.prototype, sayHiMixin);
        // now User can say hi 
        new User("Dude").sayHi(); // Hello Dude!
</pre>

sayHiMixin은 sayMixin으로부터 상속 받는다. 
sayHiMixmin에서 상위 메소드인 
super.say를 호출하면 클래스가 아닌 해당 mixin의 프로토타입의 메소드가 실행이 된다. 

<pre>

</pre>


