+++
title = "검색에 노출되게 해보자"
subtitle = "robots.txt 와 sitemap.xml 을 설정하여 블로그에 업로드한 글이 검색에 걸리거나/걸리지 않게합니다."
description = "robots.txt 와 sitemap.xml 을 설정하여 블로그에 업로드한 글이 검색에 걸리거나/걸리지 않게합니다."
date = 2026-04-23T13:00:00+09:00
draft = false
author = "ylee-101"
image = "img/post-bg-coffee.jpeg"
tags = ["hugo"]
categories = ["개발"]
+++

## 왜 썼나

블로그를 만들긴 했는데 이걸 누군가 봐야 의미가 있을 것 같고, 그러려면 내가 작성한 글의 핵심 키워드들이 검색에 걸려야할텐데 라는 생각과 함께 SEO, robots.txt, sitemap.xml 을 공부해보고 추가했습니다. 이걸 분명 잊어버릴 것이기 때문에… 기록으로 남겨놓습니다.

## 본문

현재 스킬 테스트를 위해 템플릿만 먼저 업로드 합니다. 수정 기능이 잘 돌아가는지 테스트를 하기위해서 추후 테스트 진행 후 내용이 업데이트 됩니다.

## SEO

Search Engine Optimization 검색 엔진 최적화
내용을 작성합니다.

## robots.txt

hugo 템플릿을 사용하면 빌드결과 public 에 있는 것만 노출되는데, 프로젝트 루트 경로에 robots.txt 를 만들면 이 파일이 빌드가 안돼서 404에러가 난다.
static/robots.txt 경로로 만들어줘야 hugo 빌드할 때 정상적으로 적용한다.

내용을 작성합니다.

## sitemap.xml

[https://www.xml-sitemaps.com/](https://www.xml-sitemaps.com/) 에 도메인을 넣으면 만들어주는걸 복사해서 루트경로에 넣었다.
그런데 hugo 빌드하면서 public/sitemap.xml 을 자동으로 만들더니 이걸 쓴다.
그래서 루트 경로에 넣은 sitemap.xml 은 얌전히 지웠다.

Google Search Console 에 내 도메인 사이트맵을 등록해야한다고 해서 진행해보는데

왜 가져올수없다고 하는지 모르겠다 ;ㅅ;

내용을 작성합니다.

## 정리

- 핵심 결론 1
- 핵심 결론 2
- 다음에 해볼 것

## 참고

[https://fourward.co.kr/blog/what-is-robots-txt-and-sitemap-xml](https://fourward.co.kr/blog/what-is-robots-txt-and-sitemap-xml)
[https://searchadvisor.naver.com/guide/seo-basic-robots](https://searchadvisor.naver.com/guide/seo-basic-robots)
[https://seo.tbwakorea.com/blog/robots-txt-complete-guide](https://seo.tbwakorea.com/blog/robots-txt-complete-guide/)/
[https://seo.tbwakorea.com/blog/how-to-create-and-submit-a-sitemap/](https://seo.tbwakorea.com/blog/how-to-create-and-submit-a-sitemap/)
[https://www.xml-sitemaps.com/](https://www.xml-sitemaps.com/)
[https://www.screamingfrog.co.uk/seo-spider/](https://www.screamingfrog.co.uk/seo-spider/)
관련 링크나 참고한 문서를 적습니다.
