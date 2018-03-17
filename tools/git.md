## git

> 2018/03/17 - init


#### 기본

```
git init  -> 현재 폴더를 깃 디렉토리로 만듦
git remote add <remote alias> <url> -> 리모트 레포지토리 등록
git fetch <remote> -> 리모트 상태 동기화
git add <filename>
git commit -m <message>
git push <remote> <branch>
git pull <remote> <branch>

git checkout <branch> -> 브랜치 이동
git checkout -b <branch> -> 브랜치 생성 및 이동
git merge <branch>
```

#### 자주

```
git status -> staged/unstaged 상황
git status -s -> simple 옵션

git branch -> 로컬 브랜치 보기
git branch -a -> 로컬/리모트 브랜치 보기
git branch <branch> -> 브랜치 생성
git branch -d <branch> -> 브랜치 삭제
git branch --delete <remote alias> <branch> -> 리모트 브랜치 삭제

git diff -> unstaged / staged 비교
git diff --staged -> staged / committed 비교
git diff <commit hash-before> <commit hash-after> -> 두 commit 비교
git diff --name-only -> 이름만 표시

git log -> 커밋 로그 표시
git log --oneline -> 한줄씩으로 표시
git log -p -> diff를 같이 표시
git log --graph -> 그래프 형태로 표시

git commit --amend -> 마지막 커밋 수정
git reset <commit hash> -> 해당 커밋으로 되돌리기
git reset --hard <commit hash> -> 해당 커밋으로 되돌리면서 이후의 커밋을 삭제
git rebase -i <commit hash> -> 해당 커밋까지 rebase
```

#### 가끔

```
git show -> 마지막 커밋 조회
git show <commit hash> -> 해당 커밋 조회

git rm <filename> -> 파일 삭제 및 stage
git rm --cached -> git 내에서 파일 삭제, unstage

git config -l -> 현재 설정보기

git revert <commit hash> -> 해당 커밋을 삭제하는 커밋을 커밋

git stash -> 현재 스냅샷 저장(stack)
git stash pop -> 스냅샷 꺼내기
git stash list -> 스냅샷 리스트
git stash drop -> 마지막 스냅샷 삭제
git stash clear -> 스냅샷 모두 삭제

git remote ser-url <remote alias> <url> -> 리모트 url 변경

git reflog -> HEAD 변경 내용 조회
```
