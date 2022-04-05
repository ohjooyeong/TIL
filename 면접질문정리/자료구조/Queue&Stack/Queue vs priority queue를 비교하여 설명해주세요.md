# Q. Queue vs priority queue를 비교하여 설명해주세요.

[답변]
Queue는 자료구조는 시간 순서상 먼저 집어넣은 데이터가 먼저 나오는 선입선출 FIFO구조로 저장하는 형식입니다. 이와 다르게 우선순위큐 (priority queue)는 들어간 순서에 상관없이 우선순위가 높은 데이터가 먼저 나옵니다

- Queue의 operation 시간복잡도는 enqueue O(1), dequeue O(1)이고,
- Priority queue는 push O(logn), pop O(logn) 입니다.

[TIP]

> 면접질문에서 우선순위큐를 잘 답하기 위해서는 구현 방법과 operation의 시간복잡도를 잘 설명할 수 있어야 합니다.

> 우선순위큐를 구현하라고 하면 Heap을 구현하면 됩니다. Heap 자료구조는 이진완전트리를 활용하는 것이고, 대표적인 operation의 시간복잡도는 push O(logn), pop O(logn) 입니다. 이 두가지 특징을 중심으로 공부해가면 됩니다.

> 또한 tree가 그려져 있는 상태에서 최대힙, 최소힙의 삽입과 삭제시에 어떻게 node가 삭제되고 연결이 변경되는지의 과정을 그려서 설명할 수 있다면 더 좋습니다.

## Heap

```
Heap은 그 자체로 우선순위큐(priority queue)의 구현과 일치합니다.
```

Heap은 완전이진트리 구조입니다. Heap이 되기 위한 조건은 다음과 같습니다.

- 각 node에 저장된 값은 child node 들에 저장된 값보다 크거나 같다(max heap)
  - root node에 저장된 값이 가장 큰 값이 된다.
- 각 node에 저장된 값은 child node들에 저장된 값보다 작거나 같다(min heap)
  - root node에 저장된 값이 가장 작은 값이 된다.

### Heap 구현

트리는 보통 Linked list로 구현합니다. 하지만 Heap은 tree임에도 불구하고 array를 기반으로 구현해야합니다. 그 이유는 새로운 node를 힙의 '마지막 위치'에 추가해야 하는데, 이 때 array기반으로 구현해야 이 과정이 수월해지기 때문입니다.

- 구현의 편의를 위해 array의 0번째 index는 사용하지 않습니다.
- 완전이진트리의 특성을 활용하여 array의 index만으로 부모 자식간의 관계를 정의합니다.
  - n번째 node의 left child node = 2n
  - n번째 node의 right child node = 2n + 1
  - n번째 node의 parent node = n / 2

### Heap push - O(logn)

heap tree의 높이는 logN입니다.
push()를 했을 때, swap하는 과정이 최대 logN번 반복되기 때문에 시간복잡도는 O(logn)입니다.

### Heap pop - O(logn)

pop()을 했을 때, swap하는 과정이 최대 logN번 반복되기 때문에 시간복잡도는 O(logn)입니다.
