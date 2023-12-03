---
title: 'Github Pages 로 호스팅하기'
date: 2023-12-03T22:49:17+09:00
draft: false
---
## 블로그 보기를 돌 같이 하자

[이전 포스트](/HwanBlog/posts/first-post/) 에서 로컬에서 블로그 포스팅 결과물을 보기 위해 hugo server를 사용해 웹 브라우저를 통해 볼 수 있게 해보았다.

하지만 매번 열심히 포스팅을 작성하고, 집에서 혼자 볼 생각으로 만들기 시작한 건 아니니 누구나 볼 수 있도록 배포(Deploy)를 해보자.

## 배포 방식 선택하기

배포를 하는 방법은 여러가지가 있는데 일단 하드웨어를 직접 구축해  사용한다거나, aws를 사용해 ec2에 배포한다거나... 정말 여러가지 옵션으로 배포 할 수 있는데, 필자는 github Pages를 통해 배포한다.

Github Pages 를 선택한 이유는 여러가지가 있는데, 첫째로 이미 git 을 통해 블로그 소스를 관리하고 있어 git을 통해 github. 둘째로는 별도의 도메인 호스팅 비용이 들지 않는다. 셋째로는 물리적인 서버도 필요 없다. 

도메인 호스팅과 물리적인 서버를 통해 직접 서비스 하려면 비용 측면의 문제는 둘째 치고, 도메인과 서버를 직접 연결하는 과정과, 물리적인 서버를 외부 노출 시키는 등의 네트워크와 관련된 지식이 필요하다.

가장 중요한 것은 간단하게 시작하기 위함이다. 설정 자체에 너무 목 매이지 않고 최대한 간결하게, 문제가 생길만한 여지를 지워두고 '배포' 그 자체에 집중해본다.

## GitHub Pages 설정하기

github pages 초기 화면

![image](/HwanBlog/images//github_action_Source_default.png)

Source 원본을 GitHub Action으로 변경해준다. 변경하고 나면 아래와 같이 추천 workflow 템플릿을 띄워주는데, hugo를 선택하면 된다. 만일 추천에 hugo가 보이지 않는다면, github action으로 직접 이동해서, hugo를 검색, 선택해주면 된다.

![image](/HwanBlog/images//github_action_hugo.png)

이 외에 custom domain등 별도의 설정을 추가적으로 할 수 있지만, 목적에 맞게 최대한 버튼을 적게 ~~'딸깍'~~ 누르고, 설정한다.

## GitHub Action 설정하기

![image](/HwanBlog/images//github_action_webIDE.png)

위에서 Hugo GitHub Action의 configure 버튼을 누르면 위와 같은 Web IDE에서 GitHub Action을 편집할 수 있게 되는데, 이 부분은 나중에 GitHub Action 자체를 다루는 포스팅  ~~희망사항~~ 을 통해서 알아보도록 하자.

오른쪽 위에 보이는 `commit changes...` 버튼을 누르고, 이후 팝업에 커밋 메세지를 입력 한 뒤 커밋해주면, 변경사항이 Repo에 저장되고, 해당 커밋에 의한 Action이 실행되게 된다.

![image](/HwanBlog/images//Run_Action.png)

Repo의 Action으로 이동하면 실행된 액션을 확인할 수 있다. Action에 대한 간단한 부가설명을 덧붙이자면, action.yml 파일에서 언제 Action이 실행될 지 정할 수 있고, 이번에 만든 hugo.yml파일은 main 브랜치에 push 가 발생하면 동작하도록 설정되어있다. 고로 앞으로는 git push를 하게되면 자동으로 배포가 이루어지게 된다.

실행된 Action을 클릭해 들어가게 되면 아래와 같은 세부적인 실행 정보를 볼 수 있는데, deploy 부분에 링크가 해당 페이지가 배포된 링크를 보여주는 것이다 .

![image](/HwanBlog/images//Action_Details.png)

클릭해 이동하면 정상적으로 배포된 GitHub Pages를 확인 할 수 있다.

![image](/HwanBlog/images//deploied_pages.png)

## referance

[HOSTING AND DEPLOYMEN - Host on GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/)