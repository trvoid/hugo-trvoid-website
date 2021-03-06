---
title: "Hugo + DocDock 웹사이트를 GitHub Pages로 호스팅하기"
---

[Hugo](https://gohugo.io/) 프레임워크에 [DocDock](https://themes.gohugo.io/docdock/) 테마를 추가하여 정적 웹사이트를 만들고 이를 [GitHub](https://github.com/) 저장소에 올려서 [GitHub Pages](https://pages.github.com/)로 호스팅하는 과정을 정리하였습니다.

## 1 제품 소개

### 1.1 Hugo

* 정적 웹사이트를 생성하는 도구.
* Go 언어로 개발함.

### 1.2 DocDock

* 기술 문서 작성을 위한 Hugo용 테마.
* [Learn](https://themes.gohugo.io/hugo-theme-learn/) 테마를 기반으로 함.

### 1.3 GitHub Pages

* 정적 웹사이트 호스팅 서비스를 무료로 제공.
* GitHub 저장소와 직접 연결.
* 개인, 조직, 프로젝트 유형에 따른 페이지 제공.
* 사이트 저장 용량은 최대 1GB.

## 2 Hugo와 DocDock 설치

다음과 같은 환경에서 설치를 진행하고 이 문서를 작성하였습니다.

* 프로세서: Intel Core i5 (x64 기반)
* 운영체제: Windows 10 (64 비트)

### 2.1 Hugo 설치
 
1) [Hugo Releases](https://github.com/gohugoio/hugo/releases) 페이지에서 다음 파일을 다운로드하고 압축을 풉니다.

    hugo_0.25.1_Windows-64bit.zip

2) 압축을 푼 폴더를 환경 변수 `PATH`에 추가하고 사이트를 생성하고자 하는 폴더에서 명령창을 엽니다.

3) 다음과 같이 명령을 실행하여 새 Hugo 사이트를 생성합니다.

    C:\DevApps\hugo_0.25.1_Windows-64bit>hugo new site quickstart
    Congratulations! Your new Hugo site is created in C:\DevApps\hugo_0.25.1_Windows-64bit\quickstart.
    
    Just a few more steps and you're ready to go:
    
    1. Download a theme into the same-named folder.
       Choose a theme from https://themes.gohugo.io/, or
       create your own with the "hugo new theme <THEMENAME>" command.
    2. Perhaps you want to add some content. You can add single files
       with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
    3. Start the built-in live server via "hugo server".
    
    Visit https://gohugo.io/ for quickstart guide and full documentation.

위 명령은 `quickstart` 폴더에 새 사이트를 만듭니다.

4) 위에서 생성한 Hugo 사이트 폴더를 Git 저장소로 만듭니다.

    > cd quickstart
    > git init

이후부터 본문에서 언급하는 폴더들과 명령창에서 실행하는 명령들의 기준 위치는 `quickstart` 폴더입니다.

### 2.2 테마 DocDock 추가

1) Hugo 테마 DocDock을 `themes/dockdock` 폴더에 추가합니다.

    > git submodule add https://github.com/vjeantet/hugo-theme-docdock.git themes/docdock

2) 테마 DocDock을 사용하도록 `config.toml` 파일에 다음 한 줄을 추가합니다.

    theme = "docdock"

## 3 컨텐츠 생성

컨텐츠는 `content` 폴더 아래에서 Markdown 문법을 사용하여 작성합니다. 폴더의 계층 구조는 웹사이트 좌측 메뉴바의 계층 구조로 나타납니다. 또한 각 폴더의 `_index.md` 파일에서 작성한 내용은 해당 폴더의 주 화면에 표시됩니다.

### 3.1 컨텐츠 파일 작성

실습을 위하여 `content` 폴더 아래에 다음 파일들을 만들고 제시한 내용들을 저장합니다.

* _header.md

    화면 좌측 상단에 표시할 문구를 작성합니다.

        QuickStart

* _index.md

    홈 화면에서 표시할 문서를 작성합니다.

        ---
        Title: "Home"
        ---
        # Home

* ble/_index.md

    `ble` 폴더의 주 화면에서 표시할 문서를 작성합니다.

        ---
        Title: "Bluetooth Low Energy"
        ---

* ble/ble01-intro.md

    `ble` 폴더의 하위 메뉴로 표시할 문서를 작성합니다.

        ---
        Title: "BLE01 - Introduction"
        ---

* ble/ble02-physical-layer.md

    `ble` 폴더의 하위 메뉴로 표시할 문서를 작성합니다.
    
        ---
        Title: "BLE02 - Physical layer"
        ---

* ml/_index.md

    `ml` 폴더의 주 화면에서 표시할 문서를 작성합니다.

        ---
        Title: "Machine Learning"
        ---

* ml/ml01-intro.md

    `ml` 폴더의 하위 메뉴로 표시할 문서를 작성합니다.

        ---
        Title: "ML01 - Introduction"
        ---

* ml/ml02-linear-regression.md

    `ml` 폴더의 하위 메뉴로 표시할 문서를 작성합니다.

        ---
        Title: "ML02 - Linear regression"
        ---

### 3.2 개발 서버로 웹사이트 검증

1) Hugo 개발 서버를 실행합니다.

    > hugo server

2) 브라우져로 아래 주소에 연결합니다.

    http://localhost:1313

3) 화면 왼쪽 사이드바에 메뉴가 나타나고 각각의 메뉴 항목을 클릭하여 위에서 작성한 모든 컨텐츠를 볼 수 있는지 확인합니다.

## 4 컨텐츠 배치

`content` 폴더 아래에서 작성한 컨텐츠를 GitHub Pages 서비스를 통해서 호스팅하려면 먼저 배치용 컨텐츠로 변환해야 합니다. 변환 결과는 `public` 폴더 아래에 저장되고 `public` 폴더 아래의 내용을 GitHub 저장소에 올리면 바로 웹으로 서비스됩니다. GitHub 계정의 사용자 이름이 *yourname* 이라고 하면 GitHub 저장소 주소와 여기에 연결된 웹사이트 주소는 다음과 같습니다.

GitHub 저장소 주소:

    https://github.com/yourname/yourname.github.io.git

GitHub Pages 웹사이트 주소:
    
    https://yourname.github.io

### 4.1 설정

`config.toml` 파일을 열고 `baseURL` 항목의 값을 `/`로 지정합니다.

    baseURL = "/"
    languageCode = "en-us"
    title = "QuickStart"
    theme = "docdock"

### 4.2 GitHub 저장소를 서브모듈로 추가

GitHub의 웹사이트 저장소를 서브모듈로 `public` 폴더 아래에 추가합니다.

    > git submodule add https://github.com/yourname/yourname.github.io.git public

### 4.3 컨텐츠를 배치용으로 변환

아래와 같이 명령을 실행하여 배치용 컨텐츠로 변환합니다.

    > hugo

위 명령이 끝나면 `public` 폴더에서 배치용 컨텐츠를 찾을 수 있습니다.
    
### 4.4 컨텐츠를 GitHub에 배치

1) `public` 폴더의 변경 사항을 commit하고 push하면 GitHub 저장소에 반영됩니다.

2) 브라우져를 열고 다음 주소에 연결합니다

    https://yourname.github.io

3) 화면 왼쪽 사이드바에 메뉴가 나타나고 각각의 메뉴 항목을 클릭하여 위에서 작성한 모든 컨텐츠를 볼 수 있는지 확인합니다.

## 참고 자료

* [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)
* [Hugo Themes](https://themes.gohugo.io/)
* [How To Install and Use Hugo, a Static Site Generator, on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-hugo-a-static-site-generator-on-ubuntu-14-04)
* [What is GitHub Pages?](https://help.github.com/articles/what-is-github-pages/)
* [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
