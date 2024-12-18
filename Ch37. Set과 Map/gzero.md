## 37.1 Set

Set 객체는 중복되지 않는 유일한 값들의 집합이다. Set 객체는 배열과 유사하지만 다음과 같은 차이가 있다.

| **구분**                             | **배열** | **Set 객체** |
| ------------------------------------ | -------- | ------------ |
| 동일한 값을 중복하여 포함할 수 있다. | O        | X            |
| 인덱스로 요소에 접근할 수 있다.      | O        | X            |

- **Set 객체의 생성 ⇒** `new Set`
  - Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다. 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.
  - 중복을 허용하지 않는 특성을 활용하여 배열에서 중복된 요소를 제거할 수 있다
  ```jsx
  const unip = array => [...new Set(array)]
  console.log(unip([2, 1, 2, 3, 4, 3, 4])) => [2, 1, 3, 4]
  ```
- **요소 개수 확인 ⇒** `Set.prototype.size`
- **요소 추가** ⇒ `Set.prototype.add`
  - NaN과 NaN을 같다고 평가하여 중복 추가를 허용하지 않는다
  - +0, -0은 일치 비교 연산자와(===)와 마찬가지로 같다고 평가하여 중복 추가를 허용하지 않는다
  - 자바스크립트의 모든 값을 요소로 저장할 수 있다
- **요소 존재 여부 확인 ⇒** `Set.prototype.has`
- **요소 삭제** ⇒ `Set.prototype.delete`
- **요소 일괄 삭제** ⇒ `Set.prototype.clear`
- **요소 순회 ⇒** `Set.prototype.forEach`
  - forEach 메서드는 콜백 함수와 forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체(옵션)를 인수로 전달한다.
    - 첫 번째 인수: 현재 순회 중인 요소값
    - 두 번째 인수: 현재 순회 중인 요소값
    - 세 번째 인수: 현재 순회 중인 Set 객체 자체
  - 첫 번째 인수와 두 번째 인수가 같은 이유인 이유는, `Array.prototype.forEach` 메서드와 인터페이스를 통일하기 위함이며 다른 의미는 없다.
  - Set 객체는 이터러블이여서, for … of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 된다

## 37.2 Map

Map 객체는 키와 값의 쌍으로 이루어진 컬렉션이다. Map 객체는 객체와 유사하지만 다음과 같은 차이가 있다.

| **구분**               | **객체**                | **Map 객체**          |
| ---------------------- | ----------------------- | --------------------- |
| 키로 사용할 수 있는 값 | 문자열 또는 심벌 값     | 객체를 포함한 모든 값 |
| 이터러블               | X                       | O                     |
| 요소 개수 확인         | Object.keys(obj).length | map.size              |

- **Map 객체 생성**
  - Map 생성자 함수는 이터러블을 인수로 전달받아 Map 객체를 생성한다.
  - 이때 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성되어야 한다.
  - 이터러블에 중복된 키를 갖는 요소가 존재하면 값이 덮어써진다. 그래서 Map 객체에는 중복된 키를 갖는 요소가 존재할 수 없다
  ```jsx
  const map1 = new Map([
    ["key1", "value1"],
    ["key2", "value2"],
  ]);
  console.log(map1); // Map(2) {'key1' => 'value1', 'key2' => 'value2'}
  ```
- **요소 개수 확인** ⇒ `Map.prototype.size`
- **요소 추가** ⇒ `Map.prototype.set`
  - Map 객체는 키 타입에 제한이 없다. 객체를 포함한 모든 값을 키로 사용할 수 있다.
- **요소 취득** ⇒ `Map.prototype.get`
- **요소 존재 여부 확인 ⇒** `Map.prototype.has`
- **요소 삭제** ⇒ `Map.prototype.delete`
- **요소 일괄 삭제** ⇒ `Map.prototype.clear`
- **요소 순회** ⇒ `Map.prototype.forEach`
  - forEach 메서드는 콜백 함수와 forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체(옵션)를 인수로 전달한다.
    - 첫 번째 인수: 현재 순회 중인 요소값
    - 두 번째 인수: 현재 순회 중인 요소키
    - 세 번째 인수: 현재 순회 중인 Map 객체 자체
  - Map 객체는 이터러블이여서, for … of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 된다
  - Map 객체는 이터러블이면서 동시에 이터레이터인 객체를 반환하는 메서드를 제공한다
    | **Map 메서드**        | **설명**                                  |
    | --------------------- | ----------------------------------------- |
    | Map.prototype.keys    | 요소키를 값으로 갖는 객체를 반환          |
    | Map.prototype.values  | 요소값을 값으로 갖는 객체를 반환          |
    | Map.prototype.entries | 요소키와 요소값을 값으로 갖는 객체를 반환 |
  - Map 객체를 순회하는 순서는 요소가 추가된 순서를 따른다
