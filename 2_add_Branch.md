# Git branch 추가

### Git flow 사용해서 작업

=> <http://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html>

* master branch는 선임 개발자가 담당해서 모든 branch를 합치는 용도로
* feature branch를 이용하여 각자 개발
* hotfixes branch는 바로 master로 반영하기 위한 branch



=> <https://about.gitlab.com/2014/09/29/gitlab-flow/>

* git-lab branch flow는 비교적 간단하게 master branch에 기능들을 붙여가는 느낌으로 사용

--------------------------------------------------------------------------

* branch 생성

  ```bash
  git branch [branch name]
  ```

* branch 이동

  ```bash
  git checkout [branch name]
  ```

* branch 삭제

  ```bash
  git checkout -d [branch name]
  ```

* branch 생성하면서 이동 - (git branch 브랜치명 + bit checkout 브랜치명)

  ```bash
  git checkout -b [branch name]
  ```

  => Switch to a new branch 'ho'

* branch 사이의 code 비교

  ```bash
  git diff [현재 branch와 비교할 branch 이름]
  ```

* branch 합치기

  ```bash
  git merge [현재 branch와 합칠 branch 이름]
  ```

  * Fast-foward : 현재 branch의 변경사항이 없기때문에 현재 branch의 다음 단계가 합칠 branch가 되어 합쳐지는 상황
  * merge commit : 현재 branch의 변경사항이 있지만 합칠 branch와 충돌되는 파일이 없기때문에 다음 단계에 합쳐져 merge commit되며 branch가 합쳐짐
    * 커밋 메세지를 지정하라는 vim 창이 뜸,
    * commit log에 merge commit으로 기록이 남게 됨.
  * merge conflict : merge commit으로 합치려고 했지만, 충돌되는 파일이 있으므로 사용자가 해결하고 commit  하라는 에러 메세지가 뜸.
    * vs code로 그 파일을 열면 충돌되는 파일의 내용을 선택할수 있게 지원
    * 수정사항을 선택후 commit까지 해주면 merge conflict 해결.
  * pull request : git hub의 pull request를 이용하여 pull request로 모두 합칠수 있다.