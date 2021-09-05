---
last_modified_at : 2021-09-05
layout : single
title:  "Github 많이 쓰는 명령어"
categories: github
tags : [명령어]

toc: true
toc_sticky: true
---
## 서론
제가 빠르게 보기 위해서 적습니다.

## git add 취소
file 이름을 적지 않으면 add한 파일 전체를 취소합니다.
```powershell
git add .
git reset HEAD [file]
```

## git commit 취소
가장 많이 쓰는 것 같습니다. 저 같은 경우 대용량 파일을 add한채로 커밋하면 커밋은 올라가는데 update가 안되는 경우가 생겼을 때 사용했습니다.
```powershell
git log
git reset (--mixed) HEAD^ // 가장 기본, add파일은 unstaged
git reset --soft HEAD^    // add파일은 staged
git reset HEAD~2          // 마지막 2개의 commit 취소
git reset --hard HEAD^    // add파일을 unstaged, 워킹디렉토리에서도 삭제
```

## git branch
일반적으로 코드를 수정할 때, 새로운 버전을 만들 때 브랜치를 만들어서 사용합니다.
```powershell
git log
git checkout [commit번호]
git branch new

git checkout new
git add .
git commit
git push origin new

git checkout master
git merge new
git add .
git commit
git push origin master     

git branch -d new          // 로컬에서 브랜치 삭제
git push origin new        // 로컬에서 삭제 => push => 원격삭제
git push origin -d new     // 그냥 원격에서 바로 삭제
```