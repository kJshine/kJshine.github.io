---
layout: single
title:  "Git hub 블로그 이미지 경로"
categories: jekyll
tag: [image, github pages, jekyll]
author_profile: false
---

이전의 포스트를 작성하면서 이미지 삽입에 문제를 겪었다.

```markdown
![2023-11-08_001](../assets/images/2023-11-08-duplicate_repository/2023-11-08_001.jpg)
```

이런식으로 작성을 하면 경로는 잘 찾는다... 그런데 서버에 올리면

**https://kjshine.github.io/git/assets/images/2023-11-08-duplicate_repository/2023-11-08_001.jpg**

이런식으로 이미지의 경로를 가져온다. 내가 원하는 경로는 

**https://kjshine.github.io/assets/images/2023-11-08-duplicate_repository/2023-11-08_001.jpg**

이렇게 assets 앞에 git이 빠져야 한다. 앞에 붙은 git이 뭔지 확인을 해보니 내가 작성한 포스트의 카테고리 였다...   

### 원인

이 블로그는 jekyll을 사용하여 만든 블로그이다.
url은 repository name이 기본이다.

**ex) https://kjshine.github.io**

이 뒤에 내가 올릴 마크다운 파일이 포스트가 되는 것인데   
이 마크다운 파일에 git이라는 **카테고리가 있다면** 기존 url뒤에 git/포스트이름이 붙게된다.

이부분 때문에 이미지의 경로에 git이라는 경로가 추가된 채로 찾게된 것이였다.

**ex) https://kjshine.github.io/git/duplicate_repository**

### 문제해결

이미지의 경로를 상대경로에서 절대경로로 바꿔준 것만으로 쉽게 해결했다.

```markdown
![2023-11-08_001](/assets/images/2023-11-08-duplicate_repository/2023-11-08_001.jpg)
```

**[Git hub 블로그 참조]** [Git hub jekyll-theme](https://github.com/topics/jekyll-theme)
{: .notice--info}
