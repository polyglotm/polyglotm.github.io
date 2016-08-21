---
layout: post
title: "jekyll 기반 github blog를 Travis CI로 통합하기"
tags: jekyll TravisCI
---

### 서론

기존 블로그는 blogger.com이었는데 아주 손쉽게 마이그레이션이 가능 했습니다.
jekyll이 생각보다 강력해서 정말 많은걸 지원해줍니다.
마이그레이션(기존 블로그 글 import)을 지원하는 list는
[이 링크](http://import.jekyllrb.com/docs/home/)를 참조하세요.

jekyll을 사용함으로써category나 tags기능을 사용하여
나름 깔끔하게 정리 하려고 하였습니다만
생각보다 쉽지 않아서 현재까지 작업한것만 배포 하려고 하였으나.

에러메일과 함께 난항에 빠졌습니다.

![CI가 필요해!](/assets/images/2016-08-08-10-32-43.png)

네.
깃허브 블로그 하는데 내친김에 Travis CI까지 바로 하기로 합니다.

[공식document](http://jekyllrb-ko.github.io/docs/continuous-integration/)

이 document대로 해서 한방에 됬더라면 얼마나 좋았을까요!

### step 1. ./script/cibuild 파일 추가

```
#!/usr/bin/env bash
set -e # 에러 발생 시 스크립트 중단

bundle exec jekyll build
bundle exec htmlproofer ./_site
```
공식 번역 문서에는 
**htmlproof** 라고 되어있지만 **htmlproofer** 가 맞습니다!
>번역 문서가 아니라 원본 문서에는 **htmlproofer**로 되어 있습니다!


### step 2. Gemfile에 'html-proofer' gem 추가

```
gem "html-proofer"
```

### step 2. .travis.yml 파일 추가
>username.io repository를 사용하는경우
branches 옵션을 아래와같이 주석처리 하세요!

#### username.io master branch를 사용하는 경우
```
language: ruby
rvm:
- 2.1

before_script:
 - chmod +x ./script/cibuild # 또는 로컬에서 직접 실행 후 커밋

# bundler 를 사용한다고 가정함. 따라서
# `install` 단계에 `bundle install` 이 디폴트로 실행됨.
script: ./script/cibuild

# 브랜치 화이트리스트. GitHub Pages 에서만 사용됨
#branches:
#  only:
#  - gh-pages     # gh-pages 브랜치를 테스트 함
#  - /pages-(.*)/ # "pages-" 로 시작하는 모든 브랜치를 테스트 함

env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # html-proofer 의 설치 속도를 높여줌

```

#### project gh-pages branch를 사용하는 경우
```
language: ruby
rvm:
- 2.1

before_script:
 - chmod +x ./script/cibuild # 또는 로컬에서 직접 실행 후 커밋

# bundler 를 사용한다고 가정함. 따라서
# `install` 단계에 `bundle install` 이 디폴트로 실행됨.
script: ./script/cibuild

# 브랜치 화이트리스트. GitHub Pages 에서만 사용됨
branches:
  only:
  - gh-pages     # gh-pages 브랜치를 테스트 함
  - /pages-(.*)/ # "pages-" 로 시작하는 모든 브랜치를 테스트 함

env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # html-proofer 의 설치 속도를 높여줌

```

네 하지만 아래 보다시피 10번넘는 빌드 실패!

![travisCI-build-failed](/assets/images/2016-08-15-04-13-03.png)

![blogger-migration-to-jekyll](/assets/images/2016-08-15-04-11-08.png)

원인은 바로 blogger에서 migration한 글들이었습니다!.
결국 모든 이미지를 하나씩 긁어와야겠군요...ㅠㅠ
링크도 처리해야 하구요.
