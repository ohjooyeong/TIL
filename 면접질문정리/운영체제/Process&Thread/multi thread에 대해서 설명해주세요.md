Q. Multi thread에 대해서 설명해주세요.
[답변]

thread는 한 process 내에서 실행되는 동작(기능 function)의 단위입니다. 각 thread는 속해있는 process의 Stack 메모리를 제외한 나머지 memory 영역을 공유할 수 있습니다.

Multi thread란 하나의 process가 동시에 여러개의 일을 수행할 수 있도록 해주는 것입니다. 즉, 하나의 process에서 (실행이 된 하나의 program에서) 여러 작업을 병렬로 처리하기 위해 multi thread를 사용합니다.
multi thread에서는 한 process 내에 여러개의 thread가 있고, 각 thread들은 Stack 메모리를 제외한 나머지 영역(Code, Data, Heap) 영역을 공유하게 됩니다.

[TIP]

> thread는 process내에서 독립적인 기능을 수행합니다. 즉, 독립적으로 함수를 호출함을 의미하고 이를 위해 stack memory가 각자 필요한 것입니다. thread가 무엇인지 이해하고, multi process와 어떤 점이 다른지를 생각해보면서 공부하면 됩니다.
> 또한, 독립적인 stack memory와 PC Register가 필요하다는 점을 잘 기억합시다

## Thread와 multi thread

thread는 process 내에서 독립적인 기능을 수행합니다. 각 thread가 독립적인 기능을 수행한다는 것은 독립적으로 함수를 호출함을 의미합니다.

## Stack memory & PC register

thread가 함수를 호출하기 위해서는 인자 전달, Return Address 저장, 함수 내 지역변수 저장 들을 위한 독립적인 stack memory 공간을 필요로 합니다. 결과적으로 thread는 process로부터 Stack memory 영역은 독립적으로 할당받고, Code, Data, Heap 영역은 공유하는 형태를 갖게 됩니다.

또한 multi thread에서는 각각의 thread마다 PC register를 가지고 있어야 합니다. 그 이유는 한 process내에서도 thread끼리 context switch가 일어나게 되는데, PC register에 code address가 저장되어 있어야 이어서 실행을 할 수 있기 때문입니다.

### Q. thread는 왜 독립적인 stack memory영역이 필요한가요?

[답변]

Stack 영역은 함수 호출 시 전달되는 인자, 함수의 Return Address, 함수 내 지역변수 등을 저장하기 위한 memory영역입니다. thread가 process내에서 "독립적인 기능을 싱행" 한다는 것은 "독립적으로 함수를 호출"함을 의미합니다. 따라서 각 thread가 독립적인 동작을 싱해하기 위해서는 각 thread의 stack memory영역이 독립적이여야 합니다.

### Q. process와 thread를 비교설명해주세요.

[답변]

process는 운영체제로부터 자원을 할당받는 작업의 단위이고, thread는 process가 할당받은 자원을 이용하는 실행의 단위입니다. 즉, process는 실행파일이 memory에 적재되어 CPU를 할당받아 실행되는 것입니다. thread는 한 process내에서 실행되는 동작의 단위입니다.
process는 memory공간에 code, data, heap, stack영역이 있는데, thread는 process내에서 stack영역을 제외한 code, data, heap영역을 공유합니다.
