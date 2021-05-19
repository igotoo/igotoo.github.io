---
layout: post
title: "맥기반 jekyll로 github blogging - 01"
date: 2017-03-20 15:48:35 +0900
categories: jekyll, github
---

### 프롤로그
github blogging를 기존에 jeykll fork로 시도했다가 바로 중단한 것을 Markdown 매력과 날로 쇠약해지는 기억의 보조장치를 만들고자 nolboo님의 블로그 [지킬로 깃허브에 무료 블로그 만들기](https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/)을 기반으로 다시 시작함.
제발 부디 지속하기를 바라며 전달될 확률이 거의 없지만 블로그에 좋은 자료를 만들어 공유해 주신 nolboo님께 감사드린다. (2017.03.30)  

>[Jekyll](http://jekyllrb.com)은 여러(특히 마크다운) 형태의 텍스트와 테마를 소스로 하여 정적 HTML 웹사이트를 제너레이트하는 툴이다.  Ruby 스크립트로 만들어져 있으나, 블로그를 만드는 데에는 루비를 전혀 몰라도 된다. 워드프레스를 사용하여 블로그를 만드는 노력이면 워드프레스보다 훨씬 더 빠르고 보안에도 뛰어난 블로그를 깃허브에 무료로 만들 수 있고, 별도의 페이지를 만들기도 쉽다. 또한, HTML과 CSS에 대한 약간의 지식만 있으면 페이지는 물론 각 포스트마다 다른 레이아웃을 줄 수도 있다.

### 1. 설치
- RubyGems으로 로컬에 Jekyll 및 Bundler gems 설치
```
    iMac:~ igotoo$ ruby -v
    ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin16]
    iMac:~ igotoo$ gem install jekyll
    Fetching: public_suffix-2.0.5.gem (100%)
    ERROR:  While executing gem ... (Gem::FilePermissionError)
        You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.
    iMac:~ igotoo$ sudo gem install jekyll
    Password:
    Fetching: public_suffix-2.0.5.gem (100%)
```    
[참고 - Quick-start guide](http://jekyllrb.com/docs/quickstart/)
### 2. github 계정 주소 페이지로 블로그 생성하기
- 계정주소 ? : http://igotoo.github.io   
#### 1) 로컬 jekyll 블로그 생성

- 깃허브사용자명.github.com 디렉토리를 만들어 기본 디렉토리와 화일을 생성
- jeykll new 깃허브사용자명.github.com
  ```        
  iMac:~ igotoo$ jekyll new igoto.github.com
        Dependency Error: Yikes! It looks like you don't have bundler or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- bundler' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
      jekyll 3.4.3 | Error:  bundler
      iMac:~ igotoo$ jekyll new igoto.github.com
                Conflict: /Users/igotoo/igoto.github.com exists and is not empty.
  ```
- **Dependency Error:** 발생   
해결

1) ruby 재설치 및 환경 구성

- macOS 시스템 ruby 사용하지 않기 (v 2.0.0)
    * [이유 :The root problem is not with using a pre-installed Ruby per se, but with not using a Ruby version manager.](https://robots.thoughtbot.com/psa-do-not-use-system-ruby)
- homebrew 이용 ruby 버전 관리자 rbenv 설치
    *  homebrew(the missing package manager for macOS install) 설치 [HomeBrew](https://brew.sh)
- rbenv로 ruby 2.3.3  설치
- [rbenv not changing ruby version](http://stackoverflow.com/questions/10940736/rbenv-not-changing-ruby-version)
    * system ruby가 아닌 rbenv로 설치한 ruby를 사용하도록 변경
    *  ruby는 스크립트로 실행환경에 대한 redirector

    >First step is to find out which ruby is being called:   
       which ruby  
    >Your system says:   
    /usr/bin/ruby  
    >This is NOT the shim used by rbenv, which (on MacOS) should look like:
    /Users/<username>/.rbenv/shims/ruby
    >Use this to make sure your *MacOS will obey you:  
        eval "$(rbenv init -)"
    >Then add the line to your profile so it runs each time you open a new terminal window:
         ~/.bash_profile  
    >eval "$(rbenv init -)"   
  ```
              iMac:shims igotoo$ rbenv init -
              export PATH="/Users/igotoo/.rbenv/shims:${PATH}"
              export RBENV_SHELL=bash
              source '/usr/local/Cellar/rbenv/1.1.0/libexec/../completions/rbenv.bash'
              command rbenv rehash 2>/dev/null
              rbenv() {
                local command
                command="$1"
                if [ "$#" -gt 0 ]; then
                  shift
                fi

                case "$command" in
                rehash|shell)
                  eval "$(rbenv "sh-$command" "$@")";;
                *)
                  command rbenv "$command" "$@";;
                esac
              }

       [eval 참조](https://mug896.github.io/bash-shell/eval.html)    

              Mac:~ igotoo$ cat /Users/igotoo/.rbenv/shims/ruby
              #!/usr/bin/env bash
              set -e
              [ -n "$RBENV_DEBUG" ] && set -x

              program="${0##*/}"
              if [ "$program" = "ruby" ]; then
                for arg; do
                  case "$arg" in
                  -e* | -- ) break ;;
                  */* )
                    if [ -f "$arg" ]; then
                      export RBENV_DIR="${arg%/*}"
                      break
                    fi
                    ;;
                  esac
                done
              fi

              export RBENV_ROOT="/Users/igotoo/.rbenv"
              exec "/usr/local/Cellar/rbenv/1.1.0/libexec/rbenv" exec "$program" "$@"
  ```
2) rails 설치  
    ```
        iMac:~ igotoo$ rbenv global 2.3.3
        iMac:~ igotoo$ rbenv local 2.3.3
        iMac:~ igotoo$ rbenv rehash
        iMac:~ igotoo$ rails -v
            Rails 5.0.2        
    ```
    > rehash 옵션은 새로운 환경을 재설정하는 옵션으로 새로 루비를 설치하거나 루비 젬을 설치한 다음 반드시 실행해야 한다.

[참조 : 맥 OSX 개발머신에 설치하기](https://rorlab.gitbooks.io/railsguidebook/content/contents/rails/mac_install.html)

3) jekyll 재설치
```
        iMac:~ igotoo$ jekyll new igotoo.github.com
            Running bundle install in /Users/igotoo/igotoo.github.com...
            :
            New jekyll site installed in /Users/igotoo/igotoo.github.com.
```


4) [로컬](http://localhost:4000)에 웹서버 기동하여 블로그 확인하기
>지킬은 웹서버를 내장하고 있어 아파치나 NgineX와 같은 별도의 웹서버를 띄우지 않고도 사이트를 확인할 수 있다. --watch는 사이트를 변경하는 대로 백그라운드에서 >제너레이트하여 브라우저에서 변경사항을 바로 확인할 수 있는 옵션이다.

```
    Mac:igotoo.github.com igotoo$ jekyll serve --watch
    Configuration file: /Users/igotoo/igotoo.github.com/_config.yml
    Configuration file: /Users/igotoo/igotoo.github.com/_config.yml
                Source: /Users/igotoo/igotoo.github.com
           Destination: /Users/igotoo/igotoo.github.com/_site
     Incremental build: disabled. Enable with --incremental
          Generating...
                        done in 0.477 seconds.
     Auto-regeneration: enabled for '/Users/igotoo/igotoo.github.com'
    Configuration file: /Users/igotoo/igotoo.github.com/_config.yml
        Server address: http://127.0.0.1:4000/
      Server running... press ctrl-c to stop.
```  

### 2) github에 온라인 저장소 생성 (기생성으로 생략)
- 구글링 등을 통해 github 회원가입, jekyll fork로 저장소(igotoo.github.com) 및 jekyll blog 기설치
- config.yml 파일 수정, 테마 변경등 만 하고 작업 중지
- 참고

### 3) github 블로그(http://igotoo.github.io) 생성하기
- 기존 작업으로(jekyll fork) 기본적으로 생성된  jekyll 블로그를 없애고 새로 생성
- 블로그 생성 명령 템플릿
    ```
    git init
    git remote add origin 저장소URL
    git add .
    git commit -m "Initialize blog"
    git push origin master
    ```
- "저장소URL" 의미를 정확히 파악하지 못해 계속 에러 발생
  * 저장소 이름(igotoo.github.com)으로 시도
  ```
  git init
  411  git remote add orign igotoo.github.com
  412  git add .
  413  git commit -m "Initialize blog"
  414  git push origin master
  ```
    **---> 에러 발생**
  ```
  430  git init
  431  git remote add origin http://igotoo.github.com
  432  git remote remove  origin http://igotoo.github.com
  433  git remote remove  origin
  434  git push origin master
  ```
    **---> 에러 발생**
  * 블로그 URL(igotoo.github.io)로 시도
  ```
  435  git init
  436  git remote remove  origin
  437  git remote add origin igotoo.github.io
  438  git add .
  439  git commit -m "Initialize blog"
  440  git push origin master
  ```
    **---> 에러 발생**
  * github url(http://github.com/igotoo) 시도
  ```
  447  git init
  448  git remote add origin http://github.com/igotoo
  449  git remote remove origin
  450  git remote add origin http://github.com/igotoo
  451  git add .
  452  git commit -m "Initialize blog"
  453  git push origin master
  ```
  **---> 에러 발생**
  * 저장소 url(https://github.com/igotoo/igotoo.github.com.git) 시도
  ```
  463  git init
  465  git remote remove origin
  466  git remote add origin https://github.com/igotoo/igotoo.github.com.git
  467  git add .
  468  git commit -m "Initialize blog"
  ```     
  **--> 성공**
- 정리
* 블로그 URL : https://igotoo.github.io
* 저장소 이름 : igotoo.github.com
* 저장소 URL : https://github.com/igotoo/igotoo.github.com.git ([참고 - Which remote URL should I use?](https://help.github.com/articles/which-remote-url-should-i-use/))

### 3. 프로젝트 주소 페이지
- 프로젝트 주소 페이지 ?
- 계정주소로 생성해서 생략
### 4. 필수 엔진 설치
- 마크다운 프로세싱 엔진, 문법 하일라이터 설치 <- 왜 설치하는 거지

1) 마크다운 프로세싱 엔진 설치
   GitHub에서는 2016년 5월 1일부터 kramdown 하나만 지원
   ```
   iMac:~ igotoo$ gem install kramdown
   ```
2) Pygments(Pygments는 파이썬 기반 문법 하일라이터이며, 코드를 이쁘게 보여준다) 설치 -> Rouge로 통합되어 Rouge 설치
    ```
    iMac:~ igotoo$ sudo easy_install Rouge
    ```
### 5. 블로그 포스팅

### 에필로그
