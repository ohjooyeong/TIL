# Q. Stack 두 개를 이용하여 Queue를 구현해보세요

[답변]

queue의 enqueue()를 구현할 때 첫 번째 stack을 사용하고, dequeue()를 구현할 때 두번째 stack을 사용하면 queue를 구현할 수 있습니다.

편의상 enqueue()에 사용할 stack을 instack이라고 부르고 dequeue()에 사용할 stack을 outstack이라고 칭한다.

1. enqueue() :: instack에 push()를 하여 데이터를 저장합니다.
2. dequeue() ::
   1. 만약 outstack이 비어 있다면 instack.pop()을 하고 outstack.push()를 하여 instack에서 outstack으로 모든 데이터를 옮겨 넣습니다. 이 결과 가장 먼저 왔던 데이터는 outstack의 top의 위치하게 된다.
   2. outstack.pop()을 하면 가장 먼저 왔던 데이터가 가장 먼저 추출된다. (FIFO)

> 어디서도 배운적은 없지만 의외로 나와서 당황했던 면접 질문.
> stack 두개를 사용하여 enqueue와 dequeue를 구현하는 것에 초점을 맞춰서 문제를 해결하면 됩니다.
> 사실 이런 문제는 답이 다양하고, 답 자체가 중요하기 보단 답을 찾아가는 과정을 더 중요하게 보기 때문에, 풀이를 외우기보단 접근 방식을 주의깊게 봐야한다.

```python
class Queue(object):
  def __init__(self):
    self.instack = []
    self.outstack = []
  def enqueue(self, element):
    self.instack.append(element)
  def dequeue(self):
    if not self.outstack:
      while self.instack:
        self.outstack.append(self.instack.pop())
    return self.outstack.pop()
```

## Q. 시간복잡도는 어떻게 되는지 설명해주세요.

[답변]

- enqueue() : instack.push()를 한번만 하면 되기때문에 시간복잡도 O(1)입니다.
- dequeue() : 두가지 경우를 따져봐야 합니다. worst case는 outstack이 비어있는 경우입니다. 이때는 instack에 있는 n개의 데이터를 instack.pop()을 한 이후에 outstack.push()를 해줘야합니다. 따라서 총 2\*n번의 operation이 실행되어야 하므로 O(n)의 시간복잡도를 갖습니다.
  하지만 outstack이 비어있지 않는 경우에는 outstack.pop()만 해주면 됩니다. 이는 O(1)의 시간 복잡도를 갖습니다. 이를 종합했을 때, amortized O(1)의 시간복잡도를 갖는다고 할 수 있습니다.
