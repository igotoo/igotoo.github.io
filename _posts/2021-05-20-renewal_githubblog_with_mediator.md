---
layout: post
title: "GitHub 블로그 재 정비"
date: 2021-05-20 00:14:10 +0900
categories: jekyll, github
---
# GitHub 블로그 재 정비

[TOC]

## 시작 

오랫만에 오픈소스를 활용한 프로젝트에 참여하게 되어 윈도우 터미널을 재사용하게 되면서 참고한  '서비큐라 기술 블로그' 의 내용도 좋고 선호하는 디자인이라. 4년전에 몇달 쓰다가 그만둔 github 블로그를 정비하여 기술 전용 블로그로 만들기로 함(얼마나 갈지? ...)

- 영감을 준 블로그 글 : [2016년 블로그 회고 (subicura.com)](https://subicura.com/2016/12/31/remember-2016.html)

- mediator  : [dirkfabisch/mediator: a medium inspired jekyll theme (github.com)](https://github.com/dirkfabisch/mediator)

  > A medium inspired Jekyll blog theme. The basic idea came from the Ghost theme [Readium 2.0](http://www.svenread.com/readium-ghost-theme/). I use mediator on my own blog [The Base](http://blog.base68.com/).

  

### mediator 설치 순서

>- [Fork this repository](https://github.com/dirkfabisch/mediator)
>- Clone it: `git clone https://github.com/YOUR-USER/mediator`
>- Install the requried gems ([GitHub Pages](https://github.com/github/pages-gem), [Bourbon](https://github.com/thoughtbot/bourbon) and [Jekyll](https://github.com/jekyll/jekyll), [Jemoji](https://github.com/jekyll/jemoji)): `bundle install`
>- Run the jekyll server: `bundle exec jekyll serve`
>
>You should have a server up and running locally at [http://localhost:4000](http://localhost:4000/).

## Fork

[dirkfabisch/mediator: a medium inspired jekyll theme (github.com)](https://github.com/dirkfabisch/mediator) 에서 우측상단 포크 버튼 클릭

![image-20210519191904785](C:\Users\jb.won\AppData\Roaming\Typora\typora-user-images\image-20210519191904785.png)

### fork 란?

남의 것을 복제해서 내것으로 만든다. 원본과 복제된 것이 연결되어 남이 업데이트 하면  내것도 업데이트 된다. 

>fork는 다른 사람의 Github repository에서 내가 어떤 부분을 수정하거나 추가 기능을 넣고 싶을 때 해당 respository를 내 Github repository로 그대로 복제하는 기능이다. fork한 저장소는 원본(다른 사람의 github repository)와 연결되어 있다. 여기서 연결 되어 있다는 의미는 original repository에 어떤 변화가 생기면(새로운 commit) 이는 그대로 forked된 repository로 반영할 수 있다. 이 때 fetch나 rebase의 과정이 필요하다.
>
>![img](https://media.vlpt.us/post-images/imacoolgirlyo/cbe5ca40-5f44-11e9-88b2-25d00148b532/gitfork.png)
>
>[Forking a Repository - How to Use Git and GitHub](https://youtu.be/D2j0zebizdw) 내용을 참고했습니다.
>
>출처 : [Git fork와 clone 의 차이점 (velog.io)](https://velog.io/@imacoolgirlyo/Git-fork와-clone-의-차이점-5sjuhwfzgp)

## 블로그 디렉토리 생성 및  git clone

```bash
/mnt/d/
> mkdir Blog
> cd Blog
> git clone https://github.com/igotoo/mediator
Cloning into 'mediator'...
fatal: unable to access 'https://github.com/igotoo/mediator/': Failed to connect to 70.10.15.10 port 8080: Connection timed out
> export http_proxy=
> export https_proxy=
> git clone https://github.com/igotoo/mediator
Cloning into 'mediator'...
remote: Enumerating objects: 494, done.
remote: Total 494 (delta 0), reused 0 (delta 0), pack-reused 494
Receiving objects: 100% (494/494), 16.48 MiB | 11.59 MiB/s, done.
Resolving deltas: 100% (167/167), done.
Updating files: 100% (114/114), done.
```

## 필요 gems 설치 

어찌 설치하라는 건지  모르겠다....

### ruby 설치

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

- root 권한으로 업데이트 필요

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
>
```

- 어마어마한 에러 ... 모 어쩌라는 거지

```bash
> bundle install
Fetching gem metadata from https://rubygems.org/............
Resolving dependencies....
Using bundler 2.2.17
Following files may not be writable, so sudo is needed:
  /usr/local/bin
  /var/lib/gems/2.7.0
  /var/lib/gems/2.7.0/build_info
  /var/lib/gems/2.7.0/cache
  /var/lib/gems/2.7.0/doc
  /var/lib/gems/2.7.0/extensions
  /var/lib/gems/2.7.0/gems
  /var/lib/gems/2.7.0/specifications
Fetching zeitwerk 2.4.2
Fetching public_suffix 4.0.6
Fetching coffee-script-source 1.11.1
Fetching concurrent-ruby 1.1.8
Fetching thread_safe 0.3.6
Fetching thor 1.1.0
Fetching minitest 5.14.4
Fetching execjs 2.8.1


Your user account isn't allowed to install to the system RubyGems.
  You can cancel this installation and run:

      bundle config set --local path 'vendor/bundle'
      bundle install

  to install the gems into ./vendor/bundle/, or you can enter your password
  and install the bundled gems to RubyGems using sudo.

  Password:
Installing execjs 2.8.1
Installing zeitwerk 2.4.2
Installing thor 1.1.0
Installing coffee-script-source 1.11.1
Installing minitest 5.14.4
Installing thread_safe 0.3.6
Installing public_suffix 4.0.6
Fetching colorator 1.1.0
Fetching unf_ext 0.0.7.7
Fetching eventmachine 1.2.7
Installing concurrent-ruby 1.1.8
Fetching http_parser.rb 0.6.0
Fetching ffi 1.15.0
Fetching faraday-excon 1.1.0
Fetching faraday-net_http 1.0.1
Installing colorator 1.1.0
Installing faraday-net_http 1.0.1
Installing eventmachine 1.2.7 with native extensions
Fetching faraday-net_http_persistent 1.1.0
Installing unf_ext 0.0.7.7 with native extensions
Installing http_parser.rb 0.6.0 with native extensions
Fetching multipart-post 2.1.1
Installing faraday-net_http_persistent 1.1.0
Fetching ruby2_keywords 0.0.4
Installing faraday-excon 1.1.0
Installing ruby2_keywords 0.0.4
Installing multipart-post 2.1.1
Fetching forwardable-extended 2.6.0
Fetching gemoji 3.0.1
Fetching rb-fsevent 0.11.0
Installing ffi 1.15.0 with native extensions
Installing forwardable-extended 2.6.0
Fetching rexml 3.2.5
Installing gemoji 3.0.1
Installing rb-fsevent 0.11.0
Fetching liquid 4.0.3
Installing rexml 3.2.5
Fetching mercenary 0.3.6
Installing liquid 4.0.3
Installing mercenary 0.3.6
Fetching rouge 3.26.0
Fetching safe_yaml 1.0.5
Fetching racc 1.5.2
Installing safe_yaml 1.0.5
Fetching jekyll-paginate 1.1.0
Fetching rubyzip 2.3.0
Fetching jekyll-swiss 1.0.0
Installing jekyll-paginate 1.1.0
Installing racc 1.5.2 with native extensions
Installing jekyll-swiss 1.0.0
Installing rouge 3.26.0
Installing rubyzip 2.3.0
Fetching unicode-display_width 1.7.0
Fetching coffee-script 2.4.1
Fetching bourbon 7.0.0
Installing coffee-script 2.4.1
Installing unicode-display_width 1.7.0
Installing bourbon 7.0.0
Fetching addressable 2.7.0
Fetching tzinfo 1.2.9
Fetching i18n 0.9.5
Fetching faraday 1.4.1
Installing addressable 2.7.0
Installing i18n 0.9.5
Installing faraday 1.4.1
Installing tzinfo 1.2.9
Fetching pathutil 0.16.2
Installing pathutil 0.16.2
Fetching kramdown 2.3.1
Fetching jekyll-coffeescript 1.1.1
Fetching terminal-table 1.8.0
Fetching ruby-enum 0.9.0
Installing jekyll-coffeescript 1.1.1
Installing kramdown 2.3.1
Installing terminal-table 1.8.0
Fetching sawyer 0.8.2
Fetching activesupport 6.0.3.7
Installing ruby-enum 0.9.0
Installing sawyer 0.8.2
Fetching octokit 4.21.0
Installing activesupport 6.0.3.7
Installing octokit 4.21.0
Fetching commonmarker 0.17.13
Installing commonmarker 0.17.13 with native extensions
Fetching jekyll-gist 1.5.0
Installing jekyll-gist 1.5.0
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /tmp/bundler20210519-615-rvrpwpcommonmarker-0.17.13/gems/commonmarker-0.17.13/ext/commonmarker
/usr/bin/ruby2.7 -I /usr/lib/ruby/2.7.0 -r ./siteconf20210519-615-qzx91l.rb extconf.rb
creating Makefile

current directory: /tmp/bundler20210519-615-rvrpwpcommonmarker-0.17.13/gems/commonmarker-0.17.13/ext/commonmarker
make "DESTDIR=" clean
sh: 1: make: not found

current directory: /tmp/bundler20210519-615-rvrpwpcommonmarker-0.17.13/gems/commonmarker-0.17.13/ext/commonmarker
make "DESTDIR="
sh: 1: make: not found

make failed, exit code 127

Gem files will remain installed in /tmp/bundler20210519-615-rvrpwpcommonmarker-0.17.13/gems/commonmarker-0.17.13 for inspection.
Results logged to /tmp/bundler20210519-615-rvrpwpcommonmarker-0.17.13/extensions/x86_64-linux/2.7.0/commonmarker-0.17.13/gem_make.out

An error occurred while installing commonmarker (0.17.13), and Bundler cannot continue.
Make sure that `gem install commonmarker -v '0.17.13' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  github-pages was resolved to 214, which depends on
    jekyll-commonmark-ghpages was resolved to 0.1.6, which depends on
      jekyll-commonmark was resolved to 1.3.1, which depends on
        commonmarker


Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /tmp/bundler20210519-615-yl1uz6unf_ext-0.0.7.7/gems/unf_ext-0.0.7.7/ext/unf_ext
/usr/bin/ruby2.7 -I /usr/lib/ruby/2.7.0 -r ./siteconf20210519-615-rt2zli.rb extconf.rb
checking for -lstdc++... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
        --with-opt-dir
        --without-opt-dir
        --with-opt-include
        --without-opt-include=${opt-dir}/include
        --with-opt-lib
        --without-opt-lib=${opt-dir}/lib
        --with-make-prog
        --without-make-prog
        --srcdir=.
        --curdir
        --ruby=/usr/bin/$(RUBY_BASE_NAME)2.7
        --with-static-libstdc++
        --without-static-libstdc++
        --with-stdc++-dir
        --without-stdc++-dir
        --with-stdc++-include
        --without-stdc++-include=${stdc++-dir}/include
        --with-stdc++-lib
        --without-stdc++-lib=${stdc++-dir}/lib
        --with-stdc++lib
        --without-stdc++lib
/usr/lib/ruby/2.7.0/mkmf.rb:471:in `try_do': The compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.
        from /usr/lib/ruby/2.7.0/mkmf.rb:564:in `try_link0'
        from /usr/lib/ruby/2.7.0/mkmf.rb:582:in `try_link'
        from /usr/lib/ruby/2.7.0/mkmf.rb:801:in `try_func'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1029:in `block in have_library'
        from /usr/lib/ruby/2.7.0/mkmf.rb:971:in `block in checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block (2 levels) in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:357:in `postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:970:in `checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1024:in `have_library'
        from extconf.rb:6:in `<main>'

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /tmp/bundler20210519-615-yl1uz6unf_ext-0.0.7.7/extensions/x86_64-linux/2.7.0/unf_ext-0.0.7.7/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /tmp/bundler20210519-615-yl1uz6unf_ext-0.0.7.7/gems/unf_ext-0.0.7.7 for inspection.
Results logged to /tmp/bundler20210519-615-yl1uz6unf_ext-0.0.7.7/extensions/x86_64-linux/2.7.0/unf_ext-0.0.7.7/gem_make.out

An error occurred while installing unf_ext (0.0.7.7), and Bundler cannot continue.
Make sure that `gem install unf_ext -v '0.0.7.7' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  github-pages was resolved to 214, which depends on
    github-pages-health-check was resolved to 1.17.0, which depends on
      dnsruby was resolved to 1.61.5, which depends on
        simpleidn was resolved to 0.2.1, which depends on
          unf was resolved to 0.1.4, which depends on
            unf_ext


Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /tmp/bundler20210519-615-jlypugeventmachine-1.2.7/gems/eventmachine-1.2.7/ext
/usr/bin/ruby2.7 -I /usr/lib/ruby/2.7.0 -r ./siteconf20210519-615-1p5puiu.rb extconf.rb
checking for -lcrypto... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
        --with-opt-dir
        --without-opt-dir
        --with-opt-include
        --without-opt-include=${opt-dir}/include
        --with-opt-lib
        --without-opt-lib=${opt-dir}/lib
        --with-make-prog
        --without-make-prog
        --srcdir=.
        --curdir
        --ruby=/usr/bin/$(RUBY_BASE_NAME)2.7
        --with-ssl-dir
        --without-ssl-dir
        --with-ssl-include
        --without-ssl-include=${ssl-dir}/include
        --with-ssl-lib
        --without-ssl-lib=${ssl-dir}/lib
        --with-openssl-config
        --without-openssl-config
        --with-pkg-config
        --without-pkg-config
        --with-crypto-dir
        --without-crypto-dir
        --with-crypto-include
        --without-crypto-include=${crypto-dir}/include
        --with-crypto-lib
        --without-crypto-lib=${crypto-dir}/lib
        --with-cryptolib
        --without-cryptolib
/usr/lib/ruby/2.7.0/mkmf.rb:471:in `try_do': The compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.
        from /usr/lib/ruby/2.7.0/mkmf.rb:564:in `try_link0'
        from /usr/lib/ruby/2.7.0/mkmf.rb:582:in `try_link'
        from /usr/lib/ruby/2.7.0/mkmf.rb:801:in `try_func'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1029:in `block in have_library'
        from /usr/lib/ruby/2.7.0/mkmf.rb:971:in `block in checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block (2 levels) in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:357:in `postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:970:in `checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1024:in `have_library'
        from extconf.rb:8:in `block in check_libs'
        from extconf.rb:8:in `all?'
        from extconf.rb:8:in `check_libs'
        from extconf.rb:95:in `<main>'

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /tmp/bundler20210519-615-jlypugeventmachine-1.2.7/extensions/x86_64-linux/2.7.0/eventmachine-1.2.7/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /tmp/bundler20210519-615-jlypugeventmachine-1.2.7/gems/eventmachine-1.2.7 for inspection.
Results logged to /tmp/bundler20210519-615-jlypugeventmachine-1.2.7/extensions/x86_64-linux/2.7.0/eventmachine-1.2.7/gem_make.out

An error occurred while installing eventmachine (1.2.7), and Bundler cannot continue.
Make sure that `gem install eventmachine -v '1.2.7' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  github-pages was resolved to 214, which depends on
    jekyll-avatar was resolved to 0.7.0, which depends on
      jekyll was resolved to 3.9.0, which depends on
        em-websocket was resolved to 0.5.2, which depends on
          eventmachine


Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /tmp/bundler20210519-615-fecqaehttp_parser.rb-0.6.0/gems/http_parser.rb-0.6.0/ext/ruby_http_parser
/usr/bin/ruby2.7 -I /usr/lib/ruby/2.7.0 -r ./siteconf20210519-615-14tg968.rb extconf.rb
creating Makefile

current directory: /tmp/bundler20210519-615-fecqaehttp_parser.rb-0.6.0/gems/http_parser.rb-0.6.0/ext/ruby_http_parser
make "DESTDIR=" clean
sh: 1: make: not found

current directory: /tmp/bundler20210519-615-fecqaehttp_parser.rb-0.6.0/gems/http_parser.rb-0.6.0/ext/ruby_http_parser
make "DESTDIR="
sh: 1: make: not found

make failed, exit code 127

Gem files will remain installed in /tmp/bundler20210519-615-fecqaehttp_parser.rb-0.6.0/gems/http_parser.rb-0.6.0 for inspection.
Results logged to /tmp/bundler20210519-615-fecqaehttp_parser.rb-0.6.0/extensions/x86_64-linux/2.7.0/http_parser.rb-0.6.0/gem_make.out

An error occurred while installing http_parser.rb (0.6.0), and Bundler cannot continue.
Make sure that `gem install http_parser.rb -v '0.6.0' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  github-pages was resolved to 214, which depends on
    jekyll-avatar was resolved to 0.7.0, which depends on
      jekyll was resolved to 3.9.0, which depends on
        em-websocket was resolved to 0.5.2, which depends on
          http_parser.rb


Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /tmp/bundler20210519-615-sb9ivmffi-1.15.0/gems/ffi-1.15.0/ext/ffi_c
/usr/bin/ruby2.7 -I /usr/lib/ruby/2.7.0 -r ./siteconf20210519-615-5d0hi7.rb extconf.rb
checking for ffi.h... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
        --with-opt-dir
        --without-opt-dir
        --with-opt-include
        --without-opt-include=${opt-dir}/include
        --with-opt-lib
        --without-opt-lib=${opt-dir}/lib
        --with-make-prog
        --without-make-prog
        --srcdir=.
        --curdir
        --ruby=/usr/bin/$(RUBY_BASE_NAME)2.7
        --with-ffi_c-dir
        --without-ffi_c-dir
        --with-ffi_c-include
        --without-ffi_c-include=${ffi_c-dir}/include
        --with-ffi_c-lib
        --without-ffi_c-lib=${ffi_c-dir}/lib
        --enable-system-libffi
        --disable-system-libffi
        --with-libffi-config
        --without-libffi-config
        --with-pkg-config
        --without-pkg-config
        --with-ffi-dir
        --without-ffi-dir
        --with-ffi-include
        --without-ffi-include=${ffi-dir}/include
        --with-ffi-lib
        --without-ffi-lib=${ffi-dir}/lib
/usr/lib/ruby/2.7.0/mkmf.rb:471:in `try_do': The compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.
        from /usr/lib/ruby/2.7.0/mkmf.rb:613:in `try_cpp'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1124:in `block in have_header'
        from /usr/lib/ruby/2.7.0/mkmf.rb:971:in `block in checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block (2 levels) in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:357:in `postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:970:in `checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1123:in `have_header'
        from extconf.rb:10:in `system_libffi_usable?'
        from extconf.rb:42:in `<main>'

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /tmp/bundler20210519-615-sb9ivmffi-1.15.0/extensions/x86_64-linux/2.7.0/ffi-1.15.0/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /tmp/bundler20210519-615-sb9ivmffi-1.15.0/gems/ffi-1.15.0 for inspection.
Results logged to /tmp/bundler20210519-615-sb9ivmffi-1.15.0/extensions/x86_64-linux/2.7.0/ffi-1.15.0/gem_make.out

An error occurred while installing ffi (1.15.0), and Bundler cannot continue.
Make sure that `gem install ffi -v '1.15.0' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  github-pages was resolved to 214, which depends on
    github-pages-health-check was resolved to 1.17.0, which depends on
      typhoeus was resolved to 1.4.0, which depends on
        ethon was resolved to 0.14.0, which depends on
          ffi


Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /tmp/bundler20210519-615-sakpxjracc-1.5.2/gems/racc-1.5.2/ext/racc/cparse
/usr/bin/ruby2.7 -I /usr/lib/ruby/2.7.0 -r ./siteconf20210519-615-1b1zpm3.rb extconf.rb
checking for rb_ary_subseq()... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
        --with-opt-dir
        --without-opt-dir
        --with-opt-include
        --without-opt-include=${opt-dir}/include
        --with-opt-lib
        --without-opt-lib=${opt-dir}/lib
        --with-make-prog
        --without-make-prog
        --srcdir=.
        --curdir
        --ruby=/usr/bin/$(RUBY_BASE_NAME)2.7
/usr/lib/ruby/2.7.0/mkmf.rb:471:in `try_do': The compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.
        from /usr/lib/ruby/2.7.0/mkmf.rb:564:in `try_link0'
        from /usr/lib/ruby/2.7.0/mkmf.rb:582:in `try_link'
        from /usr/lib/ruby/2.7.0/mkmf.rb:794:in `try_func'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1083:in `block in have_func'
        from /usr/lib/ruby/2.7.0/mkmf.rb:971:in `block in checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block (2 levels) in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:361:in `block in postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:331:in `open'
        from /usr/lib/ruby/2.7.0/mkmf.rb:357:in `postpone'
        from /usr/lib/ruby/2.7.0/mkmf.rb:970:in `checking_for'
        from /usr/lib/ruby/2.7.0/mkmf.rb:1082:in `have_func'
        from extconf.rb:6:in `<main>'

To see why this extension failed to compile, please check the mkmf.log which can be found here:

  /tmp/bundler20210519-615-sakpxjracc-1.5.2/extensions/x86_64-linux/2.7.0/racc-1.5.2/mkmf.log

extconf failed, exit code 1

Gem files will remain installed in /tmp/bundler20210519-615-sakpxjracc-1.5.2/gems/racc-1.5.2 for inspection.
Results logged to /tmp/bundler20210519-615-sakpxjracc-1.5.2/extensions/x86_64-linux/2.7.0/racc-1.5.2/gem_make.out

An error occurred while installing racc (1.5.2), and Bundler cannot continue.
Make sure that `gem install racc -v '1.5.2' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  github-pages was resolved to 214, which depends on
    jekyll-mentions was resolved to 1.6.0, which depends on
      html-pipeline was resolved to 2.14.0, which depends on
        nokogiri was resolved to 1.11.4, which depends on
          racc
```

- 인스톨 프로그램? 설치 후 에러 해결 

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
  adwaita-icon-theme at-spi2-core augeas-lenses cpu-checker db-util db5.3-util debootstrap exfat-fuse exfat-utils extlinux f2fs-tools
  fontconfig fonts-droid-fallback fonts-noto-mono fonts-urw-base35 genisoimage ghostscript gstreamer1.0-plugins-base
  gstreamer1.0-plugins-good gstreamer1.0-x gtk-update-icon-cache hfsplus hicolor-icon-theme humanity-icon-theme ibverbs-providers
  icoutils ipxe-qemu ipxe-qemu-256k-compat-efi-roms ldmtool libaa1 libafflib0v5 libarchive-tools libatk-bridge2.0-0 libatk1.0-0
  libatk1.0-data libatspi2.0-0 libaugeas0 libavahi-client3 libavahi-common-data libavahi-common3 libavc1394-0 libboost-iostreams1.71.0
  libboost-thread1.71.0 libbrlapi0.7 libcaca0 libcacard0 libcairo-gobject2 libcairo2 libcdparanoia0 libcolord2 libconfig9 libcups2
  libdate-manip-perl libdatrie1 libdv4 libepoxy0 libewf2 libf2fs-format4 libf2fs5 libfdt1 libgbm1 libgdk-pixbuf2.0-0
  libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgraphite2-3 libgs9 libgs9-common libgstreamer-plugins-base1.0-0
  libgstreamer-plugins-good1.0-0 libgtk-3-0 libgtk-3-bin libgtk-3-common libguestfs-hfsplus libguestfs-perl libguestfs-reiserfs
  libguestfs-tools libguestfs-xfs libguestfs0 libharfbuzz0b libhfsp0 libhivex0 libibverbs1 libidn11 libiec61883-0 libijs-0.35
  libintl-perl libintl-xs-perl libiscsi7 libjack-jackd2-0 libjansson4 libjbig0 libjbig2dec0 libjpeg-turbo8 libjpeg8 liblcms2-2
  libldm-1.0-0 libmp3lame0 libmpg123-0 libnetpbm10 libnl-3-200 libnl-route-3-200 libnspr4 libnss3 libopenjp2-7 libopus0 liborc-0.4-0
  libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpaper-utils libpaper1 libpcsclite1 libpixman-1-0 libpmem1 librados2
  libraw1394-11 librbd1 librdmacm1 librest-0.7-0 librsvg2-2 librsvg2-common libsamplerate0 libshout3 libslirp0 libsoup-gnome2.4-1
  libspeex1 libspice-server1 libstring-shellquote-perl libsys-virt-perl libtag1v5 libtag1v5-vanilla libthai-data libthai0 libtheora0
  libtiff5 libtsk13 libtwolame0 libusbredirparser1 libv4l-0 libv4lconvert0 libvirglrenderer1 libvirt0 libvisual-0.4-0 libvpx6
  libvte-2.91-0 libvte-2.91-common libwavpack1 libwayland-cursor0 libwayland-egl1 libwayland-server0 libwebp6 libwin-hivex-perl
  libxcb-render0 libxcb-shm0 libxcursor1 libxkbcommon0 libxml-parser-perl libxml-xpath-perl libyajl2 libyara3 lsscsi lzop msr-tools
  mtools netpbm nfs-kernel-server osinfo-db ovmf poppler-data qemu-block-extra qemu-system-common qemu-system-data qemu-system-gui
  qemu-system-x86 qemu-utils reiserfsprogs ruby-bcrypt-pbkdf ruby-builder ruby-childprocess ruby-concurrent ruby-domain-name
  ruby-ed25519 ruby-erubis ruby-excon ruby-ffi ruby-fog-core ruby-fog-json ruby-fog-libvirt ruby-fog-xml ruby-formatador
  ruby-http-cookie ruby-i18n ruby-libvirt ruby-listen ruby-log4r ruby-mime-types ruby-mime-types-data ruby-multi-json ruby-net-scp
  ruby-net-sftp ruby-net-ssh ruby-netrc ruby-nokogiri ruby-oj ruby-pkg-config ruby-rb-inotify ruby-rest-client ruby-sqlite3 ruby-unf
  ruby-unf-ext ruby-vagrant-cloud ruby-zip scrub seabios sharutils sleuthkit sqlite3 supermin syslinux syslinux-common ubuntu-mono
  vagrant-libvirt
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  cpp cpp-9 dpkg-dev fakeroot g++ g++-9 gcc gcc-9 gcc-9-base libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl
  libasan5 libatomic1 libc-dev-bin libc6-dev libcc1-0 libcrypt-dev libdpkg-perl libfakeroot libfile-fcntllock-perl libgcc-9-dev libgomp1
  libisl22 libitm1 liblsan0 libmpc3 libquadmath0 libstdc++-9-dev libtsan0 libubsan1 linux-libc-dev make manpages-dev
Suggested packages:
  cpp-doc gcc-9-locales debian-keyring g++-multilib g++-9-multilib gcc-9-doc gcc-multilib autoconf automake libtool flex bison gdb
  gcc-doc gcc-9-multilib glibc-doc bzr libstdc++-9-doc make-doc
The following NEW packages will be installed:
  build-essential cpp cpp-9 dpkg-dev fakeroot g++ g++-9 gcc gcc-9 gcc-9-base libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libasan5 libatomic1 libc-dev-bin libc6-dev libcc1-0 libcrypt-dev libdpkg-perl libfakeroot
  libfile-fcntllock-perl libgcc-9-dev libgomp1 libisl22 libitm1 liblsan0 libmpc3 libquadmath0 libstdc++-9-dev libtsan0 libubsan1
  linux-libc-dev make manpages-dev
0 upgraded, 35 newly installed, 0 to remove and 0 not upgraded.
Need to get 37.6 MB of archives.
After this operation, 161 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libc-dev-bin amd64 2.31-0ubuntu9.2 [71.8 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 linux-libc-dev amd64 5.4.0-73.82 [1130 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/main amd64 libcrypt-dev amd64 1:4.4.10-10ubuntu4 [104 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libc6-dev amd64 2.31-0ubuntu9.2 [2520 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 gcc-9-base amd64 9.3.0-17ubuntu1~20.04 [19.1 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/main amd64 libisl22 amd64 0.22.1-1 [592 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal/main amd64 libmpc3 amd64 1.1.0-1 [40.8 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 cpp-9 amd64 9.3.0-17ubuntu1~20.04 [7494 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/main amd64 cpp amd64 4:9.3.0-1ubuntu2 [27.6 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libcc1-0 amd64 10.2.0-5ubuntu1~20.04 [41.1 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libgomp1 amd64 10.2.0-5ubuntu1~20.04 [102 kB]
Get:12 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libitm1 amd64 10.2.0-5ubuntu1~20.04 [26.4 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libatomic1 amd64 10.2.0-5ubuntu1~20.04 [9300 B]
Get:14 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libasan5 amd64 9.3.0-17ubuntu1~20.04 [394 kB]
Get:15 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 liblsan0 amd64 10.2.0-5ubuntu1~20.04 [144 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libtsan0 amd64 10.2.0-5ubuntu1~20.04 [320 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libubsan1 amd64 10.2.0-5ubuntu1~20.04 [136 kB]
Get:18 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libquadmath0 amd64 10.2.0-5ubuntu1~20.04 [146 kB]
Get:19 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libgcc-9-dev amd64 9.3.0-17ubuntu1~20.04 [2360 kB]
Get:20 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 gcc-9 amd64 9.3.0-17ubuntu1~20.04 [8241 kB]
Get:21 http://archive.ubuntu.com/ubuntu focal/main amd64 gcc amd64 4:9.3.0-1ubuntu2 [5208 B]
Get:22 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libstdc++-9-dev amd64 9.3.0-17ubuntu1~20.04 [1714 kB]
Get:23 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 g++-9 amd64 9.3.0-17ubuntu1~20.04 [8405 kB]
Get:24 http://archive.ubuntu.com/ubuntu focal/main amd64 g++ amd64 4:9.3.0-1ubuntu2 [1604 B]
Get:25 http://archive.ubuntu.com/ubuntu focal/main amd64 make amd64 4.2.1-1.2 [162 kB]
Get:26 http://archive.ubuntu.com/ubuntu focal/main amd64 libdpkg-perl all 1.19.7ubuntu3 [230 kB]
Get:27 http://archive.ubuntu.com/ubuntu focal/main amd64 dpkg-dev all 1.19.7ubuntu3 [679 kB]
Get:28 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 build-essential amd64 12.8ubuntu1.1 [4664 B]
Get:29 http://archive.ubuntu.com/ubuntu focal/main amd64 libfakeroot amd64 1.24-1 [25.7 kB]
Get:30 http://archive.ubuntu.com/ubuntu focal/main amd64 fakeroot amd64 1.24-1 [62.6 kB]
Get:31 http://archive.ubuntu.com/ubuntu focal/main amd64 libalgorithm-diff-perl all 1.19.03-2 [46.6 kB]
Get:32 http://archive.ubuntu.com/ubuntu focal/main amd64 libalgorithm-diff-xs-perl amd64 0.04-6 [11.3 kB]
Get:33 http://archive.ubuntu.com/ubuntu focal/main amd64 libalgorithm-merge-perl all 0.08-3 [12.0 kB]
Get:34 http://archive.ubuntu.com/ubuntu focal/main amd64 libfile-fcntllock-perl amd64 0.22-3build4 [33.1 kB]
Get:35 http://archive.ubuntu.com/ubuntu focal/main amd64 manpages-dev all 5.05-1 [2266 kB]
Fetched 37.6 MB in 11s (3432 kB/s)
Extracting templates from packages: 100%
Selecting previously unselected package libc-dev-bin.
(Reading database ... 93450 files and directories currently installed.)
Preparing to unpack .../00-libc-dev-bin_2.31-0ubuntu9.2_amd64.deb ...
Unpacking libc-dev-bin (2.31-0ubuntu9.2) ...
Selecting previously unselected package linux-libc-dev:amd64.
Preparing to unpack .../01-linux-libc-dev_5.4.0-73.82_amd64.deb ...
Unpacking linux-libc-dev:amd64 (5.4.0-73.82) ...
Selecting previously unselected package libcrypt-dev:amd64.
Preparing to unpack .../02-libcrypt-dev_1%3a4.4.10-10ubuntu4_amd64.deb ...
Unpacking libcrypt-dev:amd64 (1:4.4.10-10ubuntu4) ...
Selecting previously unselected package libc6-dev:amd64.
Preparing to unpack .../03-libc6-dev_2.31-0ubuntu9.2_amd64.deb ...
Unpacking libc6-dev:amd64 (2.31-0ubuntu9.2) ...
Selecting previously unselected package gcc-9-base:amd64.
Preparing to unpack .../04-gcc-9-base_9.3.0-17ubuntu1~20.04_amd64.deb ...
Unpacking gcc-9-base:amd64 (9.3.0-17ubuntu1~20.04) ...
Selecting previously unselected package libisl22:amd64.
Preparing to unpack .../05-libisl22_0.22.1-1_amd64.deb ...
Unpacking libisl22:amd64 (0.22.1-1) ...
Selecting previously unselected package libmpc3:amd64.
Preparing to unpack .../06-libmpc3_1.1.0-1_amd64.deb ...
Unpacking libmpc3:amd64 (1.1.0-1) ...
Selecting previously unselected package cpp-9.
Preparing to unpack .../07-cpp-9_9.3.0-17ubuntu1~20.04_amd64.deb ...
Unpacking cpp-9 (9.3.0-17ubuntu1~20.04) ...
Selecting previously unselected package cpp.
Preparing to unpack .../08-cpp_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking cpp (4:9.3.0-1ubuntu2) ...
Selecting previously unselected package libcc1-0:amd64.
Preparing to unpack .../09-libcc1-0_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking libcc1-0:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libgomp1:amd64.
Preparing to unpack .../10-libgomp1_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking libgomp1:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libitm1:amd64.
Preparing to unpack .../11-libitm1_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking libitm1:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libatomic1:amd64.
Preparing to unpack .../12-libatomic1_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking libatomic1:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libasan5:amd64.
Preparing to unpack .../13-libasan5_9.3.0-17ubuntu1~20.04_amd64.deb ...
Unpacking libasan5:amd64 (9.3.0-17ubuntu1~20.04) ...
Selecting previously unselected package liblsan0:amd64.
Preparing to unpack .../14-liblsan0_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking liblsan0:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libtsan0:amd64.
Preparing to unpack .../15-libtsan0_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking libtsan0:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libubsan1:amd64.
Preparing to unpack .../16-libubsan1_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking libubsan1:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libquadmath0:amd64.
Preparing to unpack .../17-libquadmath0_10.2.0-5ubuntu1~20.04_amd64.deb ...
Unpacking libquadmath0:amd64 (10.2.0-5ubuntu1~20.04) ...
Selecting previously unselected package libgcc-9-dev:amd64.
Preparing to unpack .../18-libgcc-9-dev_9.3.0-17ubuntu1~20.04_amd64.deb ...
Unpacking libgcc-9-dev:amd64 (9.3.0-17ubuntu1~20.04) ...
Selecting previously unselected package gcc-9.
Preparing to unpack .../19-gcc-9_9.3.0-17ubuntu1~20.04_amd64.deb ...
Unpacking gcc-9 (9.3.0-17ubuntu1~20.04) ...
Selecting previously unselected package gcc.
Preparing to unpack .../20-gcc_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking gcc (4:9.3.0-1ubuntu2) ...
Selecting previously unselected package libstdc++-9-dev:amd64.
Preparing to unpack .../21-libstdc++-9-dev_9.3.0-17ubuntu1~20.04_amd64.deb ...
Unpacking libstdc++-9-dev:amd64 (9.3.0-17ubuntu1~20.04) ...
Selecting previously unselected package g++-9.
Preparing to unpack .../22-g++-9_9.3.0-17ubuntu1~20.04_amd64.deb ...
Unpacking g++-9 (9.3.0-17ubuntu1~20.04) ...
Selecting previously unselected package g++.
Preparing to unpack .../23-g++_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking g++ (4:9.3.0-1ubuntu2) ...
Selecting previously unselected package make.
Preparing to unpack .../24-make_4.2.1-1.2_amd64.deb ...
Unpacking make (4.2.1-1.2) ...
Selecting previously unselected package libdpkg-perl.
Preparing to unpack .../25-libdpkg-perl_1.19.7ubuntu3_all.deb ...
Unpacking libdpkg-perl (1.19.7ubuntu3) ...
Selecting previously unselected package dpkg-dev.
Preparing to unpack .../26-dpkg-dev_1.19.7ubuntu3_all.deb ...
Unpacking dpkg-dev (1.19.7ubuntu3) ...
Selecting previously unselected package build-essential.
Preparing to unpack .../27-build-essential_12.8ubuntu1.1_amd64.deb ...
Unpacking build-essential (12.8ubuntu1.1) ...
Selecting previously unselected package libfakeroot:amd64.
Preparing to unpack .../28-libfakeroot_1.24-1_amd64.deb ...
Unpacking libfakeroot:amd64 (1.24-1) ...
Selecting previously unselected package fakeroot.
Preparing to unpack .../29-fakeroot_1.24-1_amd64.deb ...
Unpacking fakeroot (1.24-1) ...
Selecting previously unselected package libalgorithm-diff-perl.
Preparing to unpack .../30-libalgorithm-diff-perl_1.19.03-2_all.deb ...
Unpacking libalgorithm-diff-perl (1.19.03-2) ...
Selecting previously unselected package libalgorithm-diff-xs-perl.
Preparing to unpack .../31-libalgorithm-diff-xs-perl_0.04-6_amd64.deb ...
Unpacking libalgorithm-diff-xs-perl (0.04-6) ...
Selecting previously unselected package libalgorithm-merge-perl.
Preparing to unpack .../32-libalgorithm-merge-perl_0.08-3_all.deb ...
Unpacking libalgorithm-merge-perl (0.08-3) ...
Selecting previously unselected package libfile-fcntllock-perl.
Preparing to unpack .../33-libfile-fcntllock-perl_0.22-3build4_amd64.deb ...
Unpacking libfile-fcntllock-perl (0.22-3build4) ...
Selecting previously unselected package manpages-dev.
Preparing to unpack .../34-manpages-dev_5.05-1_all.deb ...
Unpacking manpages-dev (5.05-1) ...
Setting up manpages-dev (5.05-1) ...
Setting up libfile-fcntllock-perl (0.22-3build4) ...
Setting up libalgorithm-diff-perl (1.19.03-2) ...
Setting up linux-libc-dev:amd64 (5.4.0-73.82) ...
Setting up libgomp1:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up libfakeroot:amd64 (1.24-1) ...
Setting up fakeroot (1.24-1) ...
update-alternatives: using /usr/bin/fakeroot-sysv to provide /usr/bin/fakeroot (fakeroot) in auto mode
Setting up make (4.2.1-1.2) ...
Setting up libquadmath0:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up libmpc3:amd64 (1.1.0-1) ...
Setting up libatomic1:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up libdpkg-perl (1.19.7ubuntu3) ...
Setting up libubsan1:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up libcrypt-dev:amd64 (1:4.4.10-10ubuntu4) ...
Setting up libisl22:amd64 (0.22.1-1) ...
Setting up libc-dev-bin (2.31-0ubuntu9.2) ...
Setting up libalgorithm-diff-xs-perl (0.04-6) ...
Setting up libcc1-0:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up liblsan0:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up libitm1:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up gcc-9-base:amd64 (9.3.0-17ubuntu1~20.04) ...
Setting up libalgorithm-merge-perl (0.08-3) ...
Setting up libtsan0:amd64 (10.2.0-5ubuntu1~20.04) ...
Setting up dpkg-dev (1.19.7ubuntu3) ...
Setting up libasan5:amd64 (9.3.0-17ubuntu1~20.04) ...
Setting up cpp-9 (9.3.0-17ubuntu1~20.04) ...
Setting up libc6-dev:amd64 (2.31-0ubuntu9.2) ...
Setting up libgcc-9-dev:amd64 (9.3.0-17ubuntu1~20.04) ...
Setting up cpp (4:9.3.0-1ubuntu2) ...
Setting up gcc-9 (9.3.0-17ubuntu1~20.04) ...
Setting up libstdc++-9-dev:amd64 (9.3.0-17ubuntu1~20.04) ...
Setting up gcc (4:9.3.0-1ubuntu2) ...
Setting up g++-9 (9.3.0-17ubuntu1~20.04) ...
Setting up g++ (4:9.3.0-1ubuntu2) ...
update-alternatives: using /usr/bin/g++ to provide /usr/bin/c++ (c++) in auto mode
Setting up build-essential (12.8ubuntu1.1) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
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
>
```

## 실행

### bundle exec jekyll serve

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

![image-20210519215454781](C:\Users\jb.won\AppData\Roaming\Typora\typora-user-images\image-20210519215454781.png)

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
> cat README.md
mediator
========

A medium inspired Jekyll blog theme. The basic idea came from the Ghost theme
[Readium 2.0](http://www.svenread.com/readium-ghost-theme/). I use mediator on my own blog [The Base](http://blog.base68.com).

Screenshots
--------
![screenshot](/assets/images/screenshot1.jpg)
![screenshot](/assets/images/screenshot2.jpg)
![screenshot](/assets/images/screenshot3.jpg)

Features
-------
* Fully Responsive layout
* Use header images in articles, if you want to (add tag "image" and url to the image in the front matter section of a post)
* Minimal design
* Featured article support
* FontAwesome implemented for easy use of icons fonts
* Free & Open Source Font usage

Getting Started
---
- [Fork this repository](https://github.com/dirkfabisch/mediator)
- Clone it: `git clone https://github.com/YOUR-USER/mediator`
- Install the requried gems ([GitHub Pages](https://github.com/github/pages-gem), [Bourbon](https://github.com/thoughtbot/bourbon) and [Jekyll](https://github.com/jekyll/jekyll), [Jemoji](https://github.com/jekyll/jemoji)): `bundle install`
- Run the jekyll server: `bundle exec jekyll serve`

You should have a server up and running locally at <http://localhost:4000>.

Configuration
-----

The main settings happen in side of the _config.yml file:

### Site

Main settings for the site

* **title**: name of your site
* **description**: description of your site
* **logo**: small logo for the site (300x * 300x)
* **cover**: large background image on the index page

* **name**: name site owner
* **email**: mail address of the site owner
* **author**: author name
* **author_image**: small image of author (300x * 300px)
* **disqus**: add a disqus forum for your post

### Social

The template allows to add all major social platforms to your site.
Fill the the form for each platform. If you leave the share_* entries empty, the sharing buttons below a post are not shown.  If you leave the **url** and **desc** empty the icons are not shown on the index page, but the share icons on the article pages remains untouched (Thanks to [Phil](https://github.com/philsturgeon))

* **icon**:     name of social platform (must match a name of [font-awsome](http://fortawesome.github.io/Font-Awesome/) icon set )
* **url**:      url of your account
* **desc**: slogan of the platform
* **share_url**: share url
* **share_title**: first part of url for the title
* **share_link**: second part of the share url for the link to the post

The Liquid template engine will magical combine the different parts to a share url.

​```
http://twitter.com/share?text=post_title&amp;url=post_url
​````

See [_config.yml](https://github.com/dirkfabisch/mediator/blob/master/_config.yml) for more examples.

Licensing
---------

[MIT](https://github.com/dirkfabisch/mediator/blob/master/LICENCE) with no added caveats, so feel free to use this on your site without linking back to me or using a disclaimer or anything silly like that.

Contact
-------
I'd love to hear from you at [@dirkfabisch](https://twitter.com/dirkfabisch). Feel free to open issues if you run into trouble or have suggestions. Pull Requests always welcome.
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
Username for 'https://github.com': igotoo
Password for 'https://igotoo@github.com':
remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/igotoo/igotoo.github.io.git/'
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

![image-20210520000148451](C:\Users\jb.won\AppData\Roaming\Typora\typora-user-images\image-20210520000148451.png)

- 예전 블로그 삭제후 404 Not Found Error 발생
  - 원인 : 페이지 소스가 None으로 되어 있었음

    ![image-20210520002914315](C:\Users\jb.won\AppData\Roaming\Typora\typora-user-images\image-20210520002914315.png)

  - None 을 Main으로 변경 후 정상적으로 보임

    ![image-20210520003005822](C:\Users\jb.won\AppData\Roaming\Typora\typora-user-images\image-20210520003005822.png)

    