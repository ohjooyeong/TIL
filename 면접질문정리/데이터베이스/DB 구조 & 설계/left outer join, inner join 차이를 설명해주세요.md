# Q. left outer join, inner join 차이를 설명해주세요.

[답변]

Join이란 두 개 이상의 테이블을 서로 연결하여 하나의 결과를 만들어 보여주는 것을 말합니다.

inner join(또는 join)은 두 테이블에 모두 있는 내용만 join되는 방식입니다.

left outer join(또는 left join)은 왼쪽 table의 모든 행에 대해서 join을 진행합니다.

[TIP]

> Join중에 가장 자주 사용되는 inner join과 left outer join을 제대로 이해하고, 사용할 수 있는지 묻는 질문입니다. Join은 실무에서도 자주 사용되기 때문에 면접 질문으로도 가끔 나옵니다. 따라서 둘의 차이점을 간결하게 설명하면 됩니다.

## Inner Join(내부조인)

두 테이블을 연결할 때 가장 많이 사용되는 것이 inner join 입니다. inner join은 줄여서 join으로 부르기도 합니다. 두 테이블을 join 하기 위해서는 두 테이블이 1:N관계로 연결되어야 합니다. 1:N 관계는 주로 primary key와 foreign key관계로 맺어져 있습니다. (상호 조인의 경우에는 PK-FK 관계가 아니여도 됩니다.)

두 table에 공통된 데이터가 존재하는 행에 대해서만 데이터를 검색합니다.

## Left outer join(외부조인)

왼쪽 table의 모든 데이터를 포함한 데이터를 검색합니다.
