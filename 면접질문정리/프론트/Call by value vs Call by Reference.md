# 자바스크립트에서 인자 전달

-   Call by value(값에 의한 호출)
-   Call by reference(참조에 의한 호출)

Call by value(값에 의한 호출)는 인자로 받은 값을 복사하여 처리를 한다. Call by reference(참조에 의한 호출)는 인자로 받은 값의 주소를 참조하여 직접 값에 영향을 준다.

**_간단히 말해 값을 복사를 하여 처리를 하느냐, 아니면 직접 참조를 하느냐 차이인것이다._**

## 값의 복사 (Call by value)

**Call by value** 란 값이 그대로 복사되는 것을 의미합니다. JS에서는 원시 데이터의 경우 값의 복사 Call by value가 일어납니다.

```javascript
let a = 10;
let b = a; // a의 값을 복사해서 b에 대입
console.log(`a: ${a} b: ${b}`); // 10, 10
b = 50;
console.log(`a: ${a} b: ${b}`); // 10, 50
```

함수의 인수도 마찬가지. 아래 코드에는 두 변수의 값을 교환하는 함수 swap이 있습니다.
하지만 함수가 실행되어도 처음 변수의 값을 바뀌지 않습니다. 그 이유는 a와 b는 원시데이터(정수)이기에 val1, val2에 값만 복사되었습니다.

따라서, **a, b, val1, val2** 는 저마다 별도의 값을 가지고 있습니다.

```javascript
function swap(val1, val2) {
    let temp = val1;
    val1 = val2;
    val2 = temp;
}

let a = 1;
let b = 2;
swap(a, b);
console.log(`a: ${a} b: ${b}`); // 1, 2
```

## 주소의 복사(Call by reference)

**Call by reference**는 데이터가 있는 공간(주소: 메모리의 위치)이 **참조** 되는 것을 말합니다.

아래 코드에는 두 객체가 있고, studentB에 studentA객체를 대입해주었습니다. 이때 studentB에는 studentA의 학번, 이름이 복사되는 것이 아닌 studentA의 메모리 주소가 참조됩니다. 따라서 studentA와 studentB는 같은 메모리에 있는 데이터 즉, 완전히 같은 값을 참조하는 변수입니다.

```javascript
const studentA = {
    학번: 2123,
    이름: 김무개,
};
const studentB = studentA;
console.log(`${studentA.학번}, ${studentB.학번}`); // 2123, 2123
studentB.학번 = 1111;
console.log(`${studentA.학번}, ${studentB.학번}`); // 1111, 1111
```

위의 Call by value의 swap 함수 예제를 객체를 건네주는 형태로 바꿨습니다. val1, val2는 객체 a, b의 메모리 주소를 가지고 있기에, 두 객체 a, b의 프로퍼티(value)의 값이 정상적으로 바뀌게 됩니다.

```javascript
function swap(val1, val2) {
    let temp = val1.value;
    val1.value = val2.value;
    val2.value = temp;
}

const a = {
    value: "a의 value",
};
const b = {
    value: "b의 value",
};
swap(a, b);
console.log(`a: ${a.value}, b:${b.value}`); // b의 value, a의 value 두 객체의 프로퍼티 value값이 바뀌었다.
```

배열 또한 객체이기에 Call by reference가 일어납니다.

```javascript
function swap(arr) {
    let temp = arr[0];
    arr[0] = arr[1];
    arr[1] = temp;
}

const arr = [1, 2];
swap(arr);

console.log(`arr0: ${arr[0]}, arr1:${arr[1]}`); // 2, 1
```

## 참조가 바뀌는 상황 (객체 리터럴)

두 개의 변수가 같은 객체를 가리키고 있는 상황에서 한 객체의 프로퍼티를 객체 리터럴 형식으로 변경하면 기존의 프로퍼티를 참고한 새로운 객체가 만들어지게 된다.

아래 코드에서 첫번째 콘솔이 찍혔을 때는 a와 b는 같은 메모리를 참조하고 있다.
하지만, b는 객체 리터럴 형식으로 프로퍼티를 추가하면서 b는 새로운 객체를 담아서 참조값이 변경된다.

```javascript
let a = {
    name: "dog",
};
let b = a;
console.log(`a: ${a.name}, b: ${b.name}, a===b? ${a === b}`); // dog, dog, true

b = {
    age: 231,
}; // 객체 리터럴 형식으로 age 프로퍼티 추가
console.log(`${a.age}, ${b.age}`); // undefined, 231
// 즉 a와 b는 서로 다른 객체
```

따라서, 어떤 객체를 참조하는 변수를 선언할 때는 const 형을 사용하거나, 객체 리터럴이 아닌 (.) or ["key"]를 사용하는 것을 권장합니다.
