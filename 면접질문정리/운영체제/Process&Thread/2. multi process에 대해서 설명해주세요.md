# Q. multi process에 대해서 설명해주세요

[답변]

Multi process란 2개 이상의 process가 동시에 실행되는 것을 말합니다. 동시에라는 말은 동시성(concurrency)과 병렬성(parallelism) 두 가지를 의미합니다.

동시성은 CPU core가 1개일 때, 여러 process를 짧은 시간동안 번갈아 가면서 연산을 하게 되는 시분할 시스템(time sharing system)으로 실행되는 것입니다.

병렬성은 CPU core가 여러개일 때, 각각의 core가 각각의 process를 연산함으로써 process가 동시에 실행되는 것입니다.

[TIP]

> 요새 우리가 쓰는 노트북은 CPU core가 여러개 있습니다. core가 여러개여서 실제로 여러 process가 동시에 처리되는 것을 병렬성이라고 합니다. 하지만 면접에서는 병렬성에 대한 깊은 질문은 거의 나오지 않습니다. 다만 병렬성이 어떤 뜻인지 정도만 이해하고 넘어가시면 됩니다.

> 면접에서 병렬성보다 훨씬 중요한 것은 동시성입니다. 한 개의 CPU core는 당연히 한번에 하나의 연산밖에 못합니다. 그런데 도대체 어떻게 동시에 여러 process를 처리할까요? 정답은 동시성입니다. 동시성을 통해 multi process가 작동되는 원리를 잘 이해하면 됩니다.
> 면접에서는 시분할 시스템을 시작으로 context, PCB, context switching, process의 memory 영역을 설명하면 완벽한 답변이 됩니다.

## 동시성(Concurrency) vs 병렬성(Parallelism)

|          |                                 |                                     |
| -------- | ------------------------------- | ----------------------------------- |
|          | 동시성                          | 병렬성                              |
| Core입장 | 싱글 코어                       | 멀티 코어                           |
| 처리방법 | 동시에 실행되는 것 같아 보인다. | 실제로 동시에 여러 작업이 처리된다. |

## 장점과 단점

### 장점

-   독립된 구조이기 때문에 안정성이 높다.
-   여러 프로세스가 같이 작업하고 있기 때문에 하나의 프로세스가 죽는다해도 문제가 확산되지 않는다.
-   여러 개의 프로세스가 처리되어야 할 때 동일한 데이터를 사용하고, 이러한 데이터를 하나의 디스크에 두고 모든 프로세서(CPU)가 이를 공유하면 비용적으로 저렴해짐

### 단점

-   멀티 스레드보다 많은 메모리 공간과 CPU 시간을 차지한다.
-   독립된 메모리 영역이기 때문에 작업량이 많을수록 오버헤드가 발생하여 성능 저하가 발생할 수 있다.
    -   context switching 과정에서 캐시 메모리 초기화 등 무거운 작업이 진행되고 시간이 소모되는 등 오버헤드 발생
-   Context Switching이란?
    -   CPU는 한 번에 하나의 프로세스만 실행 가능
    -   CPU에서 여러 프로세스를 돌아가면 작업을 처리하는 데 이 과정을 Context-Switching이라고 함.
    -   즉, 동작중인 프로세스가 대기하면서 해당 프로세스 상태(Context)를 보관하고, 대기하고 있던 다음 순서의 프로세스가 동작하면서 이전에 보관했던 프로세스의 상태를 복구하는 작업

## Multi process

Multi process란 2개 이상의 process가 동시에 실행되는 것을 말합니다. 이 때, process들은 CPU와 메모리를 공유하게 됩니다.

memory의 경우에는 여러 process들이 각자의 memory영역을 차지하여 동시에 적재됩니다.

반면 하나의 CPU는 매 순간 하나의 process만 연산할 수 있습니다. 하지만 CPU의 처리 속도가 워낙 빨라서 수 ms 이내의 짧은 시간동안 여러 process들이 CPU에서 번갈아 실행되기 때문에 사용자 입장에서는 여러 프로그램이 동시에 실행되는 것처럼 보입니다. 이처럼 CPU의 작업시간을 여러 process들이 조금씩 나누어 쓰는 시스템을 시분할 시스템(time sharing system)이라고 부릅니다.

### 메모리관리

여러 process가 동시에 memory에 적재된 경우, 서로 다른 process의 영역을 침범하지 않도록 각 process가 자신의 memory영역에만 접근하도록 운영체제가 관리해줍니다.

### CPU의 연산과 PC register

CPU는 PC(Program counter) register가 가리키고 있는 명령어를 읽어들여 연산을 진행합니다. PC register에는 다음에 실행될 명령어의 주소값이 저장되어 있습니다. multi process시스템에서는 process1이 진행되고 있을 때는 process1의 code영역을 PC register가 가리키다가, process2가 진행되면 process2의 code영역을 가리키게 됩니다. CPU는 PC register가 가리키는 곳에 따라 process를 변경해가면서 명령어를 읽어들이고 연산을 하게 됩니다.

## Context

시분할 시스템에서는 한 process가 매우 짧은 시간동안 CPU를 점유하여 일정부분의 명령을 수행하고, 다른 process에게 넘깁니다. 그 후 차례가 되면 다시 CPU를 점유하여 명령을 수행합니다. 따라서 이전에 어디까지 명령을 수행했고, register에는 어떤 값이 저장되어 있었는지에 대한 정보가 필요하게 됩니다. process가 현재 어떤 상태로 수행되고 있는지에 대한 총제적인 정보가 바로 context입니다. context 정보들은 PCB(Process Control Block)에 저장을 합니다.

### PCB(Process Control Block)

PCB는 운영 체제가 프로세스를 표현한 자료구조입니다. PCB에는 프로세스의 중요한 정보가 포함되어 있기때문에, 일반 사용자가 접근하지 못하도록 보호된 메모리 영역안에 저장이 됩니다. 일부 운영 체제에서 PCB는 커널 스택의 위치합니다. 이 메모리 영역은 보호를 받으면서도 비교적 접근하기가 편리하기 때문입니다.

PCB에는 일반적으로 다음과 같은 정보가 포함됩니다.

| PCB                 |                                                                 |
| ------------------- | --------------------------------------------------------------- |
| Process State       | new, running, waiting, halted 등의 state가 있다.                |
| Process Number      | 해당 process의 number                                           |
| Program counter(PC) | 해당 process가 다음에 실행할 명령어의 주소를 가리킨다.          |
| Registers           | 컴퓨터 구조에 따라 다양한 수와 유형을 가진 register 값들        |
| Memory limits       | base register, limit register, page table 또는 segment table 등 |

### Context switch

Context switch란 한 프로세스에서 다른 프로세스로 CPU 제어권을 넘겨주는 것을 말합니다.
이 때 이전의 프로세스의 상태를 PCB에 저장하여 보관하고 새로운 프로세스의 PCB를 읽어서 보관된 상태를 복구하는 작업이 이루어집니다.

### Q. process의 context가 무엇인지 설명하시오

[답변]

context란 process가 현재 어떤 상태로 수행되고 있는지에 대한 정보입니다. 해당 정보는 PCB에 저장을 합니다.

### Q. PCB에 저장되는 것들은 무엇이 있는지 설명하시오

[답변]

PCB는 운영체제가 process에 대해 필요한 정보를 모아놓은 자료구조입니다. PCB에는 일반적으로 다음과 같은 정보가 포함됩니다.

-   Process Number
-   Process State
-   Program Counter (PC), 레지스터
-   CPU 스케쥴링 정보, 우선순위
-   메모리 정보 (해당 process의 주소 공간 등)

### Q. Context switch에 대해서 설명하시오

[답변]

Context switch란 한 프로세스에서 다른 프로세스로 CPU제어권을 넘겨주는 것을 말합니다.

이 때 이전의 프로세스의 상태(context)를 PCB에 저장하여 보관하고 새로운 프로세스의 PCB를 읽어서 보관된 상태를 복구하는 작업이 이루어집니다.

### Q. process의 state에는 어떤 것들이 잇나요?

[답변]

프로세스는 실행, 준비, 봉쇄 세가지 상태로 구분됩니다.

-   실행: 프로세스가 CPU를 점유하고 명령을 수행중인 상태
-   준비: CPU만 할당받으면 즉시 명령을 수행할 수 있도록 준비된 상태
-   봉쇄: CPU를 할당받아도 명령을 실행할 수 없는 상태 - ex. I/O 작업을 기다리는 경우 등
