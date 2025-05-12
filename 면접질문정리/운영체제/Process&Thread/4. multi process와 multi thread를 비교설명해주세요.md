# Q. multi process와 multi thread를 비교설명해주세요.

[답변]

- multi thread는 multi process보다 적은 메모리 공간을 차지하고 <u>Context Switching이 빠릅</u>니다.
- multi process는 multi thread보다 많은 메모리 공간과 CPU 시간을 차지합니다.
- multi thread는 동기화 문제와 하나의 thread 장애로 전체 thread가 종료될 위험이 있습니다.
- multi process는 하나의 process가 죽더라도 다른 process에 영향을 주지 않아 안정성이 높습니다

> Context Switching이 빠름: 멀티 프로세스와 다르게 Context switching시 캐시 메모리를 초기화할 필요가 없기때문입니다.

[TIP]

> 두 방법은 동시에 여러 작업을 수행한다는 측면에서 유사한 면이 있습니다. 적용할 시스템에 따라 두 방법의 장단점을 고려하여 적합한 방식을 선택해야 합니다.

> 메모리 구분이 필요할 떄는 multi process가 유리합니다. 반면에 Context switching이 자주 일어나고 데이터 공유가 빈번한 경우, 그리고 자원을 효율적으로 사용해야 되는 경우에는 multi thread를 사용하는 것이 유리합니다.

> 비교하여 설명하라는 면접 질문이 나오면 위에 적어드린 내용 안에서 설명을 하시면 됩니다.

## Multi process & Multi thread

multi process 대신 multi thread로 구현할 경우, 메모리 공간과 시스템 자원 소모가 줄어들게 됩니다. 하지만 multi thread를 사용할 때는 thread간 자원을 공유하기 때문에 <u>동기화문제</u>가 발생할 수 있기 때문에 이를 고려한 프로그램 설계가 필요합니다.

또한, process간의 통신(IPC)보다 thread간의 통신 비용이 적기 때문에 통신으로 인한 오버헤드가 적습니다.

> 동기화 문제: 서로 다른 thread가 메모리 영역을 공유하기 때문에 여러 thread가 동일한 자원에 동시에 접근하여 엉뚱한 값을 읽거나 수정하는 문제입니다

|               |                                  |                   |        |
| ------------- | -------------------------------- | ----------------- | ------ |
|               | 메모리 사용 / CPU 시간           | Context switching | 안정성 |
| multi process | 많은 메모리 공간 / CPU 시간 차지 | 느림              | 높음   |
| multi thread  | 적은 메모리 공간 / CPU 시간 차지 | 빠름              | 낮음   |

### Q. multi thread가 multi process보다 좋은 점은 무엇인가요?

[답변]

multi process를 이용하던 작업을 multi thread로 구현할 경우, 메모리 공간과 시스템 자원 소모가 줄어들게 됩니다. 또한 process를 생성하고 자원을 할당하는 등의 system call을 생략할 수 있기 때문에 자원을 효율적으로 관리할 수 있습니다. 뿐만 아니라 Context switching 시 캐시 메모리를 초기화할 필요가 없어서 속도가 빠릅니다.

데이터를 주고 받을 때를 비교해보면, process간의 통신(IPC)보다 multi thread 간의 통신 비용이 적기 때문에 통신으로 인한 <u>오버헤드가 적습니다.</u>

> 오버헤드가 적습니다: 통신 시 별도의 자원을 이용하지 않고, process에 할당된 Heap 영역등을 이용하여 데이터를 주고 받기 때문입니다.

### Q. multi thread가 multi process보다 안좋은 점은 무엇인가요?

[답변]

thread간의 자원 공유 시 동기화문제가 발생할 수 있어서 프로그램 설계 시 주의가 필요하고, 하나의 thread에 문제가 생기면 process내의 다른 thread에도 문제가 생길 수 있습니다.
