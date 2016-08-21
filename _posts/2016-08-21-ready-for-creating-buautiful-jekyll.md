---
layout: post
title: "지킬을 아름답게 만들기 위한 준비"
tags: jekyll
assets_directory: '/assets/images/2016-08-21-ready-for-creating-beautiful-jekyll'
---

## 서론 & 현재 상태

'buildfailed'라는 수많은 메일을 받고 나서야
드디어 github.io를 활용한 블로그가 시작되었습니다.

그렇다면 이제 꾸밀 시간이군요.

현재 상태는 말그대로 text만 있는 상태이니까요.
작업을 시작하기전 before를 스크린샷으로 남겨놓도록 합니다.

#### Screen shot 1 post 목록

![fure-jekyll-1]({{page.assets_directory}}/2016-08-15-04-31-18.png)

#### Screen shot 2 post layout

![fure-jekyll-1]({{page.assets_directory}}/2016-08-15-04-30-53.png)


네... 보다시피 처참합니다.
마치 90년대를 연상케하는군요 ㅋㅋㅋ..

2016년 8월 기준으로 최초 설치시 jekyll의 subproject인 minima theme이 적용되어 있습니다.

![minima-theme]({{page.assets_directory}}/minima.png)

저도 최초 실행할때는 분명 됬는데
딱 한번 실행후 minima theme이 안되는 상황이 발생하였습니다...
한번 깨지고 나니까 minima적용이 다시 안되네요...

사실 저는 theme제작은 한두달 뒤에 하려고 했는데
minima theme이 깨지는 바람에 90년대 웹이 되는 초유의 사태가 발생해서;;...

bower component를 로딩하게 도와주는 jekyll-assets gem으로 **bootstrap 4**적용도 실패!

*로딩만 되고 왜 적용이 안되는것이냐!!!*

네. 쉬운방법이 있지요. CDN으로 로딩합니다.


## jekyll directory 구조

#### 아래 directory 구조는 [jekyll 표준](http://jekyllrb-ko.github.io/docs/pages/)입니다. 

```
|-- _includes/ 
      -> component들을 만드는 위치입니다 없을경우 당황하지 말고 만들면 됩니다.
         header.html, footer.html등의 컴포넌트를 넣기에 적합합니다.

|-- _layouts/ 
      -> layout template을 넣는 곳입니다.
         이곳은 잠시 뒤 설명합니다.
|-- _drafts/
      -> 아직 게시하지 않을 초안을 작성 하는 곳 입니다.
         jekyll serve --drafts 옵션으로 local실행시 확인 할 수 있습니다.
|-- _posts/
      -> 게시할 post들
|-- _site/
      -> jekyll에 의해 생성된 페이지들
```

## layout template 구조 이해

최초 지킬을 실행하면 welcom-to-jekyll.markdown 파일이 생성되는데
최 상단에 아래와 같은 양식이 있습니다.

```
---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-07-30 14:54:42 +0900
categories: my_collection jekyll update
tags: test1 test2
---
```

여기서 주목할점은 layout: post인데
_layouts directory의 html들중

```
---
layout: post
---
```

라고 되어있는 html이 template으로 적용되게 됩니다.

## component 생성하기

jekyll에서는 _includes directory하위에 component를 생성하도록 하고 있습니다.
includes component 생성

저는 header.html, footer.html, 3rd-party-lib.html 이렇게 3가지로 생성했습니다.
각각 파일들을 아래와 같이 작성합니다.

#### 3rd-party-lib.html
```
<!-- bootstrap 4.0.0-alpha.3 -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.3/css/bootstrap.min.css" integrity="sha384-MIwDKRSSImVFAZCVLtU0LMDdON6KVCrZHyVQQj6e8wIEJkW4tvwqXrbMIya1vriY" crossorigin="anonymous">
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.0.0/jquery.min.js" integrity="sha384-THPy051/pYDQGanwU6poAc/hOdQxjnOEXzbT+OuUAFqNqFjL+4IGLBgCJC3ZOShY" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/tether/1.2.0/js/tether.min.js" integrity="sha384-Plbmg8JY28KFelvJVai01l8WyZzrYWG825m+cZ0eDDS1f7d/js6ikvy1+X+guPIB" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.3/js/bootstrap.min.js" integrity="sha384-ux8v3A6CPtOTqOzMKiuo3d/DomGaaClxFYdCu2HPMBEkf6x2xiDyJ7gkXU0MWwaD" crossorigin="anonymous"></script>

<!-- hightlight.js monokai_sublime css-->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/monokai_sublime.min.css">
<!-- highlight.js 9.6.0 -->
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```

> bootstrap 4와 hightlight.js를 사용하였습니다.
bootstrap은 너무 유명해서 따로 설명 안해도 될듯합니다만 
현재 블로그에 import한 [4.0.0-alpha](http://v4-alpha.getbootstrap.com/) vesion에 관한 글은 따로 다루도록 하겠습니다.
[highlight.js](https://highlightjs.org/)는 code highlight lib입니다.

#### header.html

{% highlight html %}
{% raw %}
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  {% include 3rd-party-lib.html %}
</head>
{% endraw %}
{% endhighlight %}

#### footer.html
```
 아직 아무것도 없습니다!
```

이제 작성한 파일들을 **post.html**파일에 적용 합니다.

#### post.html

{% highlight html %}
{% raw %}
---
layout: post
---

{% include header.html %}

<div class="container">
  <div class="title">
    <h1>{{ page.title }}</h1>
  </div>
  {{ page.content }}
</div>

{% include footer.html %}
{% endraw %}
{% endhighlight %}

## Style 적용하기

#### Sass file include

저의경우는 아래와 같이 _sass directory를 추가하였습니다.

```
|-- _includes/ 
|-- _layouts/ 
|-- _drafts/
|-- _posts/
|-- _sass/
    -> *.sass file들을 관리하기 위해 새로 만든 directory!
|-- _site/
```

**_sass/_post.scss** file을 아래처럼 작성하고

```
.container {
  .title {
    margin: 30px 0 0 0;
  }
  img {
    max-width: 100%;
    border: 2px solid;
    border-color: #37d6c7;
  }

  h2 {
    margin-top: 50px;
  }
}

```

**css/main.scss** 파일에 방금 생성한 _post.scss partial을 추가해줍니다.

```
@import "_post";
```

jekyll engine이 compile될때 main.scss파일을 css/main.css 파일로 변환하는데

아래와 같이 코드를 넣어주면 됩니다

```
 <link rel="stylesheet" href="css/main.css">
```



#### Pure CSS 파일을 이용하는경우

제일 간단한 방법은 main.css에 다 때려박는거지만
간단한것보다는 효율적인것이 낫지요

_includes directory에 ~~.css 파일을 만들고
아래와 같이 로드 하면 됩니다

{% highlight html %}
{% raw %}

<style>
  {% include main.css %}
</style>

{% endraw %}
{% endhighlight %}

#### Tip

css파일들을 아래 예시와 같이 _includes 하위 경로에 css directory를 별도로 만들어 놓고 import할수도 있습니다.

```
|-- _includes/
    |-- _css/
        |-- module-1.css
        |-- module-2.css
```

{% highlight html %}
{% raw %}

{% include _css/module-1.css %}
{% include _css/module-2.css %}

{% endraw %}
{% endhighlight %}

이때 주의할점은 jekyll에서 사용하는 Liquid template engine은 
include syntax를 사용할경우 _includes directory의 파일을 찾습니다.
directory를 /로 시작하여도 absolute directory는 _includes에서 시작합니다.


### 맺음말

정말 말그대로 지킬을 아릅답게 꾸미기 위한 준비 방법만 설명하고
정작 아름답게 만들질 못했네요!

그래도 jekyll을 쓰면서 참 대단하다는 생각이 듭니다.
markdown으로 글을 쓰니까 정말 글쓰기에만 집중하면 되고
jekyll엔진 덕분에 무한정 customize가 가능하니까요.
