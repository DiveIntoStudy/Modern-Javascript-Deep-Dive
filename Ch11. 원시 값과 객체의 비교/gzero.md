| **원시 값**                                                                                                     | **객체 값**                                                                                                        |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| 원시 타입의 값으로, 변경 불가능한 값이다                                                                        | 객체 타입의 값으로, 변경 가능한 값이다                                                                             |
| 원시 값을 변수에 할당하면 변수(확보된 메모리 공간)에는 **실제 값**이 저장된다                                   | 객체를 변수에 할당하면 변수(확보된 메모리 공간)에는 **참조 값**이 저장된다                                         |
| 원시 값을 갖는 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 전달된다 (’**값에 의한 전달**’이라고 한다) | 객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다 (’**참조에 의한 전달**’이라고 한다) |

---

## 1. 원시 값

1-1. 변경 불가능한 값

- 원시 타입의 값, 즉 원시 값은 변경 불가능한 값이다. (불변성)
- ‘원시 값은 변경 불가능하다’라는 말은 원시 **값 자체를 변경할 수 없다**는 것이지 변수 값을 변경할 수 없다는 것이 아니다.
  - 변수: 언제든지 재할당을 통해 변수 값을 변경할 수 있다
  - 상수: 단 한 번만 할당이 허용되므로 변수 값을 변경할 수 없다
- 원시 값을 할당한 변수에 **새로운 원시 값을 재할당**의 과정
  - 원시 값을 할당한 변수에 **새로운 원시 값을 재할당**하면 메모리 공간에 저장되어 있는 재할당 이전의 원시 값을 변경하는 것이 아니라, **새로운 메모리 공간을 확보**하고 **재할당한 원시 값을 저장**한 후, **변수는 새롭게 재할당한 원시 값을 가리킨다.**
  - 변수가 참조하던 메모리 공간의 주소가 변경된 이유는 원시 값이 변경 불가능한 값이기 때문이다.
  - 불변성을 갖는 원시 값을 할당한 변수는 재할당 이외에 변수 값을 변경할 수 있는 방법이 없다.

1-2. 문자열과 불변성

- 원시 값인 문자열은 0개 이상의 문자로 이뤄진 집합이며, 1개의 문자는 2바이트의 메모리 공간에 저장된다. 따라서 문자열은 몇 개의 문자로 이뤄졌느냐에 따라 필요한 메모리 공간의 크기가 결정된다.
- 한번 생성된 문자열은 읽기 전용 값으로서 변경할 수 없다.

  - 문자열은 유사 배열 객체어서, 인덱스를 통해 각 문자에 접근할 수 있다
    - 유사 배열 객체 : 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고, length 프로퍼티를 가진다

  ```jsx
  var str = "string";

  // 인덱스를 사용해 각 문자에 접근할 수 있음
  console.log(str[0]); // s

  // 문자열은 유사 배열 객체여서 객체처럼 동작함
  console.log(str.length); // 6
  console.log(str.toUpperCase()); // STRING

  // 인덱스를 사용해 문자열에 접근할 수 있지만,
  // 문자열은 원시값이기 때문에 접근한 문자열을 변경할 수는 없다.
  str[0] = B; // 이때 에러는 발생하지 않는다
  ```

1-3. 값에 의한 전달

```jsx
var score = 80;

var copy = score;

console.log(score, copy); // 80, 80
console.log(score === copy); // true

score = 100;

console.log(score, copy); // 100, 80
console.log(score === copy); // false
```

- score 변수와 copy 변수의 값 80은 다른 메모리 공간에 저장된 별개의 값이다.
- score이 100으로 재할당되면 새로운 메모리 공간에 원시값 100을 저장된다.
- 따라서 score 변수 값을 변경해도 copy 변수 값에는 어떠한 영향도 주지 않는다.
- 변수에 원시 값을 갖는 변수는 할당하면 변수 할당 시점이든, 두 변수 중 어느 하나의 변수에 값을 재할당하는 시점이든, 결국은 두 변수의 원시 값은 서로 다른 메모리 공간에 저장된 별개의 값이 되어 어느 한쪽에서 재할당을 통해 값을 변경하더라도 서로 간섭할 수 없다

---

## 2. 객체

- 원시 값처럼 확보해야할 메모리 공간의 크기를 사전에 정해둘 수 없다.
- 객체는 원시 값과는 다른 방식으로 동작하도록 설계되어 있다.
- 자바스크립트 객체 관리 방식
  - 자바스크립트 객체는 프로퍼티 키를 인덱스로 사용하는 해시 테이블이라 생각할 수 있다. 하지만 높은 성능을 위해 일반적인 해시 테이블보다 나은 방법으로 객체를 구현한다
  - 자바스크립트는 **클래스 없이 객체를 생성**할 수 있으며 **객체가 생성된 이후라도 동적으로 프로퍼티와 메서드를 추가**할 수 있다. 이는 사용하기 편리하지만 성능 면에서는 이론적으로 클래스 기반 객체 지향 프로그램 언어의 객체보다 생성과 프로퍼티 접근에 비용이 더 많이 드는 비효율적인 방식이다.
  - **V8 자바스크립트 엔진**은 **히든 클래스**라는 방식을 사용해 C++ 객체의 프로퍼티에 접근하는 정도의 성능을 보장한다. 히든 클래스는 자바와 같이 고정된 객체 레이아웃(클래스)과 유사하게 동작한다
    [V8의 히든 클래스 이야기](https://engineering.linecorp.com/ko/blog/v8-hidden-class)
    [자바스크립트 엔진의 최적화 기법 (2) - Hidden class, Inline Caching : NHN Cloud Meetup](https://meetup.nhncloud.com/posts/78)

2-1. 변경 가능한 값

- 객체(참조) 타입의 값, 즉 객체는 변경 가능한 값이다
- 객체를 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간(Stack)에 접근하면 참조 값에 접근할 수 있다. 참조 값은 생성된 객체가 저장된 메모리 공간(Heap)의 주소, 그 자체다
- 객체를 할당한 변수는 재할당 없이 객체를 직접 변경할 수 있다. 재할당 없이 프로퍼티를 동적으로 추가할 수도 있고, 프로퍼티 값을 갱신할 수도 있으며 프로퍼티 자체를 삭제할 수도 있다.
- 얕은 복사와 깊은 복사

  - 얕은 복사와 깊은 복사로 생성된 객체는 원본과는 다른 객체이다.
  - 원본과 복사본은 참조 값이 다른 별개의 객체다.
  - 얕은 복사
    - 객체를 프로퍼티 값으로 갖는 객체의 한 단계까지만 복사하는 것
    - 객체에 중첩되어 있는 객체의 경우 참조 값을 복사함
  - 깊은 복사
    - 객체에 중첩되어 있는 객체까지 모두 복사하는 것을 말함
    - 객체에 중첩되어 있는 객체까지 모두 복사해서 원시 값처럼 완전한 복사본을 만듬

  ```jsx
  const o = { x: { y: 1 } };

  // 얕은 복사
  const c1 = { ...o };
  console.log(c1 === o); // false
  console.log(c1.x === o.x); // true -> 중첩되어 있는 객체의 경우 참조 값을 복사했기때문

  // 깊은 복사
  const _ = require("lodash");
  const c2 = _.cloneDeep(o);
  console.log(c2 === o); // false;
  console.log(c2.x === o.x); // false -> 중첩되어 있는 객체까지 복사해서 완전한 복사본을 만듬
  ```

2-2. 참조에 의한 전달

- 객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다. 이를 참조에 의한 전달이라 한다
- 즉, 두 개의 식별자가 하나의 객체를 공유한다는 것을 의미한다. 이는 원본 또는 사본 중 어느 한쪽에서 객체를 변경하면 서로 영향을 주고 받는다

```jsx
var person = {
	name: "Lee"
}

// 참조 값을 얕은 복사. copy와 person은 동일한 참조 값을 갖는다
var copy = person;

console.log(copy === person) // true

copy.name: 'Kim';
person.address = 'Seoul'

console.log(person) // {name: "Kim", address: "Seoul"}
console.log(copy) // {name: "Kim", address: "Seoul"}
```

```jsx
var person1 = {
  name: "Lee",
};

var person2 = {
  name: "Lee",
};

console.log(person1 === person2); // false
console.log(person1.name === person2.name); // true
```

- `person1 === person2` 가 `false`인 이유는?
  - 객체를 할당한 변수는 참조 값을 가지고 있고, 객체 리터럴은 평가될 때마다 객체를 생성한다. 따라서 person1과 person2는 내용은 같지만 다른 메모리에 저장된 별개의 객체이다. 즉, person1과 person2 변수의 참조 값은 다른 값이다
- `person1.name === person2.name` 이 `true`인 이유는?
  - [person1.name](http://person1.name) 과 person2.name은 값으로 평가될 수 있는 표현식이다. 두 표현식 모두 원시 값 ‘Lee’로 평가되어, true이다.

---

### ✳️ 코드평가 및 런타임을 메모리와 연관지어 생각해보기

### 1. **코드 평가 단계** (Compilation / Parsing Phase)

자바스크립트는 기본적으로 **인터프리터** 언어이지만, 현대의 자바스크립트 엔진(V8, SpiderMonkey 등)은 **JIT(Just-In-Time) 컴파일러**를 사용해 코드를 평가합니다. 코드 평가 단계는 크게 두 가지로 나눌 수 있습니다:

- **구문 분석(Parsing)**: 자바스크립트 코드는 먼저 **추상 구문 트리(AST)**로 변환됩니다. 이는 코드의 구조를 표현하는 트리 형식의 데이터 구조입니다.
- **호이스팅(Hoisting)**: 변수 선언과 함수 선언이 먼저 처리됩니다. `var`로 선언된 변수는 스코프의 최상단으로 끌어올려지고, 함수 선언도 마찬가지입니다. 하지만 실제 값의 할당은 이후 런타임 단계에서 이루어집니다.

이 단계에서 변수를 위한 메모리 공간이 **할당되지 않으며**, 변수명은 심볼 테이블과 같은 구조에서 관리됩니다. 실제 메모리 할당은 런타임 단계에서 이루어집니다.

### 2. **런타임 단계** (Execution Phase)

코드가 평가된 후, 실제로 코드가 실행되는 **런타임 단계**에서는 변수에 값을 할당하거나 연산을 수행하게 됩니다. 이 단계에서 메모리 관리가 본격적으로 이루어집니다.

### 변수의 메모리 할당과 저장 과정

변수와 값이 메모리에 저장되는 방식은 데이터의 종류에 따라 다릅니다.

- **원시값(Primitive Values)**: 숫자, 문자열, 불리언 등과 같은 원시값은 **스택(Stack) 메모리**에 저장됩니다. 원시값은 고정된 크기를 가지므로 스택에서 빠르게 할당되고 해제될 수 있습니다.
  - 예: `let x = 10;`이 경우 `x`라는 변수는 스택 메모리에 저장되며, 값 `10`도 함께 스택에 저장됩니다.
- **참조값(Reference Values)**: 객체, 배열, 함수 등은 **힙(Heap) 메모리**에 저장됩니다. 이들은 크기가 가변적이기 때문에 힙 메모리에 할당되며, 변수는 해당 데이터가 저장된 힙 메모리의 **참조값(메모리 주소)**을 가지게 됩니다.
  - 예: `let obj = { name: "Alice" };`이 경우 `obj`라는 변수는 스택 메모리에 저장되지만, 그 값은 힙 메모리에 있는 객체를 참조하는 메모리 주소를 가집니다. 실제 객체 데이터 `{ name: "Alice" }`는 힙에 저장됩니다.

### 실행 과정에서 메모리 관리

- **변수의 값 할당**: 런타임 시 변수에 값이 할당될 때, 원시값은 스택에, 참조값은 힙에 저장됩니다. 이 때 변수명은 스코프 내에서 심볼 테이블을 통해 참조됩니다.
- **함수 호출**: 함수가 호출되면 함수의 매개변수, 지역변수 등이 **스택**에 저장됩니다. 함수가 종료되면 해당 스택 프레임이 제거됩니다.
- **가비지 컬렉션**: 자바스크립트 엔진은 **가비지 컬렉터(Garbage Collector)**를 사용하여 더 이상 참조되지 않는 힙 메모리의 데이터를 자동으로 해제합니다. 이는 명시적으로 메모리 해제를 하지 않아도 되는 자바스크립트의 특성 중 하나입니다.

### 예시 코드로 메모리 동작 이해하기

```jsx
let a = 20; // a는 스택에 저장, 값 20도 스택에 저장됨
let obj = { name: "Alice" }; // obj는 스택에 저장, { name: "Alice" }는 힙에 저장됨

function greet() {
  let greeting = "Hello"; // greeting은 함수 호출 시 스택에 저장됨
  console.log(greeting);
}

greet(); // greet 함수 호출 시, greeting 값이 스택에 저장됨
```

1. **`let a = 20;`**
   - `a`라는 변수는 스택에 저장되고, 그 값 `20`도 스택에 저장됩니다. 원시값이므로 스택에 바로 저장됩니다.
2. **`let obj = { name: "Alice" };`**
   - `obj`라는 변수는 스택에 저장되지만, 객체 `{ name: "Alice" }`는 힙에 저장됩니다. 스택의 `obj` 변수는 힙의 메모리 주소를 참조합니다.
3. **`greet()` 함수 호출**
   - 함수가 호출되면 함수 내부의 `greeting` 변수는 스택에 저장됩니다. 함수 실행이 끝나면 스택 프레임이 제거되어 `greeting` 변수는 해제됩니다.

### 결론: 자바스크립트 변수의 메모리 저장 위치

- **코드 평가 단계**에서는 변수명이나 함수명이 심볼 테이블과 같은 데이터 구조로 관리됩니다. 이 단계에서 메모리에 할당되는 것은 없습니다.
- **런타임 단계**에서는 변수가 값에 따라 스택 또는 힙 메모리에 할당됩니다.
  - 원시값은 **스택** 메모리에 할당됩니다.
  - 참조값(객체, 배열, 함수)은 힙에 할당되고, 변수는 그 **참조값(메모리 주소)**을 스택에 저장합니다.

이렇게 자바스크립트는 변수에 따라 스택과 힙 메모리를 나누어 관리하며, 가비지 컬렉터를 통해 불필요한 메모리를 자동으로 해제합니다.

---

### ✳️ 심볼테이블

심볼 테이블(Symbol Table)은 코드 실행 시 변수나 함수의 이름과 그에 해당하는 메모리 주소를 관리하는 데이터 구조입니다. 자바스크립트 코드가 실행되는 과정에서 심볼 테이블은 자바스크립트 엔진에 의해 사용되며, 이를 통해 변수명이나 함수명을 메모리의 실제 값이나 참조로 연결하게 됩니다.

### 1. **심볼 테이블의 역할**

심볼 테이블은 자바스크립트 엔진이 코드 평가와 실행 단계에서 변수를 효율적으로 관리하기 위해 사용합니다. 자바스크립트 엔진은 심볼 테이블을 사용해 변수와 함수의 이름을 메모리 주소와 연결하고, 그에 따라 코드를 실행할 때 올바른 메모리 위치를 참조합니다.

심볼 테이블은 기본적으로 다음과 같은 역할을 합니다:

- 변수명과 그에 상응하는 메모리 주소 관리
- 함수 선언과 변수 선언을 관리하여 해당 변수나 함수가 올바른 위치에서 참조될 수 있도록 함
- 특정 스코프 내에서 사용되는 식별자(identifier)를 추적

### 2. **심볼 테이블은 어디에 저장되나?**

심볼 테이블은 **자바스크립트 엔진의 내부 데이터 구조**로 관리됩니다. 이 엔진 내부에서 심볼 테이블은 메모리의 특정 영역에 위치하지 않고, **엔진의 메모리 관리 영역**에서 동적으로 관리됩니다. 스택이나 힙처럼 고정된 위치가 아니라, 자바스크립트 엔진이 메모리를 효율적으로 관리하는 구조의 일부로써 존재합니다.

### 3. **실행 시 심볼 테이블이 어떻게 작동하는가?**

자바스크립트 코드가 실행될 때 심볼 테이블은 다음과 같은 방식으로 작동합니다:

- **코드 평가 단계**: 코드가 실행되기 전에, 자바스크립트 엔진은 변수와 함수 선언을 처리하며, 이를 심볼 테이블에 기록합니다. 심볼 테이블은 각 변수나 함수가 어느 메모리 주소를 참조해야 하는지 추적합니다.
- **코드 실행 단계**: 코드가 실행될 때, 엔진은 심볼 테이블을 참조하여 변수나 함수의 이름을 실제 메모리 주소와 연결합니다. 따라서 심볼 테이블은 변수명, 함수명 같은 식별자를 실제 메모리 공간에 연결하는 "맵(map)" 역할을 합니다.

### 4. **심볼 테이블의 메모리 위치**

심볼 테이블은 자바스크립트 엔진 내부의 데이터 구조로서, 엔진이 할당한 메모리 영역(엔진 내부 스택 또는 힙의 일부)에 저장됩니다. 심볼 테이블 자체가 명시적으로 스택 또는 힙에 있다고 말할 수는 없지만, 자바스크립트 엔진이 관리하는 메모리 공간 내에서 관리됩니다.

- 각 스코프(전역, 함수, 블록 등)에 대해 개별적으로 심볼 테이블이 존재할 수 있습니다.
- 특정 스코프가 종료되면 해당 스코프와 관련된 심볼 테이블도 더 이상 필요 없어지고, 가비지 컬렉터가 이를 정리합니다.

### 예시

```jsx
function myFunction() {
  let x = 10; // 'x'가 심볼 테이블에 등록됨
  console.log(x); // 심볼 테이블을 통해 'x'의 값 10이 찾아짐
}

myFunction();
```

위 코드에서 `myFunction()`이 호출될 때, 함수의 스코프 안에서 심볼 테이블이 생성되고, `x` 변수가 심볼 테이블에 기록됩니다. 그 후 `x`의 값을 읽을 때, 심볼 테이블을 통해 `x`가 가리키는 메모리 주소를 찾아 값을 반환하게 됩니다.

### 결론

심볼 테이블은 자바스크립트 엔진이 변수와 함수의 이름을 메모리 주소와 연결하기 위해 사용하는 데이터 구조입니다. 심볼 테이블은 자바스크립트 엔진의 **내부 구조**로 존재하며, 명시적으로 스택이나 힙 같은 특정 메모리 영역에 고정되지 않고, 자바스크립트 엔진이 실행 시 필요한 메모리 공간에서 관리됩니다. 이를 통해 자바스크립트 엔진은 변수와 함수의 참조를 효율적으로 처리할 수 있습니다.
