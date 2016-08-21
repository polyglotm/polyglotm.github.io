---
layout: post
title: "AngularJS e2e Test"
tags: AngularJS e2e 생각
---

### 적절한 독자 대상은?

* angularJS(1.x)를 처음 사용하는분
* jasmine이 뭔지모르거나 2.0이하 버젼을 사용하는분
* protractor를 사용하지만 mochaJS를 사용하고 있는 시스템을 사용하는분 
* yeoman-generator로 생성할 프로젝트에서 protractor task실행이 너무 길다고 느끼시는분

### 왜 E2E test를 작성하기로 결정하였나? 

그동안 회사에서 AngularJS기반 editor를 제작하면서
2월달에 에디터 코드를 첫 커밋한 이후로 현재 8월까지
일정을 맞추기 위해 끝없이 신규 기능을 개발해 왔고
요구사항이 점점 고도화되고 복잡해질수록
QA팀에 넘기기 전에 제가 해야할 테스트가 점점 늘어났습니다.

editor특성상 많은 이벤트 로직이 엮여있어 테스트 코드를 작성하기 매우 까다로운점은 사실이나 
새로운 기능을 넣었을때 영향이 없는지 확인하기 위해
그 매우 복잡하고 유기적인것을 제가 매번 직접 테스트를 했습니다.

특히 최근에 읽은 'The Clean Coder'에서 나오는 문구를 읽고 당장 해야겠다는 생각이 듭니다.

>폴라: "맞아, 그 정도면 될 거야"  
샘: "와, 필요한 게 이렇게나 많아?"  
폴라: "샘, 두 테스트 중에 안 중요한 테스트가 있다는 거야?"  
샘: "내 말은 모든 테스트를 생각해서 작성하려면 일이 엄청 많을 것 같다는 뜻이야"  
톰: "그렇지, 하지만 수작업 테스트 계획을 만드는 정도면 돼. 수작업 테스트를 하고 또 하는 거에 비하면 약과지."

제가 수작업으로 테스트를 할 수 있다는 것은 예측 가능한 범위 내에서 어떤 특정 행위를 매번 반복 하고 있었다는 것인데
그말인 즉 **'같은 행위는 코드로 작성이 가능하며 코드로 작성할경우 한번만 작성하면 된다.'** 라는 결론에 도달하게 됩니다.
  
  
  
### Protractor는 무었이고 어떻게 실행하는가?

![protractor-logo](/assets/images/2016-08-20-angular-e2e-test-begining/protractor-logo.png)

여러 테스트 프레임워크들 중에서도 angular팀에서 만들고
공식적으로 추천하며 유지하는 프레임워크인 [protractor](http://www.protractortest.org/)로 하기로 결정하였는데
protractor의 경우 기존에는 아래와 같이 실행해야 하지만

```
$ webdriver update
$ webdriver start
$ protractor protractor.conf.js
```

editor project를 [yeoman](http://yeoman.io/)의 
[generator-gulp-angular](https://github.com/swiip/generator-gulp-angular#readme)로 생성했기 때문에
karma-jasmine과 protractor가 기본적으로 세팅 되어 있었습니다.

그 말인 즉슨 이미 unit test, E2E 테스트 환경이 모두 준비 되어 있다는 것이지요.

단순히 protractor가 아니라 [gulp-protractor](https://github.com/mllrsohn/gulp-protractor)로 wrapping 되어 있기 때문에
yeoman-generator로 project를 생성할경우 *gulp task로 'protractor'가 추가되어 있기 때문에*
project root directory에서
~~~
$ gulp protractor
~~~
명령어만 실행해 주면 됩니다.

gulp-protractor를 쓰든, 그냥 protractor를 사용하던 한가지만 주의하면 되는데
2016-08-20기준 최신 protractor 4.0.3버전 이 jasmine 2.4.1 을 import해서 사용 하고 있습니다.

![jasmine-logo](/assets/images/2016-08-20-angular-e2e-test-begining/jasmine-logo.png)

**protractor는 [jasmine](https://github.com/jasmine/jasmine)문법을 따릅니다! 그리고 내부엔진도 jasmine을 사용합니다.**

gulp-protractor를 쓰는경우 3.0.0버전을 쓰셔야 protractor 4.0.3버전을 사용하고  
protractor의경우 4.0.3버젼이 되어야 jasmine2.4.1버젼 사용이 보장됩니다.

### jasmine은 최소한 2.0.0이상 버젼을 사용해야 합니다.

#### Javascript TDD책을 보고 계시는데 jasmine 2.0이하의 버젼으로 설명하고 있다면 새로운 책을 사는게 더 낳을겁니다!

>jasmine framework는 javascript test framework로써
mochaJS, chaiJS 와 같은 테스트 프레임워크들 사이에 있습니다.
>
>과거 jasmine 1.x시절에는 done() callback메소드
즉 promise스펙을 지원하지 않아
promise 스펙을 지원하는 mochaJS가 압도적으로 우세했지만
>
>**jasmine 2.0에서 비동기 콜백 함수 지원, 즉 promise spec을 구현**함에 따라
mochaJS + chaiJS promise 조합으로 사용하던 스택과  동등한 위치가 되었지요.
>
>이에따라 angularJS팀에서 만든 protractor 테스트 프레임워크가
기존에 mocha와 jasmine을 모두 지원하다가
공식적으로 [mocha를 더이상 지원하지 않겠다고 발표](https://github.com/angular/protractor/blob/master/docs/frameworks.md)하면서
jasmine의 관심도가 더 높아지게 되었습니다.

  
  
### gulp(yeoman-generator)기반 프로젝트를 이용하고 계시다면

~~~
$ gulp protractor
~~~
위 명령어를 한번 실행하시고는 
>테스트 한번 실행하는데 무슨놈에 30초 1분씩이나 걸려?!  
이래서 내가 TDD(BDD)를 안하는거야!  
TDD가 도데체 무슨 소용이야!  

라고 말씀하실수도 있으시겠지만!

##### 조금만 응용하면 테스트를 아주짧은시간에 실행 할 수 있습니다!
yeoman-generator로 생성된 **'protractor'** task는 내부적으로 아래와 같은 call stack을 갖게됩니다.  

~~~
gulp.task('protractor', ['protractor:src']);

gulp.task('protractor:src', ['serve:e2e', 'webdriver-update'], runProtractor);

gulp.task('serve:e2e', ['inject'], function () {
  browserSyncInit([conf.paths.tmp + '/serve', conf.paths.src], []);
});

gulp.task('inject', ['scripts', 'styles'], function () {
 ...너무많아서 생략
});

gulp.task('webdriver-update', $.protractor.webdriver_update);

$ webdriver update
$ webdriver start
$ protractor
~~~

**다 읽으시거나 모두다 이해하실 필요는 없어요. 그냥 아주 많다는 뜻입니다!**

여기서 중요한점은 ***'inject'*** task가 실행 된다는점인데
수시로 테스트할때 매번 protractor task를 이용해서 실행하지마시고

```
$ gulp serve
```

평소 개발할때 처럼 위와같이 serve task를 실행하면 시간을 제일 많이 잡아먹는 'inject' task도 함께 돌아가기 때문에 이상태에서

```
$ protractor
```

root directory에서 protractor명령어 만으로 protractor를 가볍게 실행하세요.
