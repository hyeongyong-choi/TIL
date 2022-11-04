## 08장 제어문
`제어문은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다.` 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행되나, 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.

### 8.1 블록문
블록문은 0개 이상의 문을 중괄호로 묶은 것으로, 코드 블록 또는 블록이라고 부릅니다. 자바스크립트는 블록문을 하나의 실행 단위로 취급하고, 단독으로 사용할 수도 있으나 일반적으로 제어문이나 함수를 정의할 때 사용하는 것이 일반적이다.
```javascript
//블록문
{
	var foo = 10;
}

//제어문
{
	var x = 1;
  	if(x < 10) {
    x++
    }
}

//함수 선언문
function sum(a,b){
	return a+b
}
```

### 8.2 조건문
조건문은 주어진 조건식의 평가 결과에 따라 코드 블록의 실행을 결정한다. 조건식은 불리언 값으로 평가될 수 있는 표현식이다. if...else 문과 switch 문 두 가지 조건문을 제공한다.

#### 8.2.1 if...else문
조건식의 평가 결과가 true일 경우 if문의 코드 블록이 실행되고, false일 경우 else문의 코드 블록이 실행된다.

```javascript
if(조건식1){
	// 조건식1이 참이면 이 코드 블록이 실행된다.  
}else if(조건식2){
	// 조건식2가 참이면 이 코드 블록이 실행된다.
}else{
	//조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
```
```javascript
// x가 짝수이면 result 변수에 문자열 '짝수'를 할당하고, 홀수이면 문자열 '홀수'를 할당한다.
var x = 2;
var result;

if(x % 2){ // 2 % 2는 0이다. 이때 0은 false로 암묵적 강제 변환된다.
	result = '홀수';
}else{
	result = '짝수';
}

//위 예제는 아래와 같이 삼항 조건 연산자로 바꿔 쓸 수 있다.
var result = x % 2 ? '홀수' : '짝수';

console.log(result); // 짝수

```

삼항 조건 연산자는 값으로 평가되는 표현식을 만들기에 변수에 할당할 수 있다. 하지만 if...else문은 표현식이 아닌 문이기에 변수에 할당할 수 없다.


#### 8.2.2 switch문
switch문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case문으로 실행 흐름을 옮긴다.
case문은 상황을 의미하는 표현식을 지정하고 콜론으로 마친다. swidth 문의 표현식과 일치하는 case문이 없다면 실행 순서는 default문으로 이동한다.

```javascript
switch(표현식){
  case 표현식1:
    switch문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    switch문의 표현식과 표현식2가 일치하면 실핼될 문;
    break;
  default:
    switch문의 표현식과 일치하는 case문이 없을 때 실행될 문;
}
```

if...else문은 논리적 참, 거짓으로 실행할 코드 블록을 결정하고, switch문은 다양한 상황에 따라 실행할 코드 블록을 결정할 때 사용한다.

```javascript
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = 'January';
  case 2:
    monthName = 'February';
  case 3:
    monthName = 'March';
  case 4:
    monthName = 'April';
  case 5:
    monthName = 'May';
  case 6:
    monthName = 'June';
  case 7:
    monthName = 'July';
  case 8:
    monthName = 'August';
  case 9:
    monthName = 'September';
  case 10:
    monthName = 'October';
  case 11:
    monthName = 'November';
  case 12:
    monthName = 'December';
  default:
    monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```

monthName 변수에 'November'가 할당된 후 switch 문을 탈출하지 않고 연이어 'December'가 재할당되고 마지막으로 'Invalid month'가 재할당되어 실행하였을 때, 'Invalid month'가 출력된다.
switch문이 끝날 때까지 이후의 모든 case문과 defalt문을 실행했기 때문인데 이를 `폴스루`라고 한다.
이를 해결하기 위해서는 코드 블록에서 탈출하는 역할을 하는 break문을 사용해야 한다.

### 8.3 반복문
반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다. 그 후 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행한다.
자바스크립트는 for문 , while문, do...while문을 제공한다.

#### 8.3.1 for문
for문은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행한다.
```javascript
for(변수 선언문 또는 할당문; 조건식; 증감식){
	조건식이 참인 경우 반복 실행될 문;
}
```
![](https://velog.velcdn.com/images/guddyd6761/post/3df3ef5c-391b-408b-a6a5-5fe7896b46f4/image.png)

for문 내에 for문을 중첩해 사용하는 중첩 for문도 가능하다.

```javascript
for (var i = 1; i <= 6; i++) {
  for (var j = 1; j <= 6; j++) {
    if (i + j === 6) console.log(`[${i}, ${j}]`);
  }
}

//결과
[1, 5]
[2, 4]
[3, 3]
[4, 2]
[5, 1]
```
#### 8.3.2 while문
while문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다. 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환하여 논리적 참, 거짓을 구별한다.

```javascript
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count);
  count++;
} // 0 1 2
```
#### 8.3.3 do...while문
do…while 문은 코드 블록을 실행하고 조건식을 평가한다. 따라서 코드 블록은 무조건 한번 이상 실행된다.

```javascript
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count);
  count++;
} while (count < 3); // 0 1 2
```

### 8.4 break문
레이블 문(식별자가 붙은 문), 반복문(for, for…in, for…of, while, do…while) 또는 switch 문의 코드 블록을 탈출한다.

```javascript
var string = 'Hello World.';
var index;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l'이면
  if (string[i] === 'l') {
    index = i;
    break; // 반복문을 탈출한다.
  }
}

console.log(index); // 2

// 참고로 String.prototype.indexOf 메소드를 사용해도 같은 동작을 한다.
console.log(string.indexOf('l')); // 2
```
### 8.5 continue문
continue 문은 반복문(for, for…in, for…of, while, do…while)의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 이동한다. break 문처럼 반복문을 탈출하지는 않는다.

```javascript
var string = 'Hello World.';
var count = 0;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== 'l') continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3

// 참고로 String.prototype.match 메소드를 사용해도 같은 동작을 한다.
console.log(string.match(/l/g).length); // 3
```
