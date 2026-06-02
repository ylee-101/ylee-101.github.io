+++
title = "블로그 검색 노출을 위한 robots.txt와 sitemap.xml 정리"
subtitle = "Hugo와 GitHub Pages에서 검색 엔진이 블로그를 찾을 수 있게 설정한 기록"
description = "Hugo 블로그에서 robots.txt와 sitemap.xml을 설정하고 Google Search Console에 제출하며 확인한 내용을 정리합니다."
date = 2026-04-28T21:00:00+09:00
lastmod = 2026-04-30T14:08:45+09:00
draft = false
author = "ylee-101"
image = "img/post-bg-coffee.jpeg"
tags = ["hugo"]
categories = ["개발"]
+++

## 왜 썼나

블로그를 만들긴 했는데 글이 검색엔진에 잘 발견되는지도 확인해야 했다. 검색 결과에 바로 잘 노출되는 것은 별개의 문제지만, 적어도 검색엔진이 블로그 주소와 글 목록을 찾을 수 있게 `robots.txt`와 `sitemap.xml`을 정리했다.

Hugo와 GitHub Pages를 같이 쓰면 파일을 어디에 둬야 실제 배포 결과에 포함되는지 헷갈릴 수 있어서, 이번에 확인한 내용을 기록으로 남긴다.

## 본문

검색 노출을 위해 먼저 확인할 것은 두 가지다.

- `robots.txt`: 검색엔진 크롤러에게 사이트 접근 정책과 사이트맵 위치를 알려준다.
- `sitemap.xml`: 검색엔진이 참고할 수 있도록 사이트의 주요 URL 목록을 제공한다.

둘 다 있다고 해서 검색 결과 상위에 바로 뜨는 것은 아니지만, 검색엔진이 사이트를 발견하고 색인하는 데 필요한 기본 준비에 가깝다.

## SEO

Search Engine Optimization 검색 엔진 최적화

SEO는 Search Engine Optimization의 약자로 검색 엔진 최적화를 뜻한다. 넓게 보면 글 제목, 설명, URL 구조, 링크, 성능, 모바일 대응까지 모두 포함하지만, 이 글에서는 검색엔진이 블로그를 발견하는 데 필요한 기본 파일 두 개에 집중한다.

개인 블로그에서 우선 확인할 항목은 아래 정도면 충분하다.

- 글마다 구체적인 `title`과 `description`을 둔다.
- 실제 공개할 글만 `draft = false`로 배포한다.
- 검색엔진이 참고할 수 있는 `sitemap.xml`을 제공한다.
- 크롤러가 확인할 수 있도록 `robots.txt`에 사이트맵 주소를 적는다.

## robots.txt

`robots.txt`는 검색 엔진 크롤러에게 사이트의 어떤 경로를 접근해도 되는지 알려주는 파일이다. 검색 노출을 보장하는 파일은 아니고, 크롤러에게 접근 정책을 전달하는 파일에 가깝다.

- User-Agent
- Disallow
- Allow
- Sitemap

Hugo는 빌드 결과물인 `public` 폴더의 파일만 배포한다. 그래서 프로젝트 루트에 `robots.txt`를 만들어도 배포 결과에 포함되지 않는다. 정적 파일로 그대로 복사되게 하려면 `static/robots.txt`에 둬야 한다.

현재는 전체 경로 접근을 허용하고 사이트맵 위치만 알려주도록 단순하게 두었다.

```txt
User-agent: *
Allow: /

Sitemap: https://ylee-101.github.io/sitemap.xml
```

특정 경로를 검색엔진이 방문하지 않게 하고 싶다면 `Disallow` 규칙을 추가하면 된다. 다만 개인 블로그에서는 공개하지 않을 내용은 애초에 배포하지 않는 편이 더 명확하다.

## sitemap.xml

`sitemap.xml`은 검색엔진이 탐색할 때 참고할 수 있는 URL 목록이다. Hugo는 기본적으로 사이트맵을 자동 생성하므로 외부 사이트에서 별도로 만든 XML을 복사해 넣을 필요가 없다.

처음에는 [https://www.xml-sitemaps.com/](https://www.xml-sitemaps.com/) 에 도메인을 넣어서 만들어진 내용을 복사하려고 했다. 그런데 Hugo 빌드 결과를 보니 `public/sitemap.xml`이 자동으로 생성되고 있었다. 그래서 직접 만든 사이트맵 파일은 지우고 Hugo가 생성하는 파일을 사용하기로 했다.

확인은 아래 순서로 했다.

```bash
hugo
```

빌드 후 `public/sitemap.xml`이 생성되는지 확인한다. 배포 후에는 브라우저나 `curl`로 운영 URL을 확인한다.

```bash
curl -I https://ylee-101.github.io/sitemap.xml
curl -I https://ylee-101.github.io/robots.txt
```

둘 다 `200 OK`가 나오면 파일은 정상적으로 배포된 것이다.

Google Search Console에 내 도메인 사이트맵을 등록하는 과정에서는 처음에 아래처럼 가져올 수 없다는 메시지를 봤다.

![](/img/post-4/1.png)

![](/img/post-4/2.png)

현재 기준으로는 운영 URL의 `robots.txt`와 `sitemap.xml`이 모두 정상 응답한다. 그래서 이 메시지가 보인다면 먼저 아래를 확인하면 된다.

- Search Console에 등록한 속성이 실제 블로그 주소와 일치하는지 확인한다.
- 사이트맵 제출 값은 전체 URL이 아니라 `sitemap.xml`만 넣어도 된다.
- GitHub Pages 배포 직후라면 몇 분 정도 기다린 뒤 다시 확인한다.
- `https://ylee-101.github.io/sitemap.xml`이 브라우저에서 직접 열리는지 확인한다.

Search Console에서 사이트맵을 가져오는 것과 실제 글이 검색 결과에 노출되는 것은 별개의 과정이다. 사이트맵 제출이 성공해도 색인에는 시간이 걸릴 수 있고, 검색 결과에 보일지는 글 품질과 검색엔진 판단에 따라 달라진다.

## 정리

- `robots.txt`는 `static/robots.txt`에 둬야 Hugo 빌드 결과에 포함된다.
- Hugo는 `sitemap.xml`을 자동 생성하므로 직접 만든 XML을 루트에 둘 필요가 없다.
- 운영 URL에서 `robots.txt`와 `sitemap.xml`이 `200 OK`로 열리면 배포는 정상이다.
- 검색용 placeholder처럼 색인할 필요 없는 페이지는 사이트맵에서 제외한다.
- 다음에는 Search Console에서 색인 상태를 확인하고, 글 제목과 설명을 계속 다듬어야 한다.

## 참고

[https://fourward.co.kr/blog/what-is-robots-txt-and-sitemap-xml](https://fourward.co.kr/blog/what-is-robots-txt-and-sitemap-xml)
[https://searchadvisor.naver.com/guide/seo-basic-robots](https://searchadvisor.naver.com/guide/seo-basic-robots)
[https://seo.tbwakorea.com/blog/robots-txt-complete-guide](https://seo.tbwakorea.com/blog/robots-txt-complete-guide/)/
[https://seo.tbwakorea.com/blog/how-to-create-and-submit-a-sitemap/](https://seo.tbwakorea.com/blog/how-to-create-and-submit-a-sitemap/)
[https://www.xml-sitemaps.com/](https://www.xml-sitemaps.com/)
[https://www.screamingfrog.co.uk/seo-spider/](https://www.screamingfrog.co.uk/seo-spider/)
