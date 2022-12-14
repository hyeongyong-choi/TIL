### 05장 표현식과 문

#### 5.1 값
`값은 식(표현식)이 평가되어 생성된 결과를 말한다.` 평가란 식을 해석해서 값을 생성하거나 참조하는 것을 의미한다. 변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 메모리 공간을 식별하기 위해 붙인 이름이니 변수에 할당되는 것은 값이다.
```javascript
//변수에는 10+20이 평가되어 생성된 숫자 값 30일 할당된다.
var sum = 10+20;
```
#### 5.2 리터럴
`리터럴은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법을 말한다.`
```javascript
//숫자 리터럴 3
3
```
위 예제의 3은 단순한 아라비아 숫자가 아니라 숫자 리터럴이다. 즉 리터럴은 사람이 이해할 수 있는 문자(아라비아 숫자, 알파벳, 한글 등) 또는 미리 약속된 기호('',"",.,[],{},// 등)로 표기한 코드이다. 자바스크립트 엔진은 코드가 실행되는 런타임에 리터럴을 평가해 값을 생성한다.

#### 5.3 표현식
`표현식은 값으로 평가될 수 있는 문이다. 즉 표현식이 평가되면 새로운 값을 생성하거나 기존값을 참조한다.`
표현식은 리터럴, 식별자(변수,함수 등의 이름), 연산자, 함수 호출 등의 조합으로 이뤄질 수 있다.
즉 값으로 평가될 수 있는 문은 모두 표현식이다.

#### 5.4 문
`문은 프로그램을 구성하는 기본 단위이자 최소 실행 단위이다.` 문의 집합으로 이뤄진 것이 바로 프로그램이며, 문을 작성하고 순서에 맞게 나열하는 것이 프로그래밍이다.
문은 여러 토큰으로 구성되는데, `토큰이란 문법적인 의미를 가지며, 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소를 의미한다.`
![](https://velog.velcdn.com/images/guddyd6761/post/e7faaea4-d40e-4df3-ba3e-ca078e86d2d9/image.png)


#### 5.5 세미콜론과 세미콜론 자동 삽입 기능
자바스크립트 엔진은 세미콜론으로 문이 종료한 위치를 파악하고 순차적으로 하나씩 문을 실행하는데, 세미콜론은 문의 종료를 나타낸다. 하지만 0개 이상의 문을 중괄호로 묶은 if문, for문, 함수 등의 코드 블록({ ... })뒤에는 붙이지 않는다.
자바스크립트 엔진이 문의 끝이라고 예측되는 지점에 세미콜론을 자동으로 붙여주는 세미콜론 자동 삽입 기능이 있기 때문에 문의 끝에 붙이는 세미콜론은 옵션으로 생략 가능하다.


#### 5.6 표현식인 문과 표현식이 아닌 문
```javascript
///변수 선언문은 값으로 평가될 수 없으므로 표현식이 아니다.
var x;
//1, 2, 1+2, x = 1+2 는 모두 표현식이다.
//x = 1+2는 표현식이면서 완전한 문이기도 하다.
x = 1+2
```
문에는 표현식인 문과 표현식이 아닌 문이 있다. 표현식인 문은 값으로 평가될 수 있는 문이며, 표현이 아닌 문은 값으로 평가될 수 없는 문을 말한다.
`표현식인 문과 표현식이 아닌 문을 구별하는 가장 간단하고 명료한 방법은 변수에 할당해 보는 것이다.`

🔥완료 값
크롬 개발자 도구에서 표현식이 아닌 문을 실행하면 언제나 undefined를 출력한다. 이를 완료 값이라고 한다. 완료 값은 표현식의 평가 결과가 아니기에 다른 값과 같이 변수에 할당할 수 없고 참조할 수도 없다.
표현식인 문을 실행하면 언제나 평가된 값을 반환한다.

![](https://velog.velcdn.com/images/guddyd6761/post/e7f1f507-18c5-440d-88c0-e70283b4bcfd/image.png)



