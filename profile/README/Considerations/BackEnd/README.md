# BE 고민내용

Q. 사용자마다 가지는 카테고리 계층 구조를 어떻게 표기할 것인가?

A. 하나의 `branch`는 소유하고 있는 `branch`들을 데이터 베이스에 저장한다.
	모든 사용자는 스스로가 하나의 `branch`와 같으므로 하위 `branch`를 조회하면서 계층을 이룬다.

Q. 위 방식대로 진행할 경우 `branch`들의 정렬을 어떻게 할 것인가?

A. 하위 `branch`의 시작일을 조회하여 정렬하는 방식은 `branch` 수가 늘어나고 사용자가 많아지면
	상당한 연산을 요구할 것으로 보인다. 그러므로 아래와 같은 방식으로 구현하는 것을 시도하였다.

​	하위 `branch`를 저장할 때 `{'branch': 시작일}` 형태로 저장한다.
​	이를 바탕으로 각 `branch`와 `leaf`들을 정렬한다.
​	사용자가 해당 `branch`를 호출했을 때, 시작일이 실제 `branch`의 시작일과 다르면 갱신한다. 

​	이 같은 방식을 사용하면 연산량을 극히 줄일 수 있다는 장점이 있으나, `branch`들의 시작일이
​	수정된 경우 반영하기 어렵다는 문제가 발생한다. 그러나 `branch`의 시작일을 수정할 일이
​	많지 않을 것으로 판단되는 점, 자주 방문하는 `branch`는 계속해서 갱신이 된다는 점 등
​	위 방식을 사용해도 무방할 것 같은 이유가 존재하므로 이 같이 진행하기로 하였다.

Q.공유받은 프로젝트에 글을 썼는데, 공유가 중단되었다면 이 글은 어디에 표기해야 하는가? 

A. 고민
	1. 글은 사람에게 귀속된다? | 프로젝트에 귀속된다?
	1. 프로젝트는 반드시 만든 사람이 주인인가?(당연히 권한을 양도할 수 있어야.)
	1. 회사 보안 등의 이유라면, 더 이상 프로젝트에 권한이 없다면 

Q. 계정을 일시정지 혹은 탈퇴할 경우 글을 처리하는 방법

A. 일시정지 및 탈퇴 시에 사용자에게 확인을 받는 것을 원칙으로 한다.
	기본적으로 자동으로 비공개되거나 삭제되지 않으며 직접 처리해야 한다.
	물론 이를 위한 다중 선택 등의 편의성은 제공한다.

​	다만, 프로젝트 관리자가 아무도 없는 글은 방문자가 특정 기간 이상 없을 시 삭제된다.



잎은 시작일, 종료일, 작성일이 포함되고 시작일과 종료일에 각각 간이 표시된다. 글을 누르면 해당 글이 확장되어 표시된다.

4. 권한 체계를 제공하는 방법에 대해 고민해야한다. 사용자마다, 기능마다 권한을 부여할 수 있으려면 다양한 고려 사항이 필요하다.
5. 사용자가 많은 채팅방에 대해 채팅 내용을 캐싱할 수 있어야 한다.
6. 일반 스크롤을 통해 하나의 글 단위, 스크롤 바를 이용해 비율 단위로 이동할 수 있도록 만든다.
7. 보고 있는 부분과 볼 것으로 예상되는 부분에 대한 로딩을 구현한다.
