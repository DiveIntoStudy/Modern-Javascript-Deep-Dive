4.1 변수란 무엇인가?

변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름

---

4.2 식별자

- 식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다.
- 식별자는 값이 저장되어 있는 메모리 주소와 매핑 관계를 맺으며, 이 매핑 정보도 메모리에 저장되어야 한다.
- 식별자는 값이 아니라 메모리 주소를 기억하고 있다.

---

4.3 변수선언

- 변수를 사용하려면 반드시 선언이 필요하다
- 변수를 선언할 때는 var, let, const 키워드를 사용한다
  - var 키워드 단점
    - 블록 레벨 스코프를 지원하지 않고 함수 레벨 스코프를 지원해서, 의도치 않게 전역 변수가 선언되어 심각한 부작용이 발생하기도 한다
- 변수 선언
  - 변수를 생성하는 것을 말한다
  - 메모리 공간을 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것이다.
  - 변수 선언에 의해 확보된 메모리 공간은 확보가 해제되기 전까지 누구도 확보된 메모리 공간을 사용할 수 없도록 보호되므로 안전하게 사용할 수 있다.
- 변수 선언 2단계
  - 선언 단계 : 변수 이름을 등록해서 자바스크립트 엔진에 변수의 존재를 알린다
  - 초기화 단계 : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화 한다.
- 변수 이름은 어디에 등록 되는걸까?
  - 등록과 저장의 단어 의미를 구분해야한다. 책의 내용으로는 부족해서 아래 내용을 조금 더 찾아봤다.
  - 자바스크립트 변수명(식별자)과 참조하는 메모리 주소를 저장하는 곳은 심볼테이블(메모리 상에서 작동하는 자료구조)이다.
  - 심볼테이블은 실행컨텍스트 내에서 관리된다.
    - 실행컨텍스트는 자바스크립트 코드가 실행될 때마다 생성되는 ‘환경’이다
    - 실행컨텍스트는 변수 객체, 스코프 체인, this 값을 가지고 있다.
  - 실행 컨텍스트는 코드가 실행되는 환경을 정의하고, 해당 환경 안에서 변수를 어떻게 접근할 지 결정한다.
  - 심볼 테이블은 실행 컨텍스트 내부에서 식별자와 메모리 주소를 연결하여 변수를 빠르게 찾을 수 있도록 돕는다.

---

4.4 변수 선언의 실행 시점과 변수 호이스팅

변수 선언의 실행 시점

- 자바스크립트 엔진은 런타임에 앞서 소스코드의 평가 과정을 거치면서 소스코드 실행 준비를 한다.
- 실행 준비 단계에서 자바스크립트 엔진은 변수 선언을 포함한 모든 선언문(변수 선언문, 함수 선언문 등)을 소스코드에서 찾아내 먼저 실행한다.
- 소스코드 평가 과정이 끝나면 선언문을 제외하고 소스코드를 한 줄씩 순차적으로 실행한다

변수 호이스팅

- 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징

---

4.5 값의 할당

- 변수 선언은 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 먼저 실행된다
- 값의 할당은 소스코드가 순차적으로 실행되는 시점인 런타임에 실행된다.

---

4.6 값의 재할당

- 재할당이란 이미 값이 할당되어 있는 변수에 새로운 값을 또다시 할당하는 것이다. 이전 메모리 공간을 지우고, 새로운 메모리 공간을 확보해서 재할당 값을 저장하는 것이다.
- var 키워드로 선언한 변수는 선언과 동시에 undefined로 초기화되기 때문에 엄밀히 말하자면 변수에 처음으로 값을 할당하는 것도 사실은 재할당이다
- 값을 재할당할 수 없어서 변수에 저장된 값을 변경할 수 없다면 변수가 아니라 상수(constant)라 한다

---

4.7 식별자 네이밍 규칙

- 자바스크립트는 대소문자를 구별한다
- 변수나 함수의 이름에는 카멜 케이스를 사용한다
- 생성자 함수, 클래스 이름에는 파스칼 케이스를 사용한다
