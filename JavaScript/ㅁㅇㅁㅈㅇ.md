## 10장 객체 리터럴
### 10.1 객체란?
자바스크립트는 객체기반의 프로그래밍 언어이며, 자바스크립트를 구성하는 거의 "모든 것"이 객체다. 원시 타입은 단 하나의 값만 나타내지만 객체 타입은 다양한 타입의 값을 하나의 단위로 구성한 복합적인 자료구조다.
**원시 타입의 값, 즉 원시 값은 변경 불가능한 값이지만 객체 타입의 값, 즉 객체는 변경 가능한 값**이다.
객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키와 값으로 구성된다.
자바스크립트에서 사용할 수 있는 모든 값은 프로퍼티 값이 될 수 있고, 함수는 일급 객체이므로 값으로 취급할 수 있다. 프로퍼티 값이 함수일 경우, 일반 함수와 구분하기 위해 메서드라 부른다.
![](https://velog.velcdn.com/images/guddyd6761/post/3c5952ad-f6d6-4942-8089-3a9e0215968f/image.png)

- 프로퍼티: 객체의 상태를 나타내는 값
- 메서드: 프로퍼티를 참조하고 조작할 수 있는 동작

### 10.2 객체 리터럴에 의한 객체 생성
C++나 자바 같은 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다.
> 인스턴스
인스턴스란 클래스에 의해 생성되어 메모리에 저장된 실체를 말한다. 객체지향 프로그래밍에서 객체는 클래스와 인스턴스를 포함한 개념이다.

자바스크립트는 프로토타입 기반 객체지향 언어로서 다양한 객체 생성 방법을 지원한다.
객체 리터럴 / object 생성자 함수 / 생성자 함수 / object.create 메서드 / 클래스(ES6)
객체 생성 방법 중에서 가장 일반적으로 간단한 방법은 객체 리터럴을 사용하는 방법이다. 객체 리터럴은 중괄호({...})내에 0개 이상의 프로퍼티를 정의한다.
```javascript
var person = {
	name: 'Lee',
  	sayHello: function(){
    	console.log(`Hello! My name is ${this.name}.`);
    }
};

console.log(typeof person); // object
console.log(person); // {name: "Lee" , sayHello: f}
```
객체 리터럴은 자바스크립트의 유연함과 강력함을 대표하는 객체 생성 방식으로, 객체를 생성하기 위해 클래스를 먼저 정의하고 new 연산자와 함께 생성자를 호출할 필요가 없다. 

### 10.3 프로퍼티
**객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.**
프로퍼티를 나열할 때는 쉼표(,)로 구분한다. 
- 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
- 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값

식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야 한다.
```javascript
var person = {
	firstName: 'Ung-mo', //식별자 네이밍 규칙을 준수하는 프로퍼티 키
  	'last-name' : 'Lee' //식별자 네이밍 규칙을 준수하는 않는 프로퍼티 키
}
console.log(persone); //{firstName: 'Ung-mo' , last-name: 'Lee'}
```

### 10.4 메서드
프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라 부른다. 
```javascript
var circle = {
	radius: 5 // <- 프로퍼티
  
  //원의 지름
  getDiameter: function(){// <- 메서드
  	return 2 * this.radius; // this는 circle을 가리킨다.
  }
}

console.log(circle.getDiameter()); // 10
```

### 10.5 프로퍼티 접근
프로퍼티에 접근하는 방법은 다음과 같이 두 가지다.
- 마침표 프로퍼티 접근 연산자(.)를 사용하는 **마침표 표기법**
- 대괄호 프로퍼티 접근 연산자([...])를 사용하는 **대괄호 표기법**

### 10.6 프로퍼티 값 갱신
이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.
```javascript
var persone = {
	name: 'Lee'
};

// person 객체에 name 프로퍼티가 존재하므로 name 프로퍼티의 값이 갱신된다.
person.name = 'Kim';

console.log(person); // {name: "Kim"}
```

### 10.7 프로퍼티 동적 생성
존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.
```javascript
var person = {
	name: 'Lee'
};

//person 객체에는 age 프로퍼티가 존재하지 않는다.
//따라서 persone 객체에 age 프로퍼티가 동적으로 생성되고 값이 할당된다.
persone.age = 20;

console.log(persone); //{name: "Lee", age: 20}
```

### 10.8 프로퍼티 삭제
delete 연산자는 객체의 프로퍼티를 삭제한다. 이때 delete 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.
```javascript
var person = {
	name: 'Lee'
};

//프로퍼티 동적 생성
persone.age = 20;

//person 객체에 age 프로퍼티가 존재한다.
//따라서 delete 연산자로 age 프로퍼티를 삭제할 수 있다.
delete person.age;

//person 객체에 address 프로퍼티가 존재하지 않는다.
//따라서 delete 연산자로 address 프로퍼티를 삭제할 수 없다.
delete person.address;

console.log(persone); //{name: "Lee"}
```

### 10.9 ES6에서 추가된 객체 리터럴의 확장 기능
#### 프로퍼티 축약 표현
객체 리터럴의 프로퍼티는 프로퍼티 키와 프로퍼티 값으로 구성된다.ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략할 수 있다.
```javascript
//ES6
let x = 1 , y = 2;

//프로퍼티 축약 표현
const obj = {x , y};

console.log(obj); // {x:1 , y:2}
```

#### 계산된 프로퍼티 이름
문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다.
```javascript
//ES6
const prefix = 'prop';
let i = 0;

//객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성
const obj = {
	[`${prefix}-${++i}`]: i,
  	[`${prefix}-${++i}`]: i,
  	[`${prefix}-${++i}`]: i,
};

console.log(obj)l //{prop-1: 1,prop-2: 2, prop-3: 3} 
```

#### 메서드 축약 표현
ES6에서는 메서드를 정의할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.
```javascript
//ES6
const obj = {
	name: 'Lee',
  	//메서드 축약 표현
  	sayHi(){
    console.log('Hi!' + this.name);
    }
};

obj.sayHi(); //Hi! Lee
```


