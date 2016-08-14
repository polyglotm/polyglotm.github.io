---
layout: post
title: "vim markdown preview plugin"
tags: vim-plugin markdown-preview
---

vim기반 markdown preivew를 알아보니 실시간으로 갱신되는 플러그인이 있더군요.
물론 chrome브라우저 기반으로 갱신이 됩니다.

설치할 plugin은 vim-instant-markdown이고 
github repository는
[이 링크](https://github.com/suan/vim-instant-markdown)를 참조하세요.

### step 1 download

```
npm -g install instant-markdown-d
```

### step 2 copy plugin
Copy the after/ftplugin/markdown/instant-markdown.vim file from this repo into your ~/.vim/after/ftplugin/markdown/


### step 3 configuration
기본 옵션은 autostart이기 때문에 markdown파일을 열때마다 크롬에 새창이 뜨게 됩니다.

.vimrc 파일에 아래 내용을 추가하세요
```
let g:instant_markdown_autostart = 0
```
이후 markdown파일을 보다가 preview하고 싶을때 아래 명령어를 실행하면 됩니다.
```
:InstantMarkdownPreview
```

한번 실행하게 되면 localhost:8090 port로 구동되며
다른 markdown창에서 타이핑을 치게되면 자동으로 해당 파일이 display됩니다.

완성된모습
![exmaple](/assets/images/2016-08-14-11-18-50.png)
