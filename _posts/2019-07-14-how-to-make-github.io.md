---
layout: post
title:  "github.io 블로그 만드는 방법"
author: stashzero
categories: [ info ]
tags: [ github, theme ]
image: assets/images/github-fork.png
description: "github.io 블로그 만드는 방법"
featured: true
hidden: false
beforetoc: "ruby를 깊게 공부할 생각은 아직 없다. yml은 필수로 해야겠지만... 그래서 블로그를 만들 때, 깊게 생각하지 않았다. 특별한 것을 공부하지 않았다. 쉽게 개설하는 방법만을 찾았을 뿐"
toc: true
---

<br/>

github.io 블로그를 만드는 것은 비교적 쉽다.

> 이것만 기억하자.  
> 1. jekyll theme 찾기
> 2. fork 버튼 누르기  
> 3. git repository 변경
> 4. style 설정

<br/>
<br/>
<br/>  

# theme 찾기
- - -

theme 찾는 방법은 뭐 없다. 그냥 구글신께서 알아서 찾아주실 거다. 아래 링크를 따라가서 theme를 검색하자.

`jekyll theme` 라고 [검색](https://www.google.com/search?q=jekyll+theme){: target="_blank" }한다.



theme를 올려 둔 몇 가지 사이트를 발견할 수 있는데, github에서 해당 theme가 잘 활성화되고 있는지 여부만 판단하여 fork를 하면 된다.

- <https://jekyllthemes.io/>{: target="_blank" }

[![Git fork]({{ site.baseurl }}/assets/images/jekyllthemes-io.png)](https://jekyllthemes.io/){: target="_blank" }

- <http://jekyllthemes.org/>{: target="_blank" }

[![Git fork]({{ site.baseurl }}/assets/images/jekyllthemes-org.png)](http://jekyllthemes.org/){: target="_blank" }

<br/>
<br/>
<br/>  

# fork git repository
- - -
적절한 git theme를 찾았다면, 해당 git repository를 fork 하면 된다. fork 버튼을 누르면 내 저장소로 복사가 된다.

![Git fork]({{ site.baseurl }}/assets/images/github-fork.png)


<br/>
<br/>
<br/>  

# rename my repository
- - -

fork 가 완료되었으면, 내 저장소에 추가가 되면서 바로 이동이 될 텐데, 내 repository 이름을 변경한다.

변경한 이름이 내 블로그 url 로 사용이 된다.

![rename]({{ site.baseurl }}/assets/images/rename-repo.png)



# setup
- - -

혹시 스타일 등이 깨지면 _config.yml 파일의 baseurl 값이 잘못 되어 있을 수 있다. 우리는 언제나 오류들을 찾을 수 있는 준비가 된 개발자들이다. 적절하게 수정을 해주자.


```yml
# Site
name: "Stashzero"
title: "Stashzero"
description: "Hello World :)"
logo: 'assets/images/logo.png'
favicon: 'assets/images/logo.png'
baseurl: '/'    //여기를 적절하게 고쳐보자.
```

이렇게 내 블로그가 생겼다. 나도 이제 양산형 기술 블로거다.
