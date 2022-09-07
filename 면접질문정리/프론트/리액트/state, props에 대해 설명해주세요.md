# State, Props에 대해

한마디로 정의하자면 리액트 컴포넌트 사이에 데이터 교환을 하기 위한 방법이며 그에 따라 쓰여지는 요소

리액트에서 컴포넌트 간 데이터 교환을 도와주는 요소는 state와 props 두가지가 있습니다.

1. State: 컴포넌트 내에서만 사용가능한 Private Data
2. Props: 다른 컴포넌트로 넘길 수 있는 Public Data

## Props in React

Props는 외부 컴포넌트에서 파라미터로 전달되는 public data입니다. props를 받은 컴포넌트는 props 자체를 수정할 권한은 없습니다. 리액트에서 props는 Javascript에서의 매개변수나 HTML에서의 속성과 유사한 성질을 가지고 있습니다.
props를 받은 컴포넌트는 props를 사용해서 동적인 렌더링을 할 수 있습니다.

## State in React

리액트 컴포넌트들은 build-in state 객체를 가지고 있습니다. state는 private data이기 때문에 다른 컴포넌트에서 접근 자체가 불가능합니다. 하지만 매개변수 형식으로 다른 컴포넌트에 변수로 넘겨서 사용하는 것이 가능합니다.

state가 변경될 때마다 컴포넌트는 render() function을 실행시키고 HTML에 반영하게 됩니다.
