# CH12 함수

## 12.1 함수란?

&nbsp;일련의 과정을 문으로 구현하고 코드 블록으로 감싸서 하나의 실행단위로 정의한 것

## 12.2 함수를 사용하는 이유

- 코드의 재사용
- 유지보수의 편의성
- 코드의 신뢰성 증대
- 코드의 가독성 향상

## 12.3 함수 리터럴

&nbsp;함수는 객체다. 단, 일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.

```javascript
// 변수에 함수 리터럴을 할당
var f = function add(x, y) {
  return x + y;
};
```

#### 함수 리터럴의 구성요소

- 함수 이름
  - 함수 이름은 식별자다. 따라서 식별자 네이밍 규칙을 준수해야 한다.
  - 함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자다.
  - 함수 이름은 생략할 수 있다. 이름이 있는 함수를 기명 함수, 이름이 없는 함수를 무명/익명 함수라 한다.
- 매개변수 목록
  - 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분하다.
  - 각 매개변수에는 함수를 호출할 때 지정한 인수가 순서대로 할당된다. 즉, 매개변수 목록은 순서에 의미가 있다.
  - 매개변수는 함수 몸체 내에서 변수와 동일하게 취급된다. 따라서 매개변수도 변수와 마찬가지로 식별자 네이밍 규칙을 준수해야 한다.
- 함수 몸체
  - 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행 단위로 정의한 코드 블록이다.
  - 함수 몸체는 함수 호출에 의해 실행된다.

## 12.4 함수 정의

&nbsp;함수를 호출하기 이전에 인수를 전달받을 매개변수와 실행할 문들, 그리고 반환할 값을 지정하는 것

### 12.4.1 함수 선언문

```javascript
function (x, y) {
    return x + y;
}
// SyntaxError: Function statements require a function name
```

&nbsp;함수 이름을 생략할 수 없음

```javascript
// 함수 선언문은 표현식이 아닌 문이므로 변수에 할당할 수 없다.
// 하지만 함수 선언문이 변수에 할당되는 것처럼 보인다.
var add = function add(x, y) {
  return x + y;
};

// 함수 호출
console.log(add(2, 5)); // 7
```

-> 이렇게 동작하는 이유는 자바스크립트 엔진이 코드의 문맥에 따라 동일한 함수 리터럴을 표현식이 아닌 문인 함수 선언문으로 해석하는 경우와 표현식인 문인 함수 리터럴 표현식으로 해석하는 경우가 있기 때문(기명 함수 리터럴은 함수 선언문 또는 함수 리터럴 표현식으로 해석될 가능성이 있음)

```javascript
// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() {
  console.log("foo");
}

foo(); // foo

// 함수 리터럴을 피연산자로 사용하면 함수 선언문이 아니라 함수 리터럴 표현식으로 해석된다.
// 함수 리터럴에서는 함수 이름을 생략할 수 있다.
// 함수를 가리키는 식별자가 없다.
(function bar() {
  console.log("bar");
});
bar(); // ReferenceError: bar is not defined
```

&nbsp;자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체를 할당한다. 함수는 함수 이름으로 호출하는 것이 아니라 **함수 객체를 가리키는 식별자로 호출**한다.

```javascript
// var add: 식별자, function add: 함수 이름
var add = function add(x, y) {
  return x + y;
};

console.log(add(2, 5)); // 식별자 add
```

## 12.4.2 함수 표현식

&nbsp;자바스크립트의 함수는 **일급 객체**다. 값처럼 변수에 할당할 수도 있고 프로퍼티 값이 될 수도 있으며 배열의 요소가 될 수도 있는, 값의 성질을 갖는 객체를 일급 객체라 한다.

```javascript
// 기명 함수 표현식
var add = function foo(x, y) {
  return x + y;
};

// 함수 객체를 가리키는 식별자로 호출
console.log(add(2, 5));

// 함수 이름으로 호출하면 ReferenceError가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined
```

&nbsp;함수 선언문은 표현식이 아닌 문이고, 함수 표현식은 표현식인 문이다.

### 12.4.3 함수 생성 시점과 함수 호이스팅

```javascript
// 함수 참조
console.dir(add); // f add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

Q. 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있다. 그러나 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출할 수 없다. 왜?
A. 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르기 때문이다. 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다.

### 12.4.4 Function 생성자 함수

&nbsp;FUnction 생성자 함수로 생성한 함수는 클로저를 생성하지 않는 등, 함수 선언문이나 함수 표현식으로 생성한 함수와 다르게 동작한다. **권장하지 않는 방식**

### 12.4.5 화살표 함수

```javascript
// 화살표 함수
const add = (x, y) => x + y;
console.log(add(2, 5)); // 7
```

&nbsp;화살표 함수는 생성자 함수로 사용할 수 없으며, 기존 함수와 this 바인딩 방식이 다르고, prototype 프로퍼티가 없으며 arguments 객체를 생성하지 않는다.

## 12.5 함수 호출

### 12.5.1 매개변수와 인수

```javascript
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 호출
// 인수 1과 2가 매개변수 x와 y에 순서대로 할당되고 함수 몸체의 문들이 실행된다.
var result = add(1, 2);
```

- 매개변수의 개수와 인수의 개수가 일치하는지 체크하지 않음
- 인수가 부족할 경우에는 할당되지 않은 매개변수의 값은 undefined
- 인수가 초과됐을 경우에는 arguments 객체의 프로퍼티로 보관

```javascript
function add(x, y) {
  console.log(arguments);
  // Arguments(3) [2, 5, 10, callee: f, Symbol(Symbol.iterator): f]

  return x + y;
}

add(2, 5, 10);
```

### 12.5.2 인수 확인

```javascript
function add(x, y) {
  return x + y;
}

console.log(add(2)); // NaN
console.log(add("a", "b")); // "ab"
```

1. 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않는다.
2. 자바스크립트는 동적 타입 언어다. 따라서 자바스크립트 함수는 매개변수 타입을 사전에 지정할 수 없다.

&nbsp;매개변수에 기본값을 줘보자!(ES6)

```javascript
function add(a = 0, b = 0, c = 0) {
  return a + b + c;
}

console.log(add(1, 2, 3)); // 6
console.log(add(1, 2)); // 3
console.log(add(1)); // 1
console.log(add()); // 0
```

### 12.5.3 매개변수의 최대 개수

&nbsp;함수는 한 가지 일만 해야 하며 가급적 작게 만들어야 한다. 따라서 매개변수는 최대 3개 이상을 넘지 않는 것을 권장하고 그 이상의 매개변수가 필요하다면, 객체로 전달하는 것이 유리하다.

### 12.5.4 반환문

- 함수의 실행을 중단하고 함수 몸체를 빠져나감
- `return` 뒤에 오는 표현식을 평가해 반환, 표현식이 없으면 undefined
- 생략 가능하고 생략 시, 함수 몸체의 마지막 문까지 실행 후 암묵적으로 undefined를 반환
- 함수 몸체 내부에서만 사용 가능

## 12.6 참조에 의한 전달과 외부 상태의 변경

&nbsp;원시 값은 값 자체가 복사되어 전달되나, 객체는 참조 값이 복사되어 전달돼서 원본이 훼손된다.

## 12.7 다양한 함수의 형태

### 12.7.1 즉시 실행 함수

&nbsp;함수 정의와 동시에 즉시 호출되는 함수로, 단 한 번만 호출되며 다시 호출할 수 없다.

### 12.7.2 재귀 함수

&nbsp;재귀 호출을 수행하는 함수, 반드시 탈출 조건이 있어야한다.

### 12.7.3 중첩 함수

&nbsp;함수 내부에 정의된 함수를 말한다.

### 12.7.4 콜백 함수

&nbsp;함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 말하며, 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차 함수라고 한다.

### 12.7.5 순수 함수와 비순수 함수

- 순수 함수
  - 어떤 외부 상태에 의존하지도 않고 변경하지도 않는 함수
  - 최소 하나 이상의 인수를 전달받음
  - 부수 효과가 없는 함수
- 비순수 함수
  - 외부 상태에 의존하거나 외부 상태를 변경하는 함수
