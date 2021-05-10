# Git

`Git`은 분산형버전관리시스템(DVCS-Distributed Version Control System)이다.

소스코드의 버전 관리를 확인 할 수 있고, 이력이 관리된다.

## 기초 명령어 정리

### 1. git 저장소 설정

```
$ git init
```

```
student@DESKTOP MINGW64~/Desktop/TIL (master)
$
```

**주의!! 반드시 현재 디렉토리에 git을 사용하고 있는지, (master) 있는지 확인 할 것**

### 2. git add

`git add`는 현재 `working tree`에서 `commit`할 목록에 담아 놓는 것이다. 그리고 그 목록은 `staging area`라고 한다.

```
$ touch a.txt
$ git add .
```

* `git add a.txt`를 해도 되지만, 우선 `git add .` 을 하자!!
* `.` 은 리눅스 상에서 현재 디렉토리를 뜻한다.

### 3. git commit

`git commit`은 현재 소스코드 상태를 스냅샷을 찍는 것과 동일하다.

`staging area`에 담겨 있는 내용을 이력으로 기록한다.

```
$ git status
$ git commit -m "커밋메세지"
```



### git status

git의 현재상태를 확인한다. 자주자주 입력해보자!

```
$ git status
```

---

## 원격 저장소로 보내기(push)

사전에 git hub에 저장소(repository)를 만들어 놓는다.

1. git hub 저장소(원격저장소) `url`를 `origin` 이라는 이름으로 저장한다.

```
$ git remote add origin https://github.com/leeiopd/Til.git
```

2. 원격 저장소로 보낸다.(push)

```
$ git push -u origin master
```



git status - 현 상태 확인

git add . - commit 할 파일 담기

git commit -m "~~" - 메세지 ~~로 commit 작성

git push -u orign master - push는 파일 git hub에 올리기



## 원격저장소에서 가져오기 (pull)

github 원격 저장소에서 변경된 커밋 내용(파일)을 가졍괴 위해서는 `pull`명령어를 사용한다.

```
$ git pull origin matser
```



## 원격저장소 복제하기(clone)

원격 저장소를 복제하기 위해서는 `clone`명령어를 사용한다.

``` $ git clone https://~~~~ <- url
$ git clone https://~~~~ (<- url)
```



