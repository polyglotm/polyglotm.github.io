---
layout: post
title: "yadr에 vim plugin 추가하기"
tags: yadr zsh vim-plugin
---

jekyll을 선택한만큼 markdown으로 쓰려고 하는데
preview가 있었으면 좋겠다는 생각이 들었습니다.

vim자체에서 plugin을 검색하고 설치 할 수 있지만
yadr(zsh)을 사용할경우 충돌이 나거나 인식이 안되는 경우가 있더라구요.

이 삽질을 했던걸 기억한다는게 참 다행이지만
yadr에 플러그인 설치하는 방법이 바로 딱 기억나진 않더군요.

다음번에 마주칠 이 상황을 위해 글을 남기기로 합니다.
앞으로는 30초 안에 기억 안나는건 다 블로그에 남겨놔야겠어요.


### Add a plugin

```
yav -u https://github.com/airblade/vim-rooter
```

### Delete a plugin

```
ydv -u airblade/vim-rooter
```

[original-document](https://github.com/skwp/dotfiles/blob/master/doc/vim/manage_plugins.md)
