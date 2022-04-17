# Q. segmentation에 대해서 설명해주세요.

[답변]

segmentation이란 process가 할당받은 메모리 공간을 논리적 의미 단위(segment)로 나누어, 연속되지 않는 물리 메모리 공간에 할당될 수 있도록 하는 메모리 관리 기법입니다.

[TIP]

> page와 같이 면접에 자주 나오진 않지만, 메모리에 대해서 이해하는데 중요한 내용이 많이 담겨져 있기 때문에 알아두시면 좋습니다<br/>
> 일정한 크기의 단위로 나누어 할당을 했던 page와 다르게, segmentation은 의미 다윈로 물리 메모리에 할당을 하는 기법임을 설명할 수 있어야 합니다. 특히 code, data, heap, stack등의 기능(의미)단위로 나눈다는 점을 기억하시길 바랍니다.

## Segmentation

segmentation 기법은 process가 할당받은 메모리 공간을 논리적 의미 단위(segment)로 나누어, 연속되지 않는 물리 메모리 공간에 할당될 수 있도록 하는 메모리 관리 기법입니다.

일반적으로 process의 메모리 영역 중 Code, Data, Heap, Stack 등의 기능 단위로 segment를 정의하는 경우가 많습니다.

segmentation 기법에서는 주소 바인딩(address binding)을 위해 모든 프로세스가 각각의 주소 변환을 위한 segment table을 갖습니다.

### Q. segmentation의 메모리 단편화 문제에 대해 설명해주세요.

[답변]

segmentation 기법에서 segment의 크기만큼 메모리를 할당하므로 내부 단편화 문제가 발생하지 않습니다. 하지만 서로 다른 크기의 segment들이 메모리에 적재되고 제거되는 일이 반복되면, 외부 단편화 문제가 발생할 가능성이 있습니다.

### Q. paging과 segmentation의 차이는 뭔가요?

paging은 일정한 크기의 단위로 나누어 할당을 하는데, 이에 반해 segmentation은 code, data, heap, stack등의 기능(의미)단위로 물리 메모리에 할당하는 기법입니다.

paging의 경우 내부 단편화 문제가 발생할 수 있는데, 이에 반해 segmentation은 외부 단편화 문제가 발생할 수 있습니다.

### Q. paged segmentation 기법에 대해 설명하시오

[답변]

paged segmentation이란 segmentation을 기본으로 하되 이를 다시 동일 크기의 page로 나누어 물리 메모리에 할당하는 메모리 관리 기법입니다. 즉, 프로그램을 의미 단위로 segment로 나누고 개별 segment의 크기를 page의 배수가 되도록 하는 방법입니다.

이를 통해 segmentation 기법에서 발생하는 외부 단편화 문제를 해결하고, 동시에 segment단위로 process간의 공유나 process 내의 접근 권한 보호가 이루어지도록 해서 paging 기법의 단점을 해결합니다.
