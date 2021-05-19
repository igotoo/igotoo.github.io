---
layout: post
title: "라즈베리언 재설치"
date: 2017-03-26 15:48:35 +0900
categories: Rasberry Pi
---

-  Why
    Open Plex  용으로  사용하던  라즈베리 파이 2  B 를  TV 앱 (LG)  프로그램으로
    PLEX를 사용 가능 하게 됨으로 써  효용가치  급격히 떨어짐

    ※ 미디어 서버와 클라이언트로 주로 XBMC를 써오다가  XBMC 비해 연동 클라이언트 가  많고,
         상대적으로  안정적인 PLEX  Media Server 를  PC와 iMac 에 운용 중
         (향후 라즈베리 파이 3 로  PLEX  Media Server 이관 예정)
         라즈베리 파이는 원래   라즈베리용  XBMC  클라이언트인  Open ELEC 용으로 구매.

- What
     Rasbian  설치  및  환경 설정 (한글 설정, realVNC 설치 등 )   

### 1. Rasbian 설치  : Raspbian Jessie with PIXEL
- Command line  install  방법으로 설치
-  diskutil list  : Identify the disk (not partition) of your SD card e.g. disk4, not disk4s1.
- Unmount your SD card by using the disk identifier, to prepare it for copying data:
  diskutil unmountDisk /dev/disk<disk# from diskutil>
- Copy the data to your SD card:
   sudo dd bs=1m if=image.img of=/dev/rdisk<disk# from diskutil>
- 설치 정보  
Raspbian Jessie with PIXEL
Image with PIXEL desktop based on Debian Jessie
Version: March 2017
Release date: 2017-03-02
Kernel version: 4.4

※ graphical interface (반반 방법 ) 으로 설치하려다가  dd 명령시 rdisk 를 disk3로 오기 (문서는 상관 없다고 하여 일단 무시 진행 )  -> 부팅되지 않음 -> SSD card 읽히지 않음 -> 삭제 후 재 포멧  -> command line 방법으로 재 설치

 [참고 - INSTALLING OPERATING SYSTEM IMAGES ON MAC OS](  https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)

### 2. 초기 설정
- 패스워드 변경
- Time Zone 셋팅
-  locale 변경  :  en -> euc-kr  (putty, Mac terminal 에서  한글 깨짐 ) -> ko-utf-8
- 고정 IP 셋팅
  * [참고 - Static IP For Your Pi On The Home Network](http://readwrite.com/2014/04/09/raspberry-pi-projects-ssh-remote-desktop-static-ip-tutorial/)
  * [참고 - 라즈베리파이 기본 설정 (OS 부터 필수 패키지 설치까지)](http://www.hardcopyworld.com/gnuboard5/bbs/board.php?bo_table=lecture_rpi&wr_id=1)

### 3. 셋팅 중 해상도 변경으로 부팅 안됨
 - 1280*1024 해상도로 변경후  부팅되지 않음
 - SSDCard 분리 Mac에서 config.txt를  열어서 safe mode  #제거 후 재부팅  성공
 - 안전모드로 진입 후 해상 도 default  mode로 셋팅 후  안전모드 코멘트(#)처리 하고 재부팅 성공

### 4. realVNC 설치  
- XRDP를 설치 하려 고  했으나 .....

  > "라즈베리 파이를 PC에서 원격제어하기 위해서 XRDP 를 시도해 보았습니다.
   이번에 새로나온 라즈비안 PIXEL 버젼에는 이미 RealVNC라는 프로그램이 깔려있기 때문에 XRDP와 충돌한다고 합니다."  [출처 - 라즈베리파이 VNC 실행](http://m.blog.naver.com/cubloc/220829612566)
   > ```
   >RealVNC have ported their VNC server and viewer applications to Pi, and they are now integrated with the system. To enable the server, select the option on the Interfaces tab in Raspberry Pi Configuration; you’ll see the VNC menu appear on the taskbar, and you can then log in to your Pi and control it remotely from a VNC viewer.
  >
  >The RealVNC viewer is also included – you can find it from the Internet section of the Applications menu – and it allows you to control other RealVNC clients, including other Pis. Have a look here on RealVNC’s site for more information.  
  >  
  > Please note that if you already use xrdp to remotely access your Pi, this conflicts with the RealVNC server, so you shouldn’t install both at once.
  >```
  >
  >[출처 - INTRODUCING PIXEL](https://www.raspberrypi.org/blog/introducing-pixel/)
>
- PC/iMac realVNC viewer 설치 및 한글 설정(uim 설치 )   
  * [참고 - Raspberry PI 3를 VNC로 접속하여 원격 제어 (x11vnc)](http://webnautes.tistory.com/549)
