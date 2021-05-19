---
layout: post
title: "Atom 에디터 설치 및 세팅 (markdown package 위주)"
date: 2017-04-14 19:48:35 +0900
categories:   Atom, Markdown
---

### 개요
[Atom flight-manual](http://flight-manual.atom.io/) 및 구글링 바탕 작성 - 2017.04.14

#### Atom Editor를 선택한 이유
github blogging를 위해 Markdown Editor 필요. sublime text3을 사용하다가 다음 블로거의 멘트가 결정적이었음
>아톰은 여러 운영체제에서 사용할 수 있는 서브라임 텍스트(Sublime Text)와 맥 OS에서 주로 사용되는 텍스트메이트(TextMate)의 핵심 기능을 가져왔다. 두 텍스트 편집기가 가지고 있는 유용성, 편리성에 이맥(Emacs)과 VIM이 가지고 있는 극단적인 확장성을 더했다. 따라서 사용해 보면 서브라임 텍스트를 쓰는 것과 분위기상 차이가 나지 않는다. 잘 정리된 서브라임 텍스트같은 느낌이다.  
> ... 중략 ...
>무엇 보다도 마크다운(Markdown)으로 글 쓰는 사람에게 아톰 보다 나은 선택은 없는 것 같았다.  

[출처 - 장난(?)으로 시작한 여정, 없어서는 안될 Atom 편집기!](http://offree.net/entry/Atom-A-Hackable-Text-Editor-for-The-21st-Century)

### Atom Editor 설치
Atom Site(http://atom.io) 에서 Atom 설치 파일 다운로드 및 설치
>Atom is available with a Windows installer that can be downloaded from https://atom.io or from Atom Releases named AtomSetup.exe.
This setup program will install Atom, add the atom and apm commands to your PATH, create shortcuts on the desktop and in the start menu, add an "Open with Atom" context menu in the Explorer and make Atom available for association with files using "Open with...".

[출처 - Atom Flight : Installing Atom on Windows](http://flight-manual.atom.io/getting-started/sections/installing-atom/#installing-atom-on-windows)

### Markdown 패키지 설치 및 설정
#### 프록시 환경에서 패키지 설치

- 프록시 환경에서 패키지 설치시 에러발생 :  it shows an error "unable to verify the first certificate
- Atom Strict-ssl 설정 false 설정 및 프록시 서버 셋팅 필요
##### strict-ssl fale / 프록시 서버 세팅
```
C:\Users\S>apm config set strict-ssl false
C:\Users\S>apm config set https-proxy http://proxyserver:포트
C:\Users\S>apm config set http-proxy http://proxyserver:포트
C:\Users\S>apm config get https-proxy
http://proxyserver:포트
C:\Users\S>apm config get http-proxy
http://proxyserver:포트
```
[참고1 - How to install plugins behind a proxy with a self-signed certificate?](https://github.com/Microsoft/vscode/issues/155)  
[참고2 - Atom Flight : Proxy and Firewall Settings Manual](http://flight-manual.atom.io/getting-started/sections/installing-atom/#behind-a-firewall)
#### markdown-preview-enhanced 설치

#### language-markdown 설치
- Package 설명
>Adds grammar support for Markdown (including Github flavored, AtomDoc, Markdown Extra, CriticMark, YAML/TOML front-matter, and R Markdown), and smart context-aware behavior to lists, and keyboard shortcuts for inline emphasis.
#markdown #commonmark #gfm #github flavored #markdown extra

- 설치
>**Installation**
>1. Install language-markdown
>* via either your terminal: apm install language-markdown  
>* the Atom GUI: Atom > Settings > Install > Search for language-markdown.  
>
>2. Select language-markdown as your Markdown grammar. Open a Markdown file and
>* press ctrl+shift+L and choose "Markdown" choose "Markdown" from the grammar >selection interface in the bottom right-hand corner of the window
>
>To avoid conflicts this package tries to disable the core package language-gfm. If you run into any issue, make sure you've selected the correct grammar.

[출처 - language-markdown](https://atom.io/packages/language-markdown)

#### Monokai Extended Theme 설치
>**Installation**
>
>You can open the Atom settings (cmd-,), select Themes and search for >monokai-extended or install via the command line with apm:
>```apm install monokai-extended```
>Once installed, activate the theme by opening the Atom settings (cmd-,) and >going to Themes -> Syntax Theme or via cmd-shift-p and Settings View - Change >Themes.  

[출처 - Monokai Extended Theme](https://atom.io/themes/monokai-extended)

#### 패키지 동기화 도구 : sync-settings

1. github Personal access tokens 생성

2.
