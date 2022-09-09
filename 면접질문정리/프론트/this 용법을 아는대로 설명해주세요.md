# 자바스크립트에서 This란 무엇인가?

this의 값은 함수가 호출되는 방식에 따라 달라집니다.

1. 함수를 호출할 때 new 키워드를 사용하는 경우
    - 함수 내부에 있는 this는 완전히 새로운 객체입니다.
2. apply, call, bind가 함수의 호출/생성에 사용되는 경우
    - 함수 내의 this는 인수로 전달된 객체입니다.
3. obj.method()와 같이 함수를 메서드로 호출하는 경우,
    - this는 함수가 프로퍼티인 객체입니다.
4. 함수가 전역 스코프에서 익명함수로 호출되는 경우,
    - 위의 조건없이 호출되는 경우 this는 전역 객체입니다. 브라우저에서는 window객체입니다. 엄격 모드("use strict")일 경우, this는 전역 객체 대신 undefined 가 됩니다.

위의 규칙 중 다수가 적용되면 더 상위 규칙이 승리하고 this 값을 설정합니다.

## 일반함수의 this와 화살표 함수의 this는 어떻게 다른가?

함수가 ES2015 화살표 함수인 경우, 위의 모든 규칙을 무시하고 생성된 시점에서 주변 스코프의 this 값을 받습니다.

화살표 함수와 일반 함수는 this가 다른 곳을 가리키는데,

-   화살표 함수의 this는 바로 상위 스코프의 this를 가리킨다.
-   일반 함수는 this가 동적으로 바인딩 됩니다.
    -   일반 함수의 this는 내부 함수, 콜백함수: 전역 객체, 객체의 메소드, 생성자 함수입니다.

use strict 모드에서의 this?
엄격 모드일 경우, this는 전역객체 대신 undefined 가 됩니다.

## Call, Apply, Bind 함수에 대해 설명해달라

### Call, Apply

```javascript
function add(a, b) {
    return a + b;
}

console.log(add.call(null, 1, 2)); // 3
console.log(add.apply(null, [1, 2])); // 3
```

Call과 Apply는 함수를 호출하는데 사용하며 , 첫 번째 매개변수는 함수 내에서 this의 값으로 사용됩니다. 그러나 이 둘의 차이점은

-   Call은 쉼표로 구분된 인수를 두번째 인수로 취하고
-   Apply는 인수의 배열을 두번째 인수로 취합니다.
-   Call은 C:Comma로 구분되며, Apply는 인수 배열인 A:Arguments라고 기억하면 쉽습니다. 그냥 실행하는 것이 아닌 첫번째 this로 setting하고 싶은 객체를 넘겨주어 this를 바꾸고 나서 실행한다. call과 apply의 차이점은 첫번째 인자(this를 대체할 값)를 제외하고 실제 함수 호출에 필요한 파라미터를 넣어야 한다. call과 다르게 apply 함수는 두번째 인자부터 모두 배열에 넣어야 한다.

## Bind

```javascript
const module = {
    x: 42,
    getX: function () {
        return this.x;
    },
};

const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// expected output: undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// expected output: 42
```

Bind 함수가 call과 apply와 다른 점은 함수를 실행하지 않으며 새로운 바인딩한 함수를 만듭니다 . 바인딩한 함수는 원본 함수 객체를 감싸는 함수로, ECMAScript 2015에서 말하는 특이 함수 객체(exotic function object) 입니다. 바인딩한 함수를 호출하면 일반적으로 래핑된 함수가 호출 됩니다.
