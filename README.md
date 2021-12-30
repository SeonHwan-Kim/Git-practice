## Ci&Ai 깃 정리

### Git & Github
Git : 모든 파일의 변화를 기록하고 같은 파일에 대한 각기 다른 버전 보관가능, 같은 파일을 가지고 여러 사람과 함께 일할 수 있다
Github : 클라우드에 있는 깃 제공자

### Git의 동작 원리
* Working Directory : 작업할 파일이 있는 디렉토리
* Staging Area : 커밋을 수행할 파일들이 올라가는 영역
* Git Directory : Git 프로젝트의 메타 데이터와 데이터 정보가 저장되는 디렉토리

Git의 기본적인 동작 과정
1. Working Directory 에서 Staging Area에 올라가기 위해 git add를 사용.
2. 정상적으로 수정되어 올라간 것들은 git commit을 통해 Local Repository(자신의 컴퓨터에 있는 Repository)에 반영이 된다.
3. git push를 해야 Github와 같은 Remote Repository에 저장이 된다.
4. 다른사람이 작업한 데이터를 자신의 컴퓨터에 받기 위ㅐ서는 git fetch 를 이용한다.
5. 충돌이 일어나면 git merge 를 이용한다.
6. 보통은 git fetch와 git merge를 합친 git pull을 사용

### 저장소
**저장소**는 실제 소스코드가 담겨 있으면서 커밋 내역 등의 모든 작업 이력이 담겨 있는 공간
.git 폴더에는 각종 데이터와 해시 값 등이 담겨있다.

### 소스코드 수정하여 Git 저장소에 반영
commit하고 push하여 저장소에 수정 내역을 반영

git add .
git reset ~ 하면 add 된 것 reset
git commit -m "~~" 이런식으로 commit
git push를 하면 저장소에 저장
소스코드를 수정한 경우 다시 위의 과정 반복
git commit -ammend를 하면 vi 켜지고 commit 메세지 수정 

### 커밋 내역 수정하기
만약 예전에 커밋했던 상황으로 돌아가기 위해서는 
git reset --hard 해쉬값 을 이용하면 그 당시 커밋했던 상황으로 돌아감
--hard는 그 이후의 커밋 상태를 아예 지워버림
git push에 -f를 붙여 강제로 push 가능

### Git 브랜치 개요
동시에 여러 개발자들이 프로젝트에서 각기 다른 기능을 개발할 수 있도록 Branch 기능을 제공
서로 다른 브랜치는 작업을 함에 있어서 서로에게 영향을 받지 않는다는 점에서 마음 놓고 서로 다른 개발 작업 수행 가능
기본적으로 Git 저장소를 만들면 자동으로 마스터 브랜치가 생성
별도의 브랜치를 만들기 위해서는 Checkout 명령어 이용
Merge가 수행되기 전까지는 안정적으로 배포가 이루어지고 있다가, 모든 기능이 합쳐진 이후에 다시 배포할 수 있다.

* 통합 브랜치 : 배포가 가능한 수준의 브랜치로 일반적으로 마스터 브랜치를 의미
* 토픽 브랜치 : 특정한 기능을 위해 만들어진 브랜치로 일반적으로 마스터 브랜치 이외의 다른 브랜치를 의미

git branch ~ 를 통해 branch 생성
git checkout ~ 를 통해 ~를 지켜보도록 변경
~에 commit을 해도 마스터 브랜치에는 변화 없음
git checkout master(내 노트북의 경우 main)으로 바꾼 후 git merge ~를 하여 합치기 가능

병합이 끝난 브랜치는 git branch -d ~를 통해 브랜치 제거

### 브랜치 간 충돌 처리
마스터 브랜치와 다른 브랜치의 파일과 커밋 메세지가 다른상태에서 병합을 하면 충돌 발생
다시 파일을 열면 서로 다른 코드를 보여줌, 수동으로 수정 후 저장
다시 git add . 후 커밋하여 merge하면 충돌 문제 해결

### Git 원격 저장소 관리
**원격 저장소** : 네트워크 공간 어딘가에 존재하는 또 다른 컴퓨터를 원격 저장소로 사용할 수 있는 것
원격 저장소로 Github를 주로 사용
git remote 를 통해 원격 저장소에 무엇이 있는지 알 수 있다
git remote show ~를 통해 원격 저장소에 무엇이 있는지 자세히 알 수 있다
git remote -v 를 통해 전체 목록 확인
git remote rename ~을 통해 원격 저장소 이름 변경 가능
git log ~ 로 특정 원격 저장소에 대한 log를 찍어볼 수 있음
git remote rm ~를 통해 특정 원격 저장소를 제거 가능

### Git log 다루기
log를 본다는 것은 다양한 커밋 내역들을 시간 순서대로 확인하겠다는 의미
처리 내역 쉽게 확인 가능
git log stat을 통해 각 커밋에 대한 통계정보 출력
graph는 브랜치와 병합 정보를 그래프로 표시
p를 통해 커밋에 적영된 구체적인 항목 출력
pretty 자신이 지정한 형식으로 출력할 수 있게 해줌(pretty=oneline 등)
git log ==pretty=format:"%h -> %an, %ar : %s" --graph(h는 해쉬값, an은 작성자, ar은 작성 날짜, s는 커밋 주제)

### Git에서 소개글 파일 작성하기
add a readme를 통해 바로 작성 가능
소스코드 블록은 다음과 같이 작성할 수 있다.
```c
#include<stdio.h>

int main(void)
{
  printf("Hello World!");
  return 0;
}
```

링크는 다음과 같이 작성할 수 있다.
[블로그 주소] (https://blog.naver.com/ndb796)

순서 없는 목록은 다음과 같이 작성할 수 있다.

* 깃 튜토리얼
  * 깃 Clone
  * 깃 Pull
  * 깃 Commit
    * 깃 Commit 1)
    * 깃 Commit 2)
인용 구문은 다음과 같이 작성할 수 있다.

>'공부합시다.' -김선환-

테이블은 다음과 같이 작성할 수 있다.
이름|영어|정보|수학
---|---|---|---|
김선환|100점|100점|100점|
홍길동|100점|100점|100점|
이순신|100점|100점|100점|

강조는 다음과 같이 할 수 있다.

**치킨** 먹다가 ~~두드러기~~ 났어요. ㅠㅠ

### Git Archive 명령으로 소스코드 압축하기
git archive --format=zip master -o ../~.zip 으로 압축 가능(상대경로 지정 할 수 있음)

### Git Rebase 명령으로 특정한 커밋 수정/삭제
git rebase -i HEAD~3으로 최근 3개 커밋 내역 보여줌
pick이라 적힌 내용을 reword로 변경 후 :wq!
나오자마자 어떻게 바꿀지 물어봄
바꾸고 저장하면 바뀜
git rebase -i 해쉬값 을 하면 그 값 위쪽으로 확인 가능
pick을 drop으로 변경 시 커밋 제거

### Git config 환경설정에 대해 알아보기
git config --list 로 설정이 어떻게 되어있는지 확인
git config --global user.name "~"
git config --global user.email "~"
sudo vi .gitconfig 를 통애 vi에서 변경 가능
git config --global core.editor vi로 기본 설정을 vi로 설정 가능

### Git commit 날짜 변경 및 커미터 변경
git rebase -i 이전 커밋의 해쉬값 후 pick을 edit으로 변경
GIT_COMMITER_DATE="Oct 1 10:00:00 2018 +0000" git commit --amend --no-edit --date "Oct 1 10:00:00 2018 +0000"
git rebase --continue 를 통해 변경을 바꾸겠다고 하면 변경
git filter-branch -f --env-filter \ 
 'if ( $GIT_COMMIT = 해쉬값)
 then
  export GIT_AUTHOR_DATE="~~"
  export GIT_COMMITER_DATE="~~"
  fi'
git filter-branch -f --env-filter '
OLD_EMAIL="~"
CORRECT_NAME="~"
CORRECT_EMAIL="~"
if($GIT_COMMITTER_EMAIL = $OLD_EMAIL)
then
  export GIT_COMMITTER_NAME="$CORRECT_NAME"
  export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi'


# 안녕
## 안녕
### 안녕
**안녕**
~~안녕~~


>'깃허브 공부하기' -김선환-
* 2022년
* 파이팅
    * 아자아자

이름|영어|정보|수학
---|---|---|---|
김선환|깃|깃허브|CI|

```c
#include<stdio.h>
int main(void)
{
  printf("Hello World");
}
```









