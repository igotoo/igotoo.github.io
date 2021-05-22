---
layout: post
title: "GitHub 블로그 재 정비"
date: 2021-05-20 00:14:10 +0900
categories: jekyll, github
---
[TOC]

## 시작 

오랫만에 오픈소스를 활용한 프로젝트에 참여하게 되어 윈도우 터미널을 재사용하게 되면서 참고한  '서비큐라 기술 블로그' 의 내용도 좋고 선호하는 디자인이라. 4년전에 몇달 쓰다가 그만둔 github 블로그를 정비하여 기술 전용 블로그로 만들기로 함(얼마나 갈지? ...)

- 영감을 준 블로그 글 : [2016년 블로그 회고 (subicura.com)](https://subicura.com/2016/12/31/remember-2016.html)

- mediator  : [dirkfabisch/mediator: a medium inspired jekyll theme (github.com)](https://github.com/dirkfabisch/mediator)

  > A medium inspired Jekyll blog theme. The basic idea came from the Ghost theme [Readium 2.0](http://www.svenread.com/readium-ghost-theme/). I use mediator on my own blog [The Base](http://blog.base68.com/).

- mediator 설치 환경 (windows, osx에서도 가능)

  - wsl2  - ubuntu in Windows 10 

    ```bash
    > lsb_release -a
    No LSB modules are available.
    Distributor ID: Ubuntu
    Description:    Ubuntu 20.04.2 LTS
    Release:        20.04
    Codename:       focal
    ```

     

### github blog 생성(테마변경) 요약

- 생성(테마 변경) 절차 

  1. mediator github fork  
  2. 로컬(PC) 디렉토리에 clone 
  3. 필요 gem파일 설치 
  4.  jekyll 서버 실행 정상 설치 여부 점검 
  5.  블로그 포스트 작성 
  6. git add > commit > push 
  7. custom domain 설정 (추후 추가)

  > - [Fork this repository](https://github.com/dirkfabisch/mediator)
  > - Clone it: `git clone https://github.com/YOUR-USER/mediator`
  > - Install the requried gems ([GitHub Pages](https://github.com/github/pages-gem), [Bourbon](https://github.com/thoughtbot/bourbon) and [Jekyll](https://github.com/jekyll/jekyll), [Jemoji](https://github.com/jekyll/jemoji)): `bundle install`
  > - Run the jekyll server: `bundle exec jekyll serve`
  >
  > You should have a server up and running locally at [http://localhost:4000](http://localhost:4000/)

- 사전 준비 필요 사항 : github 가입, wsl , ubuntu 등 리눅스 배포판, git 설치   

- 기존 블로그 igotoo.github.com -> igotoo.github.io으로 테마와 함께변경

## Fork

[dirkfabisch/mediator: a medium inspired jekyll theme (github.com)](https://github.com/dirkfabisch/mediator) 에서 우측상단 포크 버튼 클릭

![image-20210519191904785](/assets/images/image-20210519191904785.png)

### fork 란?

남의 것을 복제해서 내것으로 만든다. 원본과 복제된 것이 연결되어 남이 업데이트 하면  내것도 업데이트 된다. 

>fork는 다른 사람의 Github repository에서 내가 어떤 부분을 수정하거나 추가 기능을 넣고 싶을 때 해당 respository를 내 Github repository로 그대로 복제하는 기능이다. fork한 저장소는 원본(다른 사람의 github repository)와 연결되어 있다. 여기서 연결 되어 있다는 의미는 original repository에 어떤 변화가 생기면(새로운 commit) 이는 그대로 forked된 repository로 반영할 수 있다. 이 때 fetch나 rebase의 과정이 필요하다.
>
>![img](/assets/images/gitfork.png)
>
>[Forking a Repository - How to Use Git and GitHub](https://youtu.be/D2j0zebizdw) 내용을 참고했습니다.
>
>출처 : [Git fork와 clone 의 차이점 (velog.io)](https://velog.io/@imacoolgirlyo/Git-fork와-clone-의-차이점-5sjuhwfzgp)

## 블로그 디렉토리 생성 및  git clone

- git clone https://github.com/igotoo/mediator

```bash
/mnt/d/
> mkdir Blog
> cd Blog
> git clone https://github.com/igotoo/mediator
Cloning into 'mediator'...
remote: Enumerating objects: 494, done.
remote: Total 494 (delta 0), reused 0 (delta 0), pack-reused 494
Receiving objects: 100% (494/494), 16.48 MiB | 11.59 MiB/s, done.
Resolving deltas: 100% (167/167), done.
Updating files: 100% (114/114), done.
```

## 필요 gems 설치 

### ruby 설치 

- sudo apt-get install ruby-full

```bash
> sudo apt-get install ruby-full
[sudo] password for igotoo:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required:
  ...
Preparing to unpack .../3-ri_1%3a2.7+1_all.deb ...
 ...
> ruby -v
ruby 2.7.0p0 (2019-12-25 revision 647ee6f091) [x86_64-linux-gnu]
/mnt/d/Blog/mediator
```

### gem update

- root 권한으로 업데이트 필요 : sudo gem update bundler

```bash
/mnt/d/Blog/mediator master 
> gem update bundler
Updating installed gems
Updating bundler
Fetching bundler-2.2.17.gem
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /var/lib/gems/2.7.0 directory.
> sudo gem update bundler
Updating installed gems
Updating bundler
Fetching bundler-2.2.17.gem
Successfully installed bundler-2.2.17
Parsing documentation for bundler-2.2.17
Installing ri documentation for bundler-2.2.17
Installing darkfish documentation for bundler-2.2.17
Done installing documentation for bundler after 3 seconds
Parsing documentation for bundler-2.2.17
Done installing documentation for bundler after 1 seconds
Gems updated: bundler
```

### gemfile 설치

- 설치할 라이브러리 (gemfile)
  - [GitHub Pages](https://github.com/github/pages-gem) : A simple Ruby Gem to bootstrap dependencies for setting up and maintaining a local Jekyll environment in sync with GitHub Pages.
  - [Bourbon](https://github.com/thoughtbot/bourbon) :   library of [Sass](http://sass-lang.com/) mixins and functions that are designed to make you a more efficient style sheet author.
  - [Jekyll](https://github.com/jekyll/jekyll) : Jekyll is a simple, blog-aware, static site generator perfect for personal, project, or organization sites. 
  - [Jemoji](https://github.com/jekyll/jemoji) : GitHub-flavored Emoji plugin for Jekyll

```bash
> cat Gemfile
source 'https://rubygems.org'

# 'github-pages' includes 'jekyll' gem
gem 'github-pages'
gem 'bourbon'
gem 'jemoji'%
/mnt/d/Blog/mediator master                                                                                                      19:56:51
```

- build-essential 설치 (기 설치시 Skip) : sudo apt-get install build-essential

  - 참고 : [ruby - Install gem gives "Failed to build gem native extension." - Stack Overflow](https://stackoverflow.com/questions/33201630/install-gem-gives-failed-to-build-gem-native-extension)

  - build-essential

    > **build-essential** 은 소스코드 빌드 시 필요한 기본적인 패키지들을 다운로드 합니다.
    >
    > 설치 후에는 gcc, g++, make, perl 등과 각종 라이브러리들이 설치됩니다.
    >
    > 출처 : [build-essential (linux-command.org)](http://linux-command.org/ko/build-essential.html)
  
  ```bash
  > sudo apt-get install build-essential
  [sudo] password for igotoo:
  Reading package lists... Done
  Building dependency tree
  Reading state information... Done
  The following packages were automatically installed and are no longer required:
  :
  
  ```
  
  - build tool이 설치되지 않았을 경우 아래와 같은 에러 발생 할 수 있음
  
  ```bash
  Gem::Ext::BuildError: ERROR: Failed to build gem native extension.
  
  An error occurred while installing commonmarker (0.17.13), and Bundler cannot continue.
  Make sure that `gem install commonmarker -v '0.17.13' --source 'https://rubygems.org/'` succeeds before bundling.
  
  ```
  
- 설치 : bundle install

  ```bash
  > bundle install
  Fetching gem metadata from https://rubygems.org/...........
  Resolving dependencies....
  Using concurrent-ruby 1.1.8
  Using minitest 5.14.4
  Using thread_safe 0.3.6
  Using zeitwerk 2.4.2
  Using public_suffix 4.0.6
  Following files may not be writable, so sudo is needed:
    /usr/local/bin
    /var/lib/gems/2.7.0
    /var/lib/gems/2.7.0/build_info
    /var/lib/gems/2.7.0/cache
    /var/lib/gems/2.7.0/doc
    /var/lib/gems/2.7.0/extensions
    /var/lib/gems/2.7.0/gems
    /var/lib/gems/2.7.0/specifications
  Using execjs 2.8.1
  Using colorator 1.1.0
  Using thor 1.1.0
  Using bundler 2.2.17
  Using faraday-excon 1.1.0
  Using faraday-net_http 1.0.1
  Using faraday-net_http_persistent 1.1.0
  Using forwardable-extended 2.6.0
  Using ruby2_keywords 0.0.4
  Using gemoji 3.0.1
  Using rb-fsevent 0.11.0
  Using rexml 3.2.5
  Using liquid 4.0.3
  Using rouge 3.26.0
  Using safe_yaml 1.0.5
  Using multipart-post 2.1.1
  Using jekyll-paginate 1.1.0
  Using rubyzip 2.3.0
  Using jekyll-swiss 1.0.0
  Using mercenary 0.3.6
  Using i18n 0.9.5
  Using unicode-display_width 1.7.0
  Fetching http_parser.rb 0.6.0
  Fetching eventmachine 1.2.7
  Using tzinfo 1.2.9
  Using bourbon 7.0.0
  Using kramdown 2.3.1
  Using pathutil 0.16.2
  Using faraday 1.4.1
  Using ruby-enum 0.9.0
  Using terminal-table 1.8.0
  Using activesupport 6.0.3.7
  Using kramdown-parser-gfm 1.1.0
  Using coffee-script-source 1.11.1
  Using addressable 2.7.0
  Using coffee-script 2.4.1
  Using sawyer 0.8.2
  Using jekyll-coffeescript 1.1.1
  Using octokit 4.21.0
  Fetching ffi 1.15.0
  Using jekyll-gist 1.5.0
  Fetching unf_ext 0.0.7.7
  Fetching commonmarker 0.17.13
  Fetching racc 1.5.2
  
  
  Your user account isn't allowed to install to the system RubyGems.
    You can cancel this installation and run:
  
        bundle config set --local path 'vendor/bundle'
        bundle install
  
    to install the gems into ./vendor/bundle/, or you can enter your password
    and install the bundled gems to RubyGems using sudo.
  
    Password:
  Installing http_parser.rb 0.6.0 with native extensions
  Installing commonmarker 0.17.13 with native extensions
  Installing eventmachine 1.2.7 with native extensions
  Installing unf_ext 0.0.7.7 with native extensions
  Installing racc 1.5.2 with native extensions
  Installing ffi 1.15.0 with native extensions
  Using unf 0.1.4
  Fetching simpleidn 0.2.1
  Installing simpleidn 0.2.1
  Fetching ethon 0.14.0
  Fetching rb-inotify 0.10.1
  Fetching nokogiri 1.11.4 (x86_64-linux)
  Fetching dnsruby 1.61.5
  Fetching em-websocket 0.5.2
  Installing rb-inotify 0.10.1
  Installing ethon 0.14.0
  Installing em-websocket 0.5.2
  Installing dnsruby 1.61.5
  Fetching sass-listen 4.0.0
  Fetching listen 3.5.1
  Fetching typhoeus 1.4.0
  Installing sass-listen 4.0.0
  Installing listen 3.5.1
  Installing typhoeus 1.4.0
  Fetching sass 3.7.4
  Fetching jekyll-watch 2.2.1
  Installing nokogiri 1.11.4 (x86_64-linux)
  Fetching github-pages-health-check 1.17.0
  Installing jekyll-watch 2.2.1
  Installing sass 3.7.4
  Installing github-pages-health-check 1.17.0
  Fetching jekyll-sass-converter 1.5.2
  Fetching html-pipeline 2.14.0
  Installing jekyll-sass-converter 1.5.2
  Fetching jekyll 3.9.0
  Installing html-pipeline 2.14.0
  Installing jekyll 3.9.0
  Fetching jekyll-feed 0.15.1
  Fetching jekyll-mentions 1.6.0
  Fetching jekyll-default-layout 0.1.4
  Fetching jekyll-github-metadata 2.13.0
  Fetching jekyll-optional-front-matter 0.3.2
  Fetching jekyll-readme-index 0.3.0
  Fetching jekyll-commonmark 1.3.1
  Fetching jekyll-avatar 0.7.0
  Installing jekyll-feed 0.15.1
  Installing jekyll-commonmark 1.3.1
  Installing jekyll-optional-front-matter 0.3.2
  Installing jekyll-readme-index 0.3.0
  Installing jekyll-default-layout 0.1.4
  Installing jekyll-github-metadata 2.13.0
  Installing jekyll-mentions 1.6.0
  Installing jekyll-avatar 0.7.0
  Fetching jekyll-redirect-from 0.16.0
  Fetching jekyll-relative-links 0.6.1
  Fetching jekyll-remote-theme 0.4.3
  Fetching jekyll-seo-tag 2.7.1
  Fetching jekyll-sitemap 1.4.0
  Fetching jekyll-titles-from-headings 0.5.3
  Fetching jemoji 0.12.0
  Installing jekyll-redirect-from 0.16.0
  Installing jekyll-relative-links 0.6.1
  Installing jekyll-remote-theme 0.4.3
  Fetching jekyll-commonmark-ghpages 0.1.6
  Installing jekyll-seo-tag 2.7.1
  Installing jekyll-titles-from-headings 0.5.3
  Installing jemoji 0.12.0
  Installing jekyll-sitemap 1.4.0
  Installing jekyll-commonmark-ghpages 0.1.6
  Fetching jekyll-theme-dinky 0.1.1
  Fetching jekyll-theme-merlot 0.1.1
  Fetching jekyll-theme-hacker 0.1.2
  Fetching jekyll-theme-architect 0.1.1
  Fetching jekyll-theme-cayman 0.1.1
  Fetching jekyll-theme-leap-day 0.1.1
  Fetching jekyll-theme-midnight 0.1.1
  Fetching jekyll-theme-minimal 0.1.1
  Installing jekyll-theme-dinky 0.1.1
  Installing jekyll-theme-cayman 0.1.1
  Installing jekyll-theme-hacker 0.1.2
  Installing jekyll-theme-architect 0.1.1
  Installing jekyll-theme-merlot 0.1.1
  Fetching jekyll-theme-modernist 0.1.1
  Installing jekyll-theme-minimal 0.1.1
  Fetching jekyll-theme-primer 0.5.4
  Fetching jekyll-theme-slate 0.1.1
  Fetching jekyll-theme-tactile 0.1.1
  Installing jekyll-theme-midnight 0.1.1
  Installing jekyll-theme-leap-day 0.1.1
  Installing jekyll-theme-modernist 0.1.1
  Installing jekyll-theme-slate 0.1.1
  Installing jekyll-theme-primer 0.5.4
  Installing jekyll-theme-tactile 0.1.1
  Fetching jekyll-theme-time-machine 0.1.1
  Fetching minima 2.5.1
  Installing jekyll-theme-time-machine 0.1.1
  Installing minima 2.5.1
  Fetching github-pages 214
  Installing github-pages 214
  Bundle complete! 3 Gemfile dependencies, 96 gems now installed.
  Use `bundle info [gemname]` to see where a bundled gem is installed.
  Post-install message from dnsruby:
  Installing dnsruby...
    For issues and source code: https://github.com/alexdalitz/dnsruby
    For general discussion (please tell us how you use dnsruby): https://groups.google.com/forum/#!forum/dnsruby
  Post-install message from sass:
  
  Ruby Sass has reached end-of-life and should no longer be used.
  
  * If you use Sass as a command-line tool, we recommend using Dart Sass, the new
    primary implementation: https://sass-lang.com/install
  
  * If you use Sass as a plug-in for a Ruby web framework, we recommend using the
    sassc gem: https://github.com/sass/sassc-ruby#readme
  
  * For more details, please refer to the Sass blog:
    https://sass-lang.com/blog/posts/7828841
  
  Post-install message from html-pipeline:
  -------------------------------------------------
  Thank you for installing html-pipeline!
  You must bundle Filter gem dependencies.
  See html-pipeline README.md for more details.
  https://github.com/jch/html-pipeline#dependencies
  -------------------------------------------------
  /mnt/d/Blog/mediator master ?1                                                                                               46s 21:24:38
  ```

   

## jekyll server 실행

### bundle exec jekyll server

```bash
> bundle exec jekyll serve
Configuration file: /mnt/d/Blog/mediator/_config.yml
       Deprecation: The 'gems' configuration option has been renamed to 'plugins'. Please update your config file accordingly.
            Source: /mnt/d/Blog/mediator
       Destination: /mnt/d/Blog/mediator/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
    Liquid Warning: Liquid syntax error (line 23): Unexpected character # in "{{#foreach tags}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 23): Unexpected character # in "{{#if @first}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 23): Unexpected character / in "{{/if}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 23): Unexpected character / in "{{/foreach}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character # in "{{#foreach tags}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character # in "{{#if @first}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character / in "{{/if}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character / in "{{/foreach}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 77): Unexpected character / in "{{/post}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 84): Unexpected character @ in "{{@blog.url}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 23): Unexpected character # in "{{#foreach tags}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 23): Unexpected character # in "{{#if @first}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 23): Unexpected character / in "{{/if}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 23): Unexpected character / in "{{/foreach}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character # in "{{#foreach tags}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character # in "{{#if @first}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character / in "{{/if}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 39): Unexpected character / in "{{/foreach}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 77): Unexpected character / in "{{/post}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 84): Unexpected character @ in "{{@blog.url}}" in /_layouts/post.html
    Liquid Warning: Liquid syntax error (line 44): Unexpected character # in "{{#foreach tags}}" in index.html
    Liquid Warning: Liquid syntax error (line 44): Unexpected character # in "{{#if @first}}" in index.html
    Liquid Warning: Liquid syntax error (line 44): Unexpected character / in "{{/if}}" in index.html
    Liquid Warning: Liquid syntax error (line 44): Unexpected character / in "{{/foreach}}" in index.html
    Liquid Warning: Liquid syntax error (line 66): Unexpected character # in "{{#foreach tags}}" in index.html
    Liquid Warning: Liquid syntax error (line 66): Unexpected character # in "{{#if @first}}" in index.html
    Liquid Warning: Liquid syntax error (line 66): Unexpected character / in "{{/if}}" in index.html
    Liquid Warning: Liquid syntax error (line 66): Unexpected character / in "{{/foreach}}" in index.html
    Liquid Warning: Liquid syntax error (line 88): Unexpected character ! in "{{!! After all the posts, we have the previous/next pagination links }}" in index.html
                    done in 4.994 seconds.
/var/lib/gems/2.7.0/gems/pathutil-0.16.2/lib/pathutil.rb:502: warning: Using the last argument as keyword parameters is deprecated
                    Auto-regeneration may not work on some Windows versions.
                    Please see: https://github.com/Microsoft/BashOnWindows/issues/216
                    If it does not work, please upgrade Bash on Windows or run Jekyll with --no-watch.
 Auto-regeneration: enabled for '/mnt/d/Blog/mediator'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

```

![image-20210519215454781](/assets/images/image-20210519215454781.png)

## 블로그 게시하기

기존에 jeykll로 만든 블로그가 있어서 삭제후 다시 만들기로 함

참고 : [Github 블로그 만들기 (1)](https://velog.io/@zawook/Github-블로그-만들기-1), [Github 블로그 만들기 (2) (velog.io)](https://velog.io/@zawook/Github-블로그-만들기-2)

```bash
> git init
Reinitialized existing Git repository in /mnt/d/Blog/mediator/.git/
> ls -al
total 36
drwxrwxrwx 1 igotoo igotoo  512 May 19 21:49 .
drwxrwxrwx 1 igotoo igotoo  512 May 19 22:35 ..
drwxrwxrwx 1 igotoo igotoo  512 May 19 23:39 .git
-rwxrwxrwx 1 igotoo igotoo   27 May 19 19:40 .gitignore
drwxrwxrwx 1 igotoo igotoo  512 May 19 21:49 .sass-cache
-rwxrwxrwx 1 igotoo igotoo  116 May 19 19:40 Gemfile
-rwxrwxrwx 1 igotoo igotoo 7483 May 19 21:24 Gemfile.lock
-rwxrwxrwx 1 igotoo igotoo 1119 May 19 19:40 LICENCE
-rwxrwxrwx 1 igotoo igotoo 3131 May 19 19:40 README.md
-rwxrwxrwx 1 igotoo igotoo 1568 May 19 22:02 _config.yml
drwxrwxrwx 1 igotoo igotoo  512 May 19 19:40 _includes
drwxrwxrwx 1 igotoo igotoo  512 May 19 19:40 _layouts
drwxrwxrwx 1 igotoo igotoo  512 May 19 22:42 _posts
drwxrwxrwx 1 igotoo igotoo  512 May 19 19:40 _sass
drwxrwxrwx 1 igotoo igotoo  512 May 19 23:19 _site
-rwxrwxrwx 1 igotoo igotoo  761 May 19 19:40 about.md
drwxrwxrwx 1 igotoo igotoo  512 May 19 19:40 assets
drwxrwxrwx 1 igotoo igotoo  512 May 19 19:40 css
-rwxrwxrwx 1 igotoo igotoo 1150 May 19 19:40 favicon.ico
-rwxrwxrwx 1 igotoo igotoo 1292 May 19 19:40 feed.xml
-rwxrwxrwx 1 igotoo igotoo 4065 May 19 19:40 index.html

> git commit -m "first commit"

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: empty ident name (for <igotoo@jb-won001.samsungsds-ad.net>) not allowed
> git config --global user.email "igotoo@gmail.com"
> git config --global user.name "igotoo"
> git commit -m "first commit"
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   _config.yml
        deleted:    _posts/2014-08-29-welcome-to-jekyll.markdown
        modified:   assets/images/author.jpg

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Gemfile.lock
        _posts/2017-03-19-sublimetext-setting.md
        _posts/2017-03-24-ST3-Markdown-install.md
        _posts/2017-03-26-RasberryPi-Rasbrian-intall.md
        _posts/2017-03-28-Vagrant1.md
        _posts/2017-04-14-AtomEditor1.md
        _posts/2017-04-15-MakigTorrentbot-1.md
        _posts/2017-04-15-githubblooging-1.md

no changes added to commit (use "git add" and/or "git commit -a")
> git branch -M main
> git remote add origin https://github.com/igotoo/igotoo.github.io.git
fatal: remote origin already exists.
> git remote remove origin
> git remote add origin https://github.com/igotoo/igotoo.github.io.git
> git push -u origin main
Username for 'https://github.com': igotoo@gmail.com
Password for 'https://igotoo@gmail.com@github.com':
Enumerating objects: 494, done.
Counting objects: 100% (494/494), done.
Delta compression using up to 8 threads
Compressing objects: 100% (321/321), done.
Writing objects: 100% (494/494), 16.48 MiB | 5.16 MiB/s, done.
Total 494 (delta 167), reused 494 (delta 167)
remote: Resolving deltas: 100% (167/167), done.
To https://github.com/igotoo/igotoo.github.io.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
/mnt/d/Blog/mediator main !3 ?8                                                                                              32s 23:46:12
>
```

클론 이후 변경된 페이지 반영 안되어  post add 후 다시 시도 

> Changes not staged for commit:
>   (use "git add/rm <file>..." to update what will be committed)

```bash
> git add _posts/*
> git commit -m "second commit"
[main 1c1f115] second commit
 7 files changed, 665 insertions(+)
 create mode 100644 _posts/2017-03-19-sublimetext-setting.md
 create mode 100644 _posts/2017-03-24-ST3-Markdown-install.md
 create mode 100644 _posts/2017-03-26-RasberryPi-Rasbrian-intall.md
 create mode 100644 _posts/2017-03-28-Vagrant1.md
 create mode 100644 _posts/2017-04-14-AtomEditor1.md
 create mode 100644 _posts/2017-04-15-MakigTorrentbot-1.md
 create mode 100644 _posts/2017-04-15-githubblooging-1.md
> git push -u origin main
Username for 'https://github.com': igotoo@gmail.com
Password for 'https://igotoo@gmail.com@github.com':
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 8 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (10/10), 17.34 KiB | 443.00 KiB/s, done.
Total 10 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/igotoo/igotoo.github.io.git
   9a916a5..1c1f115  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
/mnt/d/Blog/mediator main !3 ?1                                                                                              16s 23:51:58
>
```

- 구블로그에서 옮겨온 post 들은 github에 올라 갔으나 ...  블로그 예전거 그대로 임 이를 어찌 변경하나...

- 예전 블로그

![image-20210520000148451](/assets/images/image-20210520000148451.png)

- 예전 블로그 삭제후 404 Not Found Error 발생
  - 원인 : 페이지 소스가 None으로 되어 있었음

    ![image-20210520002914315](/assets/images/image-20210520002914315.png)

  - None 을 Main으로 변경 후 정상적으로 보임

    ![image-20210520003005822](/assets/images/image-20210520003005822.png)


## Custom domain 설정

​	참고 : [블로그 만들기 GitHub 심화 3편 - 커스텀 도메인 (chulgil.me)](https://blog.chulgil.me/how-to-make-blog-using-github-3/), [Configuring a custom domain for your GitHub Pages site - GitHub Docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site) 

- github에서 custom domain를 설정할 수 있는 2가지 (subdomain, apex domain) 중 간단하고 github에서 추천하는 subdomain 방법중 custom subdomain을 적용

  | Supported custom domain type | Example            |
  | :--------------------------- | :----------------- |
  | `www` subdomain              | `www.example.com`  |
  | Custom subdomain             | `blog.example.com` |
  | Apex domain                  | `example.com`      |

  > We recommend always using a `www` subdomain, even if you also use an apex domain. When you create a new site with an apex domain, we automatically attempt to secure the `www` subdomain for use when serving your site's content. If you configure a `www` subdomain, we automatically attempt to secure the associated apex domain.
  >
  > ### [Using a subdomain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages#using-a-subdomain-for-your-github-pages-site)
  >
  > A subdomain is the part of a URL before the root domain. You can configure your subdomain as `www` or as a distinct section of your site, like `blog.example.com`.
  >
  > Subdomains are configured with a `CNAME` record through your DNS provider.
  >
  > #### [`www` subdomains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages#www-subdomains)
  >
  > A `www` subdomain is the most commonly used type of subdomain. For example, `www.example.com` includes a `www` subdomain.
  >
  > `www` subdomains are the most stable type of custom domain because `www` subdomains are not affected by changes to the IP addresses of GitHub's servers.
  >
  > #### [Custom subdomains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages#custom-subdomains)
  >
  > A custom subdomain is a type of subdomain that doesn't use the standard `www` variant. Custom subdomains are mostly used when you want two distinct sections of your site. For example, you can create a site called `blog.example.com` and customize that section independently from `www.example.com`.
  >
  > ### [Using an apex domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages#using-an-apex-domain-for-your-github-pages-site)
  >
  > An apex domain is a custom domain that does not contain a subdomain, such as `example.com`. Apex domains are also known as base, bare, naked, root apex, or zone apex domains.
  >
  > An apex domain is configured with an `A`, `ALIAS`, or `ANAME` record through your DNS provider.

- 구글 도메인에서 cname 설정

  - blg.igoto.pw 가 igotoo.github.io로 리다이렉트 할 수 있도록 도메인 별명 즉 cname을 설정 

![image-20210522220538951](/assets/images/image-20210522220538951.png)

- Github pages  Custom domain 설정

![image-20210522220312683](/assets/images/image-20210522220312683.png)

- DNS 정보 확인

```bash
> dig blg.igotoo.pw +nostats +nocomments +nocmd
;blg.igotoo.pw.                 IN      A
blg.igotoo.pw.          0       IN      CNAME   igotoo.github.io.
igotoo.github.io.       0       IN      A       185.199.110.153
igotoo.github.io.       0       IN      A       185.199.108.153
igotoo.github.io.       0       IN      A       185.199.111.153
igotoo.github.io.       0       IN      A       185.199.109.153
dns1.p05.nsone.net.     0       IN      A       198.51.44.5
dns2.p05.nsone.net.     0       IN      A       198.51.45.5
dns3.p05.nsone.net.     0       IN      A       198.51.44.69
dns4.p05.nsone.net.     0       IN      A       198.51.45.69
ns-393.awsdns-49.com.   0       IN      A       205.251.193.137
ns-692.awsdns-22.net.   0       IN      A       205.251.194.180
ns-1339.awsdns-39.org.  0       IN      A       205.251.197.59
ns-1622.awsdns-10.co.uk. 0      IN      A       205.251.198.86
dns1.p05.nsone.net.     0       IN      AAAA    2620:4d:4000:6259:7:5:0:1
```

- git pull

  > If you use a static site generator to build your site locally and push the generated files to GitHub, pull the commit that added the *CNAME* file to your local repository. 

  - custom domain 생성시 github에서 자동으로 CNAME 파일을 생성하고 commit을 하므로 로컬 PC에 변경 사항을 적용하기 위해 필요 

    ```bash
    > git pull
    remote: Enumerating objects: 8, done.
    remote: Counting objects: 100% (8/8), done.
    remote: Compressing objects: 100% (5/5), done.
    remote: Total 7 (delta 2), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (7/7), 644 bytes | 7.00 KiB/s, done.
    From https://github.com/igotoo/igotoo.github.io
       1dd236d..3e6334a  main       -> origin/main
    Updating 1dd236d..3e6334a
    Fast-forward
     CNAME | 1 +
     1 file changed, 1 insertion(+)
     create mode 100644 CNAME
    ```

    