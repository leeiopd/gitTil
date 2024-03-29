# Git - Issue 기반 버전 관리 워크플로우!

> *“버전 관리 시스템을 제대로 사용한다는 것은 특정한 방식으로 사고한다는 것을 의미한다… (중략) …생각을 구조화하고, 기억하고, 공유하는 것. 이 점을 이해하지 못하면 Git 사용은 기껏해야 ‘마법 주문’을 암기해 사용하는 것에 불과하다.”*
>
> *—마크 애트우드(HP 오픈소스 규약 이사), 추천사 중*



* **핵심은 "git"이 아니라 "프로젝트 관리 철학"**
* 1인 팀 작업에도 `미래의 나` 를 멤버로 가정하고 작업을 하도록 하자.
*  ‘미래의 나’가 금방 기억을 되살릴 수 있도록 일관된 원칙에 따라 작업을 저장하는 것, 주석과 문서화를 게을리하지 않는 게 정말 중요하다.
*  *[좋은 commit 메시지 작성법](https://item4.github.io/2016-11-01/How-to-Write-a-Git-Commit-Message/)*



### 1. Git 의 isuue 트레커

>  **‘이슈’란? 프로젝트 안에서 벌어질 수 있는 가장 작은 단위의 ‘사건’**

* 오픈 소스 프로젝트에는 수많은 기여자들이 프로그램의 버그나 개선점을 제보하러 찾아오고, 프로젝트의 관리자에게 질문하거나 요청하고 싶을 때 기여자는 ‘이슈’를 ‘오픈’한다.
* 이슈를 연 기여자는 질문이나 요청을 남기고, 관리자는 나름의 답변을 해주거나 다음 릴리즈 때 해결하겠다는 약속을 한다. 이후 문제가 해결되면 관리자는 이슈를 닫는다.
* 커밋 메시지에 이슈 번호를 적어서 저장소에 올리면 github은 그 커밋을 이슈 페이지에 추가해 준다.
  * 이 기능 덕분에 이슈 페이지에는 버그가 제보되고 해결된 코드의 커밋이 올라온 뒤, 관리자가 코드를 승인하고 이슈를 닫는 과정이 타임라인 형식으로 완벽하게 기록된다.

```
이슈를 만들고 해결하는 과정을 반복 하기만 해도 github은 여러분의 프로젝트가 발전되는 과정을 알아서 정리해준다는 뜻
```



### 2. issue를 활용한 워크 플로우 개요

1. 새로운 이슈를 열고 번호를 확인한다.

2. 로컬 저장소에 새로운 브랜치를 생성한다. 형식은 “이슈 번호-설명”.
3. 이슈에 적어둔 목표를 해결한다. **(오직 이슈에 적힌 내용만 작업한다)**
4. 작업을 테스트하여 제대로 완료됐는지 확인한다.
5. 수정 사항을 커밋하고 푸시한다. **(github이 커밋을 추적할 수 있도록 커밋 메시지 안에 이슈 번호를 적어야 한다)**
6. 작업이 잘 완료됐다면 작업 브랜치를 메인 브랜치에 병합(`merge`)한다.
7. 이슈에 모든 내용이 잘 기록됐는지 확인하고 이슈를 닫는다.



### 3. 자세히 들여다 보자!

-------------------------------------------------------------

##### 1. 새로운 이슈 생성

1. Issue 메뉴에서 New issue 클릭

![NewIssie](./gitIssueImg/1.JPG)

2. 이슈 제목, 내용 작성

   ![Issue 작성](./gitIssueImg/2.JPG)

   

3. 옵션 추가

   * **Assignees:** 이슈를 함께할 멤버 `호출`.
   * **Labels:** 이슈를 분류해주는 `태그` ( 기본으로 제공해 주는 태그 외 추가로 커스텀이 가능 )
   * **Milestone:** 프로젝트가 도달해야 하는 `목표` 지정. 각 기능별 마일스톤을 지정하고 목표로 할 수 있다.
   * **Due date:** 마감 `날짜` 지정. 이슈를 완료할 날짜를 지정합니다. 일정 관리 기능.
   * **Projects:** github이 직접 만들어주는 `칸반 보드`입니다. 이슈에 프로젝트를 지정해주면 이슈가 칸반 보드 안에 카드로 작성 됨. (Git Lab에서는 `Doing`, `To do` 라벨로 자동으로 추가 된다.)

4. 작성 완료

   ![created Issue](./gitIssueImg/3.JPG)

   * 작성 완료된 이슈
   * 붉은 동그라미 안의 `#2` 는 이슈 `Number`로 `commit`시 사용 가능하다.



##### 2. Branch 생성

1. Isuue Branch 생성

   ![NewIsuueBranch](./gitIssueImg/4.JPG)

   * `checkout` : 브랜치 이동 명령어
   * `-b`: 브랜치 생성 옵션. `checkout -b` 로 새로운 브랜치를 생성하고 이동할 수 있다.
   * `2-test` : 브랜치 이름. `이슈 번호 - 이슈 내용`의 형식으로 브랜치 이름 생성



2. 로컬 브랜치와 원격 저장소 연결

   ![localConnectToRepo](./gitIssueImg/5.JPG)

   * `--set-upstream`: 로컬 브랜치와 원격 브랜치를 연결하는 옵션. 간단히 말해 적용한 브랜치( `2-test`) 브랜치로의 push와 pull 명령어를

     * ```bash
       git push (remote 이름/ branch 이름 생략 가능)
       ```

     * ```bash
       git pull (remote 이름/ branch 이름 생략 가능)
       ```

     위와 같이 간단히 설정 할 수 있다. ( default 값은 `origin master`)
     
   * branch 설정 후 `push`는 로컬의 branch를 업로드 한다



3. 결과 - Issue 와 branch 의 연결

   ![BranchConnectToIssue](./gitIssueImg/13.JPG)

   * 위와 같이 `Issue`에 자동으로 `branch`가 `연결`된 것을 확인 할 수 있다.



##### 3~4. 목표 달성 및 테스트

* test 이기 때문에 `test.txt` 파일의 생성을 이슈 해결으로 하겠다.

  ![isuueComplete](./gitIssueImg/6.JPG)



##### 5. 수정사항 Commit & Push

1. `git commit` 명령어

2. commit 작성

   ![wirteCommit](./gitIssueImg/8.JPG)

* `[#2] test 완료` : commit 제목, `[#2]` 를 시작으로 하여 이슈 표기

* `- test.text 파일 추가` : 본문, 팀원이 알기 쉽도록 작성

* `Resolves #2`: 이슈 닫기 명령어 + #이슈 num 
* close
  * closes
  * closed
  * fix
  * fixes
  * fixed
  * resolve
  * resolves
  * resolved

>  **위의 명령어와 함께 `#이슈 num`을 사용하면 pull request 요청 시 isuue를 닫을 수 있게 자동으로 요청 한다**



3. 확인하기

   ![checkCommitIssue](./gitIssueImg/10.JPG)

   ![checkCommitIssue](./gitIssueImg/11.JPG)

   * `push` 후 `commit` 내용을 통해 위에서 작성 하였던 `Issue #2`와 연동 되어 있는 것을 확인 할 수 있다.



 ##### 6. Full requet & Merge

1. Full request 요청하기

   * Repository 메뉴에서 merge 요청
   
   ![createRequest](./gitIssueImg/9.JPG)



2. merge 결과

   * `Closes #2` commit 의 `merge` 결과

   ![resultClosesCommit](./gitIssueImg/14.JPG)

   * merge 된 이후 자동으로 이슈가 닫혔다.
   * gitlab에서 수동으로도 issue를 종료 시킬 수 있다.
   * `gitlab` 의 issue 관련 commit 명령어에 대한 정보가 부족하니 오류가 발생시 되도록 일반 commit 후 pull request 요청을 사용하도록 하자.



