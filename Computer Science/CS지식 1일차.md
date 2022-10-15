### 1장 디자인 패턴과 프로그래밍 패러다임

#### 1.1 디자인 패턴
`디자인 패턴이란 프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 '규약'형태로 만들어 놓은 것을 의미합니다.`

*1.1.1 싱글톤 패턴*
`싱글톤 패턴은 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴입니다. 보통 데이터베이스 연결 모듈에 많이 사용합니다.
객체를 생성할 때마다 메모리 영역을 할당받아야 하지만, 하나의 인스턴스만 생성했기 때문에 메모리 낭비를 방지 할 수 있고, 다른 클래스의 인스턴스들이 데이터를 공유할 수 있는 장점이 있습니다.
자바스크립트에서는 리터럴{} 또는 new Object로 객체를 생성하게 되면 다른 어떤 객체와도 같지 않기 때문에 자체만으로 싱글톤 패턴을 구현할 수 있습니다.`
`생성자가 여러번 호출되도, 실제로 생성되는 객체는 하나이며 최초로 생성된 이후에 호출된 생성자는 이미 생성한 객체를 반환시키도록 만드는 것이다
(java에서는 생성자를 private으로 선언해 다른 곳에서 생성하지 못하도록 만들고, getInstance() 메소드를 통해 받아서 사용하도록 구현한다)`
```javascript
javascript

class Singleton {
    constructor() {
        if (!Singleton.instance) {
            Singleton.instance = this
        }
        return Singleton.instance
    }
    getInstance() {
        return this 
    }
}
const a = new Singleton()
const b = new Singleton() 
console.log(a === b) // true
```

```java
java

class Singleton {
    private static class singleInstanceHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance() {
        return singleInstanceHolder.INSTANCE;
    }
}

public class HelloWorld{ 
     public static void main(String []args){ 
        Singleton a = Singleton.getInstance(); 
        Singleton b = Singleton.getInstance(); 
        System.out.println(a.hashCode());
        System.out.println(b.hashCode());  
        if (a == b){
         System.out.println(true); 
        } 
     }
}
/*
705927765
705927765
true
1. 클래스안에 클래스(Holder), static이며 중첩된 클래스인 singleInstanceHolder를 
기반으로 객체를 선언했기 때문에 한 번만 로드되므로 싱글톤 클래스의 인스턴스는 애플리케이션 당 하나만 존재하며 
클래스가 두 번 로드되지 않기 때문에 두 스레드가 동일한 JVM에서 2개의 인스턴스를 생성할 수 없습니다. 
그렇기 때문에 동기화, 즉 synchronized를 신경쓰지 않아도 됩니다. 
2. final 키워드를 통해서 read only 즉, 다시 값이 할당되지 않도록 했습니다.
3. 중첩클래스 Holder로 만들었기 때문에 싱글톤 클래스가 로드될 때 클래스가 메모리에 로드되지 않고 
어떠한 모듈에서 getInstance()메서드가 호출할 때 싱글톤 객체를 최초로 생성 및 리턴하게 됩니다. 
*/
```

`싱글톤 패턴은 Node.js에서 MongoDB 데이터베이스를 연결할 때 mongoose모듈을 사용.`
`싱글톤 패턴은 Node.js에서 MySQL 데이터베이스를 연결할 때도 사용.`

`싱글톤 패턴은 각 테스트마다 '독립적인' 인스턴스를 만들기가 어려워 TDD(Test Driven Development)를 할 때 걸림돌이 되는 단점이 있습니다. 또한 사용하기가 쉽고 실용적이지만 모듈간의 결합을 강하게 만들 수 있다는 단점이 있습니다.이 때 의존성 주입을 통해 모듈간의 결합을 조금 더 느슨하게 만들어 해결할 수 있습니다.`

**의존성 주입**
`의존성이란 종속성이라고도 하며 A가 B에 의존성이 있다는 것은 B의 변경 사항에 대해 A 또한 변해야 한다는 것을 의미합니다. 메인모듈이 '직접'다른 하위 모듈에 대한 의존성을 주기보다는 중간에 의존성 주입자가 이 부분을 가로채 메인 모듈이 '간접'적으로 의존성을 주입하는 방식입니다.`
![](https://velog.velcdn.com/images/guddyd6761/post/da1749be-13c9-4a42-9a23-20a2825b64e7/image.png)

`장점: 모듈들을 쉽게 교체할 수 있는 구조가 되어 테스팅하기 쉽고 마이그레이션하기도 수월하고, 애플리케이션 의존성 방향이 일관되어지고 모듈간의 관계들이 조금 더 명확해집니다.`
`단점: 클래스 수가 늘어나 복잡성이 증가될 수 있으며 약간의 린타임 패널티가 생깁니다.`



*1.1.2 팩토리 패턴*
`팩토리 패턴은 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴입니다. 상위 클래스와 하위 클래스가 분리되기 때문에 더 많은 유연성을 갖게 되고, 객체 생성 로직이 따로 떼어져 있기 때문에 유지 보수성도 증가됩니다.`
```javascript
javascript

class Latte {
    constructor() {
        this.name = "latte"
    }
}
class Espresso {
    constructor() {
        this.name = "Espresso"
    }
} 

class LatteFactory {
    static createCoffee() {
        return new Latte()
    }
}
class EspressoFactory {
    static createCoffee() {
        return new Espresso()
    }
}
const factoryList = { LatteFactory, EspressoFactory } 
 
class CoffeeFactory {
    static createCoffee(type) {
        const factory = factoryList[type]
        return factory.createCoffee()
    }
}   
const main = () => {
    // 라떼 커피를 주문한다.  
    const coffee = CoffeeFactory.createCoffee("LatteFactory")  
    // 커피 이름을 부른다.  
    console.log(coffee.name) // latte
}
main()
/*
CoffeeFactory라는 상위 클래스가 중요한 뼈대를 결정하고 하위 클래스인 LatteFactory
가 구체적인 내용을 결정하고 있습니다. 
참고로 이는 의존성 주입이라고도 볼 수 있습니다. 
CoffeeFactory에서 LatteFactory의 인스턴스를 생성하는 것이 아닌 
LatteFactory에서 생성한 인스턴스를 CoffeeFactory에 주입하고 있기 때문이죠.
또한, CoffeeFactory를 보면 static으로 createCoffee() 정적 메서드를 정의한 것을 알
수 있는데, 정적 메서드를 쓰면 클래스의 인스턴스 없이 호출이 가능하여 메모리를 절약
할 수 있고 개별 인스턴스에 묶이지 않으며 클래스 내의 함수를 정의할 수 있는 장점이 있
습니다. 
*/
```

```java
java

abstract class Coffee { 
    public abstract int getPrice(); 
    
    @Override
    public String toString(){
        return "Hi this coffee is "+ this.getPrice();
    }
}

class CoffeeFactory { 
    public static Coffee getCoffee(String type, int price){
        if("Latte".equalsIgnoreCase(type)) return new Latte(price);
        else if("Americano".equalsIgnoreCase(type)) return new Americano(price);
        else{
            return new DefaultCoffee();
        } 
    }
}
class DefaultCoffee extends Coffee {
    private int price;

    public DefaultCoffee() {
        this.price = -1;
    }

    @Override
    public int getPrice() {
        return this.price;
    }
}
class Latte extends Coffee { 
    private int price; 
    
    public Latte(int price){
        this.price=price; 
    }
    @Override
    public int getPrice() {
        return this.price;
    } 
}
class Americano extends Coffee { 
    private int price; 
    
    public Americano(int price){
        this.price=price; 
    }
    @Override
    public int getPrice() {
        return this.price;
    } 
} 
public class HelloWorld{ 
     public static void main(String []args){ 
        Coffee latte = CoffeeFactory.getCoffee("Latte", 4000);
        Coffee ame = CoffeeFactory.getCoffee("Americano",3000); 
        System.out.println("Factory latte ::"+latte);
        System.out.println("Factory ame ::"+ame); 
     }
} 
/*
Factory latte ::Hi this coffee is 4000
Factory ame ::Hi this coffee is 3000
*/
```
