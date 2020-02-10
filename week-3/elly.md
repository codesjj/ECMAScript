# ECMAScript
1. Class 부족했던 부분
> ( Instance properties, extends, Species, Mix-ins 등 부족하다고 생각 드는 메서드 )

2. Class를 이용하여 Tab을 만들어보기
> 1. script : Tab의 기능을 가진 Class는 하나만 생성
> 2. 결과물 : 2개 이상 각각 따로 돌아가는 Tab<br>
> 참고자료 : [http://witplus.com/ex/test.html](http://witplus.com/ex/test.html){: target="_blank"}
> why target _blank 가 안되냐구요 !!



### 1. class - Instance properties
반드시 클래스 메서드 내에 정의되어야 함.

### 2. class - extends
클래스 선언이나 클래스 표현식에서 다른 클래스의 자식 클래스를 생성하기 위해 사용됨.
```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}
```

### 3. class - Mix-ins
