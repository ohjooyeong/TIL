# Primary key가 무엇인지 설명해주세요.

[답변]

candidate key 중 선택한 main key로써, 각 row를 구분하는 유일한 열(column)을 말합니다. 그래서 기본키는 Null값을 가질 수 없고, 중복된 값을 가질 수 없습니다. 기본키는 table당 1개만 지정해야 합니다.

[TIP]

> key와 관련된 기본적인 용어를 묻는 면접관들도 꽤 있습니다. 데이터베이스에서 가장 기초적인 용어들이기 때문에 대답을 하지 못하면 말이 안됩니다. 확실하게 이해하고 넘어가면 틀릴 일이 없으므로 이번 시간에 확실히 짚고 넘어 가보겠습니다.<br>
> 특히 꼬꼬무에서 처럼 후보키는 뭔지, 대체키는 뭔지, 복합키는 뭔지 묻는 경우도 많으므로 간략히 한 줄로 설명하실 수 있으면 됩니다.

### Relation

table 중 데이터베이스에서 사용되기 위한 조건을 갖춘 것이 relation입니다.

Relation의 제약 조건 중 가장 자주 등장하는 조건은 다음과 같습니다.

1. table의 cell은 단일 값을 갖는다.
2. 어떤 두개의 row도 동일하지 않다.

하지만 통상적으로 relation과 table이란 용어를 구분하지 않고 사용하기도 합니다.

## Primary key

**_Super Key(슈퍼키)_**는 각 row를 유일하게 식별할 수 있는 하나 또는 그 이상의 속성들의 집합입니다. 슈퍼키는 유일성만 만족하면 슈퍼키가 될 수 있습니다.

- 유일성 : 하나의 key값으로 특정 row만을 유일하게 찾아낼 수 있어야 합니다.
- 예시
  - (학번)
  - (학번, 이름)
  - (학번, 이름, 학과)
  - (주민등록번호)
  - (주민등록번호, 학과, 성별)
  - 등등

**Candiate key(후보키)**는 Super key 중에서 더이상 쪼개질 수 없는 Superkey를 Candidate Key라고 합니다. 즉 각 row를 유일하게 식별할 수 있는 최소한의 속성들의 집합입니다.

- 최소성 : 모든 row를 유일하게 식별하는 데 꼭 필요한 속성만으로 구성되어야 합니다.
- 예시
  - (학번)
  - (주민등록번호)

**Primary key(기본키)**는 candidate key 중 선택한 main key로써, 각 row를 구분하는 유일한 열을 말합니다. 그래서 기본키는 Null 값을 가질 수 없고, 중복된 값을 가질 수 없습니다. 기본키는 table당 1개만 지정해야합니다.

**Alternative key(대체키)**는 후보키가 두 개 이상일 경우, 기본키로 지정이 되지 못하고 남은 후보키들을 말합니다.

### Q. Primary key와 Foreign key에 대해 설명해주세요.

[답변]

Primary key는 candidate key 중 선택한 main key로써 Null값을 가질 수 없고, 중복된 값을 가질 수 없습니다. Candidate key중 선택했으므로 유일성과 최소성을 만족합니다.

Foreign key는 다른 table의 Primary key column과 연결되는 (참조되는) table의 column을 의미합니다.

### Q. Candidate key에 대해 설명하시오

[답변]

Cnadidate key는 table을 구성하는 column들 중에서 row를 유일하게 식별하기 위해 사용하는 column들, 즉 primary key로 사용할 수 있는 column들을 말합니다.

### Q. alternate key에 대해 설명하시오.

[답변]

primary key를 제외한 나머지 candidate key들을 말합니다. 대체키/보조키라고도 부릅니다.

### Q. composite key에 대해 설명하시오.

[답변]

Composite key란 table에서 각 row를 식별할 수 있는 두 개 이상의 column으로 구성된 candidate key를 말합니다.
