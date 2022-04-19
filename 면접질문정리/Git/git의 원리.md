# Git의 동작원리는 어떻게 되나요?

[답변]

git project는 크게 Working Directory, Staging Area, Local Repository, Remote Repository 4가지 요소로 나눌 수 있습니다. 이와 같은 순서로 Working Directory에서 Staging Area 영역에 add를 통해 올리고, 이 후 commit을 통해 당시의 수정내역들을 기록해 Local Repository(로컬 git 영역)에 올립니다. 그 후 마지막으로 push를 통해 Remote Repository(원격 저장소)에 올립니다.

![ex_screenshot](./img/git.png)

이후, 다른 사람이 올렸던 코드를 받아오는 것은 fetch와 merge로 이루어집니다.
위 그림에서 나타낸 것 처럼 fetch는 원격 저장소에서 Local Repository까지 가져오는 것이고, 이 내용을 merge 해야 실제 내 Working Directory에 내용이 들어가게 된다.
이 두 작업을 한번에 하는 명령어가 있는데, 바로 pull 명령어입니다.

일반적으로 git은 협업할 때 주로 사용하게 됩니다.
같은 프로젝트를 진행하는 사람들마다 Local Repository가 있을 것이고, 다들 수정한 내용을 push하고 할 것입니다. 여기서 만약 A와 B라는 사람이 같은 파일을 수정하여 push를 하게 되면 충돌이 나게 되는 것이다.

그냥 원격 저장소에서 pull을 해오고 하려면 작성했던 수정사항이 다 날라가버릴 것입니다.
이를 위해 있는 것이 Staging 영역이라고 보면 될 것입니다.
작업했던 데이터를 Staging Area에 저장해둔 뒤 충돌난 것을 해결하고 나서 다시 commit 하고 push하면 문제가 되지 않을 것입니다.

[TIP]

> 면접에서 git의 동작원리를 말해보라고 했을 때 크게 당황했었습니다. 그때 당시에는 대답을 제대로 못했지만 한번이라도 읽고 갔으면 쉽게 답했을 질문입니다. 평소 git을 써보신 분이라면 아마 답변하는데 문제 없을 것입니다. 크게 4가지 영역으로 구분되있고 add, commit, push, fetch, merge, pull 등을 알고 면접가기전에 두세번 읽으면 흐름을 금방 파악할 것이라고 생각합니다.
