# Git - 100Mb 이상 파일 Push 방법

### 0. 문제 발생

```
Github에는 기본적으로 100MB 이상의 파일을 올릴 수 없다.
```



### 1. 해결방법

##### 1. git-lfs

1. 지정한 파일을 작게 조각내주는 Git extension인 git-lfs — *Git Large File Storage* [*https://git-lfs.github.com/*](https://git-lfs.github.com/) — 를 이용한다.

```bash
$ git lfs install
Update pre-push hook.
Git LFS initialized.
```



2. `git-lfs`의 관리대상 등록

```bash
$ git lfs track “*.exe” // 파일
Tracking *.exe

$ git commit -m “Large file included”
[master (root-commit) dd2b715] Large file included
(...)
```





### %% 에러 발생 %%

```
기존에 100MB 이상의 파일을 Commit한 적이 있다면 여전히 100MB 이상의 파일을 올릴 수 없다는 경고 메시지를 보게 된다.
```

##### 1. BFG Repo-Cleaner

```
기존 Commit에서 100MB보다 큰 파일의 로그를 강제로 없애줘야 한다.
```

 BFG Repo-Cleaner — BFG Repo-Cleaner https://rtyley.github.io/bfg-repo-cleaner/ — 를 이용하자.



```bash
$ java -jar bfg-x.x.x.jar --strip-blobs-bigger-than 100M
```





---------------------------------------

```bash
$ java -jar bfg-x.x.x.jar --strip-blobs-bigger-than 100M
Using repo : C:\***\.git
Scanning packfile for large blobs: 132
Scanning packfile for large blobs completed in 13 ms.
Warning : no large blobs matching criteria found in packfiles — does the repo need to be packed?
Please specify tasks for The BFG :
bfg x.x.x
(...)
```

위와 같은 오류 발생 시

```bash
$ git repack && git gc
Counting objects: 3002, done.
(...)
```

실행



git push 재 실행

----------------------



