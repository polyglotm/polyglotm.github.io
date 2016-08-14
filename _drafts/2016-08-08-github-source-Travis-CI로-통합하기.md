---
layout: post
title: "jekyll 기반 github blog를 Travis CI로 통합하기"
tags: jekyll TravisCI
---

###서론

기존 블로그는 blogger.com이었는데 아주 손쉽게 마이그레이션이 가능 했습니다.
jekyll이 생각보다 강력해서 정말 많은걸 지원해줍니다.
마이그레이션(기존 블로그 글 import)을 지원하는 list는
[이 링크](http://import.jekyllrb.com/docs/home/)를 참조하세요.

jekyll을 사용함으로써category나 tags기능을 사용하여
나름 깔끔하게 정리 하려고 하였습니다만
생각보다 쉽지 않아서 현재까지 작업한것만 배포 하려고 하였으나.

에러메일과 함께 난항에 빠졌습니다.

![CI가 필요해!]({{ site.url }}/assets/images/2016-08-08-10-32-43.png)

네.
깃허브 블로그 하는데 내친김에 Travis CI까지 바로 하기로 합니다.


