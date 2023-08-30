---
title: "[Git] Git Command"
excerpt: "Git Command"

categories:
- Git
tags:
- [Git]

toc: true
toc_sticky: true

date: 2023-06-22
last_modified_at: 2023-08-30
---
# Git Command

## 설정 초기화

``` bash
git config --global user.name "Your name"
git config --global user.email "eamil@email.com"
```



### 커밋하지 않고 변경사항 저장

```bash
git stash
git stash pop
```



## Git 저장소에 포함되지 않은 파일 삭제

``` bash
git clean
```



## 수정한 파일 되돌리기

```
git checkout -- filename
```



## 모두 되돌리기

```
git restore .
```

