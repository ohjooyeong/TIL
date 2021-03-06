# Q. Array는 어떤 자료구조인가요?

[답변]

- Array는 연관된 Data를 메모리상에 연속적이며 순차적으로 미리 할당된 크기만큼 저장하는 자료구조입니다.

> Array에 관한 질문을 할 때에는 매우 높은 확률로 Linken List(연결리스트)에 대한 질문도 함께 나온다.
> 따라서 Array의 다양한 특징 중에서 Linked List와 비교가 되는 특성들을 위주로 대답을 하게 되면 편하게 풀어나갈 수 있다.

> Array(배열)와 Linked List(연결리스트)의 가장 큰 차이점은 메모리에 저장되는 방식과 이에 따른 Operation의 연산속도(time complexity)입니다.

## Array의 특징

- 고정된 저장 공간 (fixed-size)
- 순차적인 데이터 저장(order)

### 장점

- 조회와 추가가 빠르다는 것입니다. 따라서 조회를 자주 해야되는 작업에서는 Array 자료구조를 많이 씁니다.

### 단점

- fixed-size 특성상 선언시에 Array의 크기를 미리 정해야 된다는 것입니다. 이는 메모리 낭비나 추가적인 overhead가 발생할 수 있습니다.

## 시간복잡도

- 조회 - random access | O(1)
- 추가 | O(1)
- 마지막원소 delete | O(1)
- 중간 삽입 | O(n)
- 삭제 | O(n)
- 찾기 | O(n)

## 추가

[꼬꼬무]
Q) 미리 예상한 것보다 더 많은 수의 Data를 저장하느라 Array의 size를 넘어서게 됐습니다. 이 때, 어떻게 해결할 수 있을까요?

[답변]

> 기존의 size보다 더 큰 Array를 선언하여 데이터를 옮겨 할당합니다. 모든 데이터를 옮겼다면 기존 Array는 메모리에서 삭제하면 됩니다. 이런식으로 동적으로 배열의 크기를 조절하는 자료구조를 Dynamic array라고 합니다.

> 또 다른 방법으로는, size를 예측하기 쉽지 않다면 Array 대신 Linked list를 사용함으로써 데이터가 추가될 때마다 메모리 공간을 할당받는 방식을 사용하면 됩니다.
