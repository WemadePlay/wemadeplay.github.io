# sundaytoz.github.io

https://sundaytoz.github.io

## 환경설정

### Windows & macOS

먼저 Ruby+Devkit (with DevKit) 버전을 설치합니다. [[다운로드]](https://rubyinstaller.org/downloads/)

```shell
# jekyll 및 bunlder 설치
$ gem install jekyll bundler

# 프로젝트 클론
$ git clone git@github.com:sundaytoz/sundaytoz.github.io

# 플러그인 설치
$ cd sundaytoz.github.io
$ bundle install
```

> macOS에서 번들 설치중 ffi 라이브러리 설치 단계에서 `libgcc_s` 의존성 때문에 설치가 불가능한 경우 `sudo ln -s /usr/lib/libSystem.B.dylib /usr/local/lib/libgcc_s.10.4.dylib`로 시스템 라이브러리로 심볼링 링크를 만든뒤 재설치. (참고: https://github.com/ffi/ffi/issues/651)

### 설치 시 오류

설치된 루비 버전이 2.6.0이 아닐 경우 jekyll 설치 시 오류가 발생합니다. (특히 Mac 카탈리나 설치 후)

그럴 땐 아래와 같이 rbenv를 설치하여 머신의 루비 버전을 변경하고 설치하면 됩니다.

```shell
$ brew install rbenv
$ rbenv init
$ rbenv global 2.6.0
$ rbenv version # 변경된 버전 확인
```

## 로컬 실행

```shell
$ bundle exec jekyll serve
$ open http://127.0.0.1:4000
```

`open` 할 주소는 환경 설정에 따라 달라질 수 있습니다.

터미널에 출력되는 메시지를 잘 읽고 해당 주소를 입력해서 실행하세요.

## 새글 등록

1. `_posts` 디렉토리에 yyyy-mm-dd-{name}.md 파일 복사.
- `{name}`: 해당 포스트의 고유 키로 url의 일부로 사용. 왠만하면 특수문자없이 `영문자`, `숫자`, `-`(하이픈), `.`(점)...만 사용.
- `yyyy-mm-dd`: 발행 년-월-일.
2. 마크다운 파일 최상단에 front matter 작성.
```yaml
---
layout: post # 레이아웃(필수). page 레이아웃을 사용하면 목록에 보이지 않는 글을 쓸 수 있음.
title: {title} # 제목(필수)
author: {lastname}.{firstname} # (현재 기능 미지원)
categories: [category1,category2] # 카테고리 항목
tags: [tag1,tag2,tag3,...] # 태그 목록(선택). 왠만하면 특수문자없이 영소문자, 숫자, -(하이픈), .(점)...만 사용.
image: {image_link} # 커버이미지 url(선택)
date: YYYY-MM-DD HH:MM:SS # 발행일(필수)
---
```

3. MarkDown 양식으로 포스트 작성.

## 카테고리 등록

1. 만약 새로운 글에서 새로운 카테고리 `CATEG`를 등록했다면
2. `category` 디렉토리에 `CATEG.md` 파일 생성 : 파일명은 카테고리명과 동일해야 함.
3. front matter 작성.
```yaml
---
layout: category # (필수)
title: CATEG # (필수) title은 파일명, 카테고리명과 동일해야 함.
---
```

