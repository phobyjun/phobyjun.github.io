---
title: "My First Post"

tags: [Github, Github Blog, Tech, 깃허브, 깃허브 블로그]

comments: true
---

Guithub 블로그 만들기.

<!--more-->

## Make a blog

* * *

작년에 만들기로 생각만 하고 실행에 옮기지 못한 블로그를 만들었다. Github의 Pages를 이용해 만들었으며, 기본적인 테마는 TaylanTatli의 Moon을 사용했다. 간단한 순서는 다음과 같다.



- 자신이 원하는 Jekyll 테마의 Github repo를 Fork.

- Fork한 repo의 이름을 <**자신의 Github 이름**.github.io>로 변경

- 선택한 테마의 가이드에 따라 _config.yml 및 기타 파일 변경



페이지가 생성되고 변경되는데는 평균적으로 1~2분의 시간이 걸렸다. 페이지의 변경 사항이 바로 적용되는 것이 아니니 인내심을 가지고 기다릴 것!



## Write posts

* * *

게시글을 쓰는 방법은 테마에 따라 다르겠지만 내 경우에는 /_posts디렉토리에 *.md 파일을 추가하는 것으로 가능했다.

파일의 이름은 항상 **YYYY-MM-DD-title.md**의 양식을 지켜야 하며 게시글의 상단부에는 다음과 같은 일정한 양식(?)이 들어간다.

```markdown

---

layout: post

title: "My First Post"

date: 2019-01-25

excerpt: "Github 블로그를 통해 블로그 만들기."

tags: [Github, Github Blog, Tech, 깃허브, 깃허브 블로그]

comments: true

---

```

위의 양식은 YAML 머리말이라 불리며, 간단히 말해 게시글의 정보 및 _config.yml에 적힌 양식에 따라 게시글을 작성해준다고 생각한다. 자세한 정보는 Jekyll 가이드를 참고하길!

<center><a href="https://jekyllrb-ko.github.io/docs/home/" class="btn btn-success">Go To Jekyll Docs</a></center>
- - -

<center>내 생애 첫 블로그 게시글 작성 성공!!</center>
- - -



위 게시글은 주관적인 의견에 의해 작성되었으며, 정확한 사실을 제공하지 않을수도 있습니다. 틀린 내용이 있다면 피드백 부탁드립니다.
{: .notice}
