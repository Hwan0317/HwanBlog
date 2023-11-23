---
title: '블로그 시작하기 (With.Hugo)'
date: 2023-11-23T15:27:38+09:00
draft: true
---

# Hugo로 블로그 만들기

> 필자는 모든 내용에 대한 정확한 동작 방식을 정확히 알고 있지 않습니다! 개인의 단순 기록 용도이니 참고 용도로만 봐주시길 부탁 드립니다.

## 드디어 블로그!

예전부터 블로그를 만들어 보면 좋을 것 같다는 생각(만) 해왔는데, 드디어 블로그 구축을 직접 해본다!

## SSG 및 테마 선택

SSG란 Static Site Generator의 약자로, 말 그대로 정적인 웹 사이트를 생성해주는

필자는 [Hugo](https://gohugo.io/), 테마는 [Pages](https://themes.gohugo.io/themes/hugo-paper/)를 선택 했는데, Hugo는 언젠가 Go를 직접 다루며 구조를 만질 수 있지 않을까 하는 기대에 선택 해보았다.~~물론 기본 포스팅을 하는 정도에서는 Go언어는 전혀 사용할 일이 없다.~~ 추가적으로 Pages는, 블로그를 처음 개설하는 만큼, 직접 핸들링 할 부분이 최대한 적은, 간단한 구조를 가진 ~~예쁜~~ 테마를 선택했다.

초기 구축을 한 뒤 아쉬운 점으로는, 일단 공식적인 docker 이미지가 지원 되지 않는다는 점이 가장 크게 느껴졌다. 이 부분은 추후에 직접 이미지를 빌드 하거나, 공식적인 이미지를 지원하는 다른 SSG를 사용하도록 변경 할 생각이다.



## Hugo 설치

> 이번 포스팅에서 기본적인 설치 및 사용은 윈도우를 기준으로 작성되었습니다.
> 이후 사용 방법 또한 OS 별로 차이가 있을 수 있음을 참고 부탁드립니다.


설치는 winget을 이용해 쉽게 설치 할 수 있다.

```sh
winget install Hugo.Hugo.Extended
```

winget이란? Windows에서 사용 가능한 Windows 패키지 관리자의 cui 명령어이다. debian계열 linux의 apt, MacOS의 homebrew와 같은 역할을 한다.

### 나머지 os

다른 os의 설치 방법은 [공식문서](https://gohugo.io/installation/) 참고. 대부분 brew, apt, snap등의 패키지 관리자를 통해 설치할 수 있도록 안내되어있다.

## 블로그 생성 및 테마 설정

hugo 설치 후, 블로그 작업공간을 생성해야한다.
작업공간 폴더를 만들 위치로 이동해, 아래 명령어를 통해 hugo 작업공간을 생성하고, 해당 작업공간(폴더)로 이동한다.

```
hugo new site Blog
cd Blog
```

초기 블로그 작업 공간의 구조는 아래와 같이 만들어진다. 각 디렉터리 및 파일의 정확한 역할 구조는 차차 알아갈 예정이다.

```sh
Blog
│  hugo.toml
│
├─archetypes
│      default.md
│
├─assets
├─content
├─data
├─i18n
├─layouts
├─static
└─themes
```

## 테마 적용

hugo에서 테마를 관리하는 방법은 크게 두가지다.

hugo 모듈로서 설치하거나, theme 디렉터리의 git submodule로 추가하는 방법이 있다.

아직 hugo 시스템 자체에 익숙하지 않아, 좀 더 직관적으로 느껴지는 git submodule 방식을 사용해 설치해보자.

```
git init
git submodule add https://github.com/nanxiaobei/hugo-paper themes/paper
```

먼저 작업 공간을 git을 통해 관리 하도록 초기화한다.

이후 원하는 테마의 git remote repo를 submodule로 추가한다. 테마는 [여기](https://themes.gohugo.io/tags/blog/)에서 찾을 수 있다.

## 로컬 서버 실행

아직 별도의 포스트를 작성하지 않은 상태이지만, 이대로 원하는 테마가 적용되었는지 확인 겸 hugo 서버를 동작시켜본다.

```
hugo server
```

서버는 기본적으로 1313 포트를 통해 접근 할 수 있다.
http://localhost:1313 으로 접근해 블로그를 확인해본다.

서버 실행 후 웹 브라우저 화면
![image](/images/Hugo_Theme_Done.png)

잘 만들어진것을 볼 수 있다. 이제 이 웹 브라우저는 열어두고 블로그 작성을 진행하면 된다. 서버는 블로그 작업 공간 내의 파일이 수정, 추가, 삭제 되는 것을 감지해 자동으로 새로고침 된다. 이를 통해 수정사항이 문제 없이 반영 되는지 쉽게 확인할 수 있다.

## 페이지 추가하기

이제 포스팅을 위한 새로운 페이지를 만들어보자.

기본적으로 hugo는 Markdown을 통해 작성되기 때문에 추가할 페이지 또한 Markdown의 확장자인 `.md` 으로 생성한다.

페이지 생성 명령어

```sh
hugo new content posts/my-first-post.md
```

생성된 페이지

![image](/images/genarated_post.png)

이제 제목, 소 제목,  본문과 앞으로 자주 사용하게 될 코드 셀 까지 아래처럼 추가 해 저장해본다.

![image](/images/post_add_test.png)

이렇게 추가하고 얼어둔 서버를 통해 확인해보자. 아무런 변화가 없을 것 이다. 뭔가 잘못된 것이 아니라 오히려 잘 된 상태이다.

위 사진을 보면 draft 값이 `true`로 되어있는데, 기본적으로 hugo server 는 draft가 `true`인 파일을 빌드하지 않도록 되어있다.

draft상태를 `false`로 변경하거나, 지금 동작중인 서버를 아래 명령어를 통해 draft 상태의 파일도 빌드하도록 재 실행 하면 된다.

```
hugo server -D
```

둘 중 어떤 방법이던 적용하고 나면, 아래와 같이 정상적으로! 빌드된 블로그를 맞이할 수 있게 된다!