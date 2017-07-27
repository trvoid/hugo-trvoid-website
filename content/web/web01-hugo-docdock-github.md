---
title: "Hugo + DocDock 웹사이트를 GitHub으로 서비스"
---

[Hugo](https://gohugo.io/) 프레임워크에 [DocDock](https://themes.gohugo.io/docdock/) 테마를 추가하여 정적 웹사이트를 만들고 이를 [GitHub](https://github.com/)에 올려서 서비스하는 과정을 정리하였습니다.

[TOC]

## 1 제품 소개

### 1.1 Hugo

* 정적 웹사이트를 생성하는 도구.
* Go 언어로 개발함.

### 1.2 DocDock

* 기술 문서 작성을 위한 Hugo용 테마.
* Learn 테마를 기반으로 함.

### 1.3 GitHub

* 소스 버전 관리 서비스 제공.
* 웹사이트 서비스 제공.

## 2 Hugo와 DocDock 설치

다음과 같은 환경에서 설치를 진행하고 이 문서를 작성하였습니다.

* 프로세서: Intel Core i5 (x64 기반)
* 운영체제: Windows 10 (64비트)

### 2.1 Hugo 설치
 
1) [Hugo Releases](https://github.com/gohugoio/hugo/releases) 페이지에서  hugo_0.25.1_Windows-64bit.zip 파일을 다운로드하고 압축을 풉니다.

2) 압축을 푼 폴더를 환경 변수 PATH에 추가하고 명령창을 엽니다.

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

위 명령은 quickstart 폴더에 새 사이트를 만듭니다.

4) 위에서 생성한 Hugo 사이트 폴더를 Git 저장소로 만듭니다.

    > cd quickstart
    > git init

### 2.2 테마 DocDock 추가

1) Hugo 테마 DocDock을 추가합니다.

    > cd quickstart
    > git submodule add https://github.com/vjeantet/hugo-theme-docdock.git themes/docdock

2) 테마 DocDock을 사용하도록 config.toml 파일에 다음 한 줄을 추가합니다.

    theme = "docdock"

## 3 컨텐츠 생성

### 3.1 컨텐츠 파일 작성

content 폴더 아래에 다음 파일들을 만들고 제시한 내용들을 추가합니다.

* content/_header.md

        QuickStart

* content/_index.md

        ---
        Title: "Home"
        ---
        # Home

* content/ble/_index.md

        ---
        Title: "Bluetooth Low Energy"
        ---

* content/ble/ble01-intro.md

        ---
        Title: "BLE01 - Introduction"
        ---

* content/ble/ble02-physical-layer.md

        ---
        Title: "BLE02 - Physical layer"
        ---

* content/ml/_index.md

        ---
        Title: "Machine Learning"
        ---

* content/ml/ml01-intro.md

        ---
        Title: "ML01 - Introduction"
        ---

* content/ml/ml02-linear-regression.md

        ---
        Title: "ML02 - Linear regression"
        ---

### 3.2 개발 서버로 웹사이트 검증

1) Hugo 개발 서버를 실행합니다.

    > cd quickstart
    > hugo serve

2) 브라우져로 아래 주소에 연결합니다.

    http://localhost:1313

3) 화면 왼쪽 사이드바에 메뉴가 나타나고 각각의 메뉴 항목을 클릭하여 위에서 작성한 모든 컨텐츠를 볼 수 있는지 확인합니다.

## 4 컨텐츠 배치

앞 단원에서 생성한 컨텐츠를 배치용으로 변환한 다음 GitHub 저장소에 올립니다. GitHub 계정의 사용자 이름이 *yourname*이라고 하면 GitHub 저장소 주소와 여기에 연결된 웹사이트 주소는 다음과 같습니다.

저장소 주소:

    https://github.com/yourname/yourname.github.io.git

웹사이트 주소:
    
    https://yourname.github.io

### 4.1 설정

config.toml

    baseURL = "https://yourname.github.io"
    languageCode = "en-us"
    title = "trvoid"
    theme = "docdock"

### 4.2 컨텐츠를 배치용으로 변환

    > cd quickstart
    > hugo

위 명령이 끝나면 아래 폴더에서 배치용 컨텐츠를 찾을 수 있습니다.

    quickstart/public/
    
### 4.3 컨텐츠를 GitHub에 배치

1) GitHub의 웹사이트 저장소를 복제합니다.

    > git clone https://github.com/yourname/yourname.github.io.git

2) 배치용 컨텐츠를 복제한 저장소에 덮어씁니다.

3) 변경 사항을 commit하고 push하면 GitHub 저장소에 반영됩니다.

4) 브라우져를 열고 다음 주소에 연결합니다

    https://yourname.github.io

5) 화면 왼쪽 사이드바에 메뉴가 나타나고 각각의 메뉴 항목을 클릭하여 위에서 작성한 모든 컨텐츠를 볼 수 있는지 확인합니다.

## 참고 자료

* [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)
* [Hugo Themes](https://themes.gohugo.io/)
* [How To Install and Use Hugo, a Static Site Generator, on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-hugo-a-static-site-generator-on-ubuntu-14-04)
