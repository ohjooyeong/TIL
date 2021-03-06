# DeadLock이 뭔지 설명해주세요.

[답변]

데이터베이스 deadlock(교착 상태)이란, 여러 transaction들이 각각 자신의 데이터에 대하여 Lock을 획득한 상태에서 상대방 데이터에 대하여 접근하고자 대기를 할 때 교차 대기를 하게 되면서 서로 영원히 기다리는 상태

[TIP]

> 면접에서 종종 나오는 질문으로, deadlock은 어떤 상황에 발생하는지 그리고 해결 방법은 어떻게 되는지에 초점을 맞춰서 답변

## Deadlock

두 transaction이 각각 lock을 설정하고, unlock을 하지 않은 상태에서 서로의 lock이 걸린 데이터에 접근하려고 할때, 서로 대기를 계속하여 영원히 처리되지 않는 상황이 발생합니다.

deadlock을 해결하는 방법은 다음과 같습니다.

1. 예방기법: 각 transaction이 실행되기 전에 필요한 데이터를 모두 Locking 해주는 것입니다. 하지만 locking 해줘야 하는 데이터가 많다면 사실상 모든 데이터를 전부 locking한 것과 동일하여 transaction의 병행성을 보장하지 못할 수 있습니다.
2. 회피기법: 자원을 할당할 때 time stamp를 사용하여 deadlock가 일어나지 않도록 회피하는 방법입니다.
3. 탐지/회복 기법: Transaction이 실행되기 전에는 아무런 검사를 하지 않고, deadlock이 발생하면 이를 감지하고 회복시키는 방법입니다.

### Q. deadlock을 해결하려면 어떻게 해야하나요?

[답변]

각 transaction이 실행되기 전에 사용될 모든 데이터를 미리 locking을 해주는 예방기법이 있고, 자원할당 시 time stamp를 사용하여 deadlock이 발생하지 않도록 회피하는 기법이 있습니다. 또한 deadlock이 발생하면 이를 감지하고 회복시키는 탐지/회복 기법이 있습니다.
