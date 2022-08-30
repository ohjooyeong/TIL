# var, let, const 비교 설명

```
란 질문을 받으면 스코프 및 재할당을 먼저 생각하자!
```

> Javascript에서 변수는 어떠한 환경 내에서만 사용가능하다

> 기본적으로 스코프는 변수와 그 값이, 어디서부터 어디까지 유효한지를 판단하는 범위

## var, let, const의 차이점

크게 3가지로 나눌 수 있음

-   변수 재할당과 재선언
-   호이스팅
-   스코프 | 변수의 유효범위

### 변수 재할당과 재선언

> var 변수 재할당

```javascript
var fruit = "apple";
console.log(fruit); // apple

var fruit = "banana";
console.log(fruit); // banana
```

```
fruit 이라는 변수를 중복 선언했음에도 불구하고, 아무 에러없이 정상 동작된다.
> 이러한 현상은 협업이나 큰 프로젝트에서 큰 문제가 발생한다. 예를 들어 다른 개발자가 위에서 다른 변수를 선언했는데 아래 코드에서 다시 변수를 재선언해서 덮혀씌워져서 예상치 못한 오류가 발생
```

> let 변수 재할당과 재선언

```javascript
let fruit = "apple";
console.log(fruit); // apple

let fruit = "banana"; // SyntaxError: Identifier 'fruit' has already been declared
console.log(fruit);

fruit = "peach";
console.log(fruit); // peach"
```

```
위처럼 let을 통해 중복 선언을 했을 경우에는 SyntaxError가 발생되어 변수 재선언이 되지 않으나, 변수에 재할당하는 것은 가능하다.
```

> const 변수 재할당과 재선언

```javascript
const fruit = "apple";
console.log(fruit); // apple

const fruit = "banana"; // SyntaxError: Identifier 'fruit' has already been declared
console.log(fruit);

fruit = "peach"; // TypeError: Assignment to constant variable.
console.log(fruit); // apple
```

```
const 에서는 SyntaxError로 변수 재선언과 TypeError로 변수 재할당이 불가능합니다.
```

### 호이스팅

> 먼저 Javascript의 호이스팅 개념부터 알아보자면

```
호이스팅은 코드에 선언된 변수 및 함수를 코드 최상단으로 끌어올리는 것을 말하며, 이는 변수 범위가 전역 범위인지 함수 범위인지에 따라 다르게 수행될 수 있습니다. 즉, 변수가 함수 바깥에서 정의되었을 경우엔 전역 최상위로 변경이 되고, 변수가 함수내에서 정의되었을 경우는 해당 함수의 최상위로 변경됩니다.

변수의 선언이 초기화나 할당 시에 발생하는 것이 아니라, 최상위로 호이스트 되는 것입니다.

변수는 3단계에 걸쳐서 생성됩니다. 선언단계 -> 초기화 단계 -> 할당 단계
```

> var 호이스팅

```javascript
/* 스코프 선두에서 '선언단계 + 초기화 단계' 동시 실행 */
console.log(fruit); // undefined :: 변수 선언문 이전에 변수 참조 가능
var fruit;
fruit = "apple"; // 할당 단계
console.log(fruit); // apple
```

```
var로 선언된 변수는 선언 단계와 초기화 단계가 한번에 이루어집니다. 스코프 선두에서 변수 선언을 통해 메모리 공간 확보(선언단계)를 한 후, undefined로 초기화(초기화 단계)가 동시에 이루어지므로, 변수 선언문 이전에 변수를 참조할 수 있습니다. 이후에 변수 할당문에 도달했을 때 비로소 값이 할당됩니다.
```

> let 호이스팅

```javascript
/* 스코프 선두에서 '선언단계  실행*/
console.log(fruit); // ReferenceError :: 변수 선언문 이전에 변수 참조 불가
let fruit; // 초기화 단계
console.log(fruit); // undefined
fruit = "apple"; // 할당 단계
console.log(fruit); // apple
```

```
let으로 선언된 변수는 선언단계와 초기화 단계가 분리되어 진행됩니다. 스코프 선두에서 선언 단계가 실행된 후, 변수 선언문에 도달했을때 초기화(메모리 공간 확보)가 이루어집니다. 만약 변수 선언문 이전에 변수를 참조한다면, 초기화가 미리 선언되지 않았기 때문에 ReferenceError가 발생합니다. 이후에 변수 할당문에 도달했을때 값이 할당됩니다. const또한 같습니다.

※ 스코프의 시작점부터 초기화 시작점까지의 구간을 일시적 사각지대(TDZ; Temporal Dead Zone)이라고 부릅니다.
```

### 스코프 | 변수의 유효범위

```
자바스크립트는 기본적으로 function scope를 가지며, var 또한 마찬가지입니다. 반면에, let과 const는 block Scope를 가집니다.
```

> var - 함수 스코프(Function Scope)

var은 함수의 코드 블록만을 스코프로 인정하기 때문에, 함수 내부 이외에 생성한 변수는 모두 전역 변수가 되어, 전역 변수가 남발될 가능성이 있습니다

```javascript
var age = 21;
if (age >= 19) {
    var result = true;
}
console.log(result); // true
```

-   if 문 내부에 선언한 result 변수가 전역변수로 선언되어 result 값이 true로 할당되어 찍힌다.

```javascript
for (var i = 0; i < 3; i++) {
    console.log(i); // 0 1 2
}
console.log(i); // 3
```

-   for문의 변수 선언문에서 선언한 변수를 for문 외부에서 참조할 수 있다.

> let, const - 블록 스코프(Block Scope)

let과 const 경우는 모든 코드 블록 내에서 선언된 변수는 코드 블록 내에서만 유효하며, 코드 블록 외부에서는 참조할 수 없습니다. 즉, 코드 블록 내부에서 선언한 변수는 지역변수입니다.

```javascript
var age = 21;
if (age >= 19) {
    let result = true;
}
console.log(result); // result is not defined
```

-   if문 내부에 선언한 result는 지역변수로 해당 코드블록 외부에서는 참조할 수 없다.

```javascript
for (let i = 0; i < 3; i++) {
    console.log(i); // 0 1 2
}
console.log(i); // i is not defined
```

-   for문의 변수 선언문에서 선언한 변수를 for문 외부에서 참조할 수 없다.

---

정리하자면, let이나 const 대신에 var 키워드를 사용할 때, 주의를 기울이지 않으면 심각한 문제를 일으킬 수 있다.

> ※ var 사용 시 주의항목

1. 함수 레벨 스코프: 함수 코드 블록 이외에 생성한 변수는 전부 전역변수이므로 전역변수 남발 위험이 있다.

2. var 키워드 생략 허용: 암묵적 전역 변수를 양산할 가능성이 매우 큽니다.

3. 변수 중복 선언 허용: 의도하지 않은 변수값의 변경이 일어날 가능성이 큽니다.

4. 변수 호이스팅: 변수를 선언 이전에 참조가 가능합니다.
