---
layout: post
title: "github 접속을 https에서 ssh 접속으로 변경하기"
date: 2021-05-20 00:14:10 +0900
categories:  rsa, github, ssh, ssh-agent
---
##  Key 생성
- 개인키(private key)와 공인키(public key) 생성
- ssh-keygen -t ed25519 -C "github 로그인 메일 아이디"
```bash
> ssh-keygen -t ed25519 -C "igotoo@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/igotoo/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/igotoo/.ssh/id_ed25519
Your public key has been saved in /home/igotoo/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:c62zCE0hCHtsdfsdfgSvvXsb91edsfskYnLOuhh/GcNc igotoo@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|  . . .. o.o..   |
|   * o. . o .    |
|  + +..o.  .     |
|   +  +.....  .  |
|  .  .  S+.... E |
|       o o=oo.. o|
|      . ..+++=..o|
|       . oo*. *..|
drwxr-xr-x 14 igotoo igotoo 4096 May 23 19:08 ..
-rw-r--r--  1 igotoo igotoo  141 May 23 18:01 config
-r--------  1 igotoo igotoo 1675 May 23 17:30 gblg3_id_rsa
-rw-------  1 igotoo igotoo  411 May 23 19:08 id_ed25519
-rw-r--r--  1 igotoo igotoo   98 May 23 19:08 id_ed25519.pub
-r--------  1 igotoo igotoo 3354 May 21 18:34 id_rsa.bak
-r--------  1 igotoo igotoo 1679 May 21 18:35 kdrvstg_id_rsa
-rw-r--r--  1 igotoo igotoo 3108 May 23 17:28 known_hosts
```

## 개인 key ssh-agent 에 등록 
- ssh-agent 
  - 공개키 인증을 위한 개인키를 보관하는 프로그램으로 다른 서버를 로그인시 인증에 사용된다.
  - 공개키는 접속하려는 서버에 저장되어 있어야 한다.(이경우 github 서버)
- 등록하는 이유 
  - github 접속시 git 프로그램이 ssh-agent에 등록되어 있는 개인키 정보를 이용하여  자동 ssh 인증처리로 id/passwd 입력 불필요
- 등록방법 
  - ssh-agent 백그라운드 실행 : eval "$(ssh-agent -s)"
  - ssh-add로 개인키 등록 : ssh-add ~/.ssh/개인키파일명
```bash
> eval "$(ssh-agent -s)"
Agent pid 611
> ssh-add ~/.ssh/id_ed25519
Identity added: /home/igotoo/.ssh/id_ed25519 (igotoo@gmail.com)
```
- ssh-agent를 eval로 실행 시키는 이유
  - eval는 명령
    >  [명령 치환](https://mug896.github.io/bash-shell/exp_and_sub/command_substitution.html) 결과로 shell 에서 실행 가능한 명령문이 나온다면 그 명령은 기본적으로 실행이 가능합니다. 하지만 명령문이 조금 복잡해져서 파이프나 redirections, quotes 등이 사용된다면 이제는 그 명령문은 실행할 수 없게 됩니다. 왜냐하면 명령문에서 사용되는 shell 키워드, 메타문자들, quotes 등은 [확장과 치환](https://mug896.github.io/bash-shell/expansions_and_substitutions.html) 이전에 해석이 완료되기 때문입니다. 따라서 이와 같은 경우에도 실행이 가능하게 해주는 명령이 eval 명령입니다. eval 은 인수로 주어지는 스트링을 한번 evaluation 한 후에 결과를 다시 명령문으로 실행합니다.
    >
    > 출처 : [eval | Introduction (mug896.github.io)](https://mug896.github.io/bash-shell/eval.html)

  - 다음과 같이 ssh-agent를 실행하는 경우 환경변수를 셋팅하고 백그라운드로 실행되어야 하는데 eval를 사용하는 경우 명령문에서 먼저 해석이 되어 환경 변수가 셋팅 되지 않는다.
  ```bash
  > env | grep -i SSH
  SSH_AUTH_SOCK=
  SSH_AGENT_PID=
  > ssh-agent -s
  SSH_AUTH_SOCK=/tmp/ssh-4sIsqE1flEg0/agent.1456; export SSH_AUTH_SOCK;
  SSH_AGENT_PID=1457; export SSH_AGENT_PID;
  echo Agent pid 1457;
  > env | grep -i SSH
  SSH_AUTH_SOCK=
  SSH_AGENT_PID=
  > eval "$(ssh-agent -s)"
  Agent pid 1469
  > env | grep -i SSH
  SSH_AUTH_SOCK=/tmp/ssh-5vZqJr5zfN7B/agent.1468
  SSH_AGENT_PID=1469
  ```
## github 등록
- 개인 페이지 설정에서 공개키 (id_ed25519.pub)을 복사 붙여넣기로 등록

![image-20210523193547902](/assets/images/ximage-20210523193547902.png)

## remote origin (github 서버) 변경 
- https://github.com/igotoo/igotoo.github.io.git 에서 git@github.com:사용자id/사용자 레파지토리 명으로 변경
  - 기존 remote origin 삭제
  - ssh 접속 정보로 remote orgin 등록 
  - remote origin main 을 upstream으로 설정

```bash
> git push
Username for 'https://github.com': igotoo@gmail.com
Password for 'https://igotoo@gmail.com@github.com':
remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/igotoo/igotoo.github.io.git/'

> git remote remove origin
> git remote add origin git@github.com:igotoo/igotoo.github.io.git

> git push
fatal: The current branch main has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin main

> git push --set-upstream origin main
The authenticity of host 'github.com (15.164.81.167)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,15.164.81.167' (RSA) to the list of known hosts.
Enumerating objects: 17, done.
Counting objects: 100% (17/17), done.
Delta compression using up to 8 threads
Compressing objects: 100% (14/14), done.
Writing objects: 100% (14/14), 3.24 MiB | 2.01 MiB/s, done.
Total 14 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:igotoo/igotoo.github.io.git
   feb878a..83dabb5  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.

> git push
Warning: Permanently added the RSA host key for IP address '52.78.231.108' to the list of known hosts.
Everything up-to-date
/mnt/d/Blog/mediator main
```

## 검증 테스트 
- ssh-agent  및 ~/.ssh/config 파일 역할 검증

```bash
> echo "github login test2" >> test.txt
> git add test.txt
> git commit -m "github login test2 /w ssh"
[main 346a1d4] github login test2 /w ssh
 1 file changed, 1 insertion(+)
 
> ps -ef|grep ssh-agent
igotoo     886   271  0 19:21 pts/2    00:00:00 man ssh-agent

> cat ~/.ssh/config
#Host github.com
#       User git
#       IdentityFile ~/.ssh/id_ed25519
Host gblg3.igotoo.pw
        User igotoo
        Port 22014
        IdentityFile ~/.ssh/gblg3_id_rsa
> git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 280 bytes | 17.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:igotoo/igotoo.github.io.git
   f1dce52..346a1d4  main -> main
```
- ssh-agent 실행 필요 여부  :  실행 필요없음, git push/pull 등 github 접속이 필요할 경우 ssh-agent 자동 실행하는 것을 추정됨 
- ~/.ssh/config 사용 여부  : 설정파일이 없어도 ssh-agent에 github에 접속 정보 즉 개인키를 등록해 놓았으므로 별도 설정은 불필요

## WRAP UP
- github 접속을 https에서 ssh접속으로 변경하여 매번 ip/pwd 입력 불필요
- 개인키를 등록한 ssh-agent가 실행시 설정하는 환경변수를(pid, sock) 이용 다른 서버 접속시 자동으로 공개키 인증
- 다른 방법으로는 사용자 ssh 설정파일 (~/.ssh/config)에 호스트명(예 : giithub.com) , 개인키 파일 정보(id_ed25519)와 사용자 이름 정보를 등록하여 자동 인증 가능 
- 참고 :
  - [Connecting to GitHub with SSH - GitHub Docs](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)
  -  [Github 다수 계정을 위한 SSH key 설정 :: 마이구미 :: 마이구미의 HelloWorld (tistory.com)](https://mygumi.tistory.com/96)
  - [한 대의 맥에서 여러 개의 깃허브(github) 계정 사용하는 방법 · Tonic (jwgo.kr)](https://devlog.jwgo.kr/2018/08/17/how-to-use-multi-github-accounts-with-a-machine/)
  - [SSH Key - 비밀번호 없이 로그인 - 원격제어 (opentutorials.org)](https://opentutorials.org/module/432/3742)

