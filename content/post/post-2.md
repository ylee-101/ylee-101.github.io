+++
title = "깃허브를 통해 블로그를 만들자"
subtitle = "github 으로 배포되는 블로그를 만들어보자."
description = "github 으로 배포되는 블로그를 만들어보자."
date = 2026-04-23
lastmod = 2026-04-28T20:34:20+09:00
draft = false
author = "ylee-101"
image = "img/post-bg-coffee.jpeg"
tags = ["hugo"]
categories = ["개발"]
+++

## 왜 썼나

깃허브의 pages 기능을 통해 블로그를 배포하고싶은데, github 와 hugo 를 연결하는 것이 생각보다 쉽지 않았다. 최종적으로는 AI의 도움을 받아 배포 완료하였는데, 다시 과정을 되짚어보고 방법을 제대로 기억하고자 기록으로 남긴다.

## 본문

## github pages 로 배포하기
새 레포지토리 만드는 방법은 생략한다.
레포지토리를 만든 후 index.html 을 넣어둔다.
Setting → Pages → Build and deployment 에서 일단 브랜치통해 배포하도록 하고 main 에 커밋이 푸쉬되면 배포 시작하도록 셋팅한다.
main 에 index.html 을 올리면 해당 내용을 username.github.io/reponame/ 에서 확인할 수 있다.
문제는 이걸 블로그스럽게 보여야한다는 것이다.
여러 툴이 있지만 나는 hugo 를 사용하기로 했다.
## hugo 연결하여 블로그 포맷 보이기
터미널에서 brew install hugo 를 먼저 해줘야한다.
원하는 곳에서 hugo new site ${sitename} 으로 hugo 사이트를 생성한다.
그럼 ${sitename} 으로 폴더가 생기는데, 그 안으로 이동하고
```javascript
git init
git remote add origin ${위에서 배포한 github_repo_url}
git fetch --all
git pull origin main
```
이러면 새로 만든 hugo 프로젝트 폴더와 github 연결 시작이다.
제대로 연결되려면 hugo.toml 에서 설정을 맞춰줘야한다.
```javascript
baseURL = 'https://example.org/'
locale = 'en-us'
title = 'My New Hugo Project'
```
초반에는 이런 상태일텐데, baseURL 을 pages 를 통해 생성된 url 링크로 변경한다.
title 도 원하는 내용으로 변경하면 된다. 나는 locale 도 kr 로 변경했다.
아직은 사이트가 제대로 보이지 않을텐데, post 도 올리고 theme 을 설정해줘야한다.
theme 은 [https://themes.gohugo.io/](https://themes.gohugo.io/) 에서 취향에 따라 고르면 된다.
나는  [**hugo-theme-cleanwhite**](https://github.com/zhaohuabing/hugo-theme-cleanwhite)** **로 골랐다.
```javascript
git submodule add https://github.com/zhaohuabing/hugo-theme-cleanwhite.git themes/hugo-theme-cleanwhite
```
hugo.toml 에도 theme 설정을 맞춰줘야한다.
```javascript
...
theme = 'hugo-theme-cleanwhite'
```
이제 제대로 보이는지 확인을 해보자. 일단 배포 전에 로컬에서 확인!
```javascript
hugo server -t  hugo-theme-cleanwhite
```
위 코드를 실행하면 알려주는 url (localhost:port/url/)에서 적용된 것을 볼 수 있다.
`hugo server` 를 하면 public 폴더에 배포를 위한 파일들이 생성되는데, 이게 배포될 수 있도록 github 설정을 맞춰줘야한다.
Setting → Pages → Build and deployment 에서 workflow 를 검색해서 추가할 수 있는데 hugo 를 configure 한다. 이제 hugo workflow 를 통해서 배포하므로 브랜치통해 배포로 셋팅했던 부분을 액션 이용하는 것으로 변경한다.
나는 이 과정에서 빌드 에러가 좀 발생했는데, github 에서 자동으로 넣어준 workflow 의 hugo version 이 너무 낮은 문제였다. 실제로 터미널에서 사용하고있는 hugo version 을 찾아 수정해주니 해결되었다.

우여곡절 끝에 성공한것이라 글로 남길 때 놓친부분이 있을지도 모르겠다. 추후 발견되면 수정하는걸루…

## 정리

- github pages 통해 배포. hugo workflow 추가하기.
- hugo 설치하고 셋팅해보기
- 다음에 해볼 것 : 글쓰기

## 참고

관련 링크나 참고한 문서를 적습니다.
