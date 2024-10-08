---
layout: single
title: "[02] Jekyll을 이용한 테마 적용"
author_profile: false
categories:
  - github-blog
toc: true
toc_sticky: true
sidebar:
  nav: "sidebar-category"
typora-root-url: .
---

# 0. Jekyll

> [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/)

이전 과정에서 Github Blog를 생성하고 `.html`을 이용하여 간단한 페이지를 호스팅해 보았다. 다만 실제로 Blog가 기능하기 위해서는 메뉴나 제목, 내용 등의 보다 다양한 구성품이 필요할 것이다.

정적 사이트 생성기인  Jekyll을 통해 Github Blog에 테마를 적용하여 이러한 구성을 적용해 보도록 하겠다.



# 1. Jekyll과 Bundler 설치

> [https://jekyllrb-ko.github.io/docs/](https://jekyllrb-ko.github.io/docs/)

사전에 Ruby가 설치되어 있어야 한다.

Ruby가 설치되어 있다는 가정하에 아래 내용을 진행하여 jekyll과 bundler를 설치한다.

```bash
gem install jekyll bundler
```



내 Blog 폴더로 이동하여 Jekyll을 실행하고 Bundler Install을 진행한다. 만약 이전과정에서 생성한 `index.html` 파일이 존재할 경우 삭제해 준다.

```bash
rm -rf ~/blog/index.html
```

```bash
cd ~/blog
jekyll new ./
bundler install
```



# 2. Jekyll 실행

## 2.1. Local에서 실행

아래 명령어를 입력하여 Remote에서 호스팅하기 전 Local에서 Jekyll을 실행하여 미리 결과 화면을 살펴볼 수 있다.

```bash
bundle exec jekyll serve
```

![image-20240920142601823](/assets/02_apply_jekyll_theme/image-20240920142601823.png)



Jekyll을 실행한 후 브라우저 주소창에 [http://127.0.0.1:4000](http://127.0.0.1:4000) 또는 [http://localhost:4000](http://localhost:4000)을 입력하여 확인한다.

![Screenshot-6810115](/assets/02_apply_jekyll_theme/Screenshot-6810115.png)



## 2.2. Remote에 배포

> [https://hognod.github.io](https://hognod.github.io)

Github에 Jekyll 활성화 내용을 Push하여 브라우저 주소창에 Repository 명을 입력하여 호스팅되는 내용을 확인한다.

```bash
git add .
git commit -m 'Jekyll 활성화'
git push origin main
```

![Screenshot-6810293](/assets/02_apply_jekyll_theme/Screenshot-6810293.png)



# 3. 테마 적용

## 3.1. 테마 다운로드

> - [https://jamstackthemes.dev/ssg/jekyll](https://jamstackthemes.dev/ssg/jekyll)
> - [http://jekyllthemes.org](http://jekyllthemes.org)
> - [https://jekyllthemes.io](https://jekyllthemes.io)
> - [https://jekyll-themes.com](https://jekyll-themes.com)



Jekyll 테마를 적용시키기 위해 우선 위의 사이트 등에서 마음에 드는 테마를 선택하여 다운로드하여야 한다. 나는 우선 심플하면서 카테고리 기능이 포함된 테마를 원했기 때문에 **Minimal Mistakes** 테마를 선택했다.

> [https://github.com/mmistakes/minimal-mistakes](https://github.com/mmistakes/minimal-mistakes)

![Screenshot-6811011](/assets/02_apply_jekyll_theme/Screenshot-6811011.png)



`Download ZIP` 항목을 선택하여 `.zip` 파일을 다운로드 후 압축을 풀어준다.



## 3.2. 테마 복사

다운로드 후 압축을 해제한 테마 폴더안의 숨김 파일을 포함하여 전부 복사한다.(MacOS의 경우 `Command`+`Shift`+`.` 키를 입력하면 숨김 파일이 전부 보여진다.)

![image-20240920144912838](/assets/02_apply_jekyll_theme/image-20240920144912838.png)

 

내 Blog 폴더로 이동하여 복사한 전체 내용을 붙여넣어 준다. 이 때 동일 이름을 가진 파일에 대해서는 전부 `대치` 적용한다.

![Screenshot-6811669](/assets/02_apply_jekyll_theme/Screenshot-6811669.png)

아래 리스트의 필요없는 파일은 제거한다. (선택 사항)

> [https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remove-the-unnecessary](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remove-the-unnecessary)

* `.editorconfig`
* `.gitattributes`
* `.github`
* `/docs`
* `/test`
* `CHANGELOG.md`
* `README.md`
* `screenshot-layouts.png`
* `screenshot.png`



테마 내용이 제대로 복사되었는지 Local에서 확인한다.

```bash
bundle install
bundle exec jekyll serve
```

![Screenshot-6811828](/assets/02_apply_jekyll_theme/Screenshot-6811828.png)



만약 `control` + `c`를 입력하여 서버 구동 중지 후 다시 `bundle exec jekyll serve` 명령어를 통해 서버 구동 시 에러가 발생한다면 `_site` 폴더를 지우고 다시 구동하면 정상 동작할 것이다.

`_site` 폴더의 경우 Local에서 서버를 구동시키기 위해 필요한 폴더이므로 `.gitignore`에 등록하여 Remote 환경에 Push되지 않도록 한다.



## 3.3. Remote에 배포

> [https://hognod.github.io](https://hognod.github.io)

Local에서 테마가 정상적으로 적용된 것을 확인하였으면 Remote에 배포하여 테마가 적용된 모습이 제대로 호스팅되는 것을 확인한다.

```bash
git add .
git commit -m 'Jekyll Minimal Mistakes 테마 적용'
git push origin main
```

만약 `error: RPC failed; HTTP 400 curl 22 The requested URL returned error: 400` 에러가 발생한다면 Push할 용량이 git defatul Buffer 사이즈보다 커서 발생하는 에러이므로 아래 명령어를 이용하여 Buffer를 늘려준 후 다시 Push하면 된다.

```bash
git config http.postBuffer 524288000
```



![Screenshot-7252587](/assets/02_apply_jekyll_theme/Screenshot-7252587.png)
