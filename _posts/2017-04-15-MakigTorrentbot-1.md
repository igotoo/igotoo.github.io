---
layout: post
title:  "텔레그램 봇으로 토렌트 자동 다운로드"
date:   2017-04-15 15:48:35 +0900
categories: telepot, torrent
---
### 프롤로그
라즈베리파이를 어디에 쓸데가 없을까 고민하다가 봇에 대하 잡담중에 우연히 떠오른 아이디어(?) 웹크롤링, 토렌트 서버 등을 이용해서 토렌트를 찾아서 자동으로 다운로드해주는 봇을 만들어보자로 시작.
그러나 이런거 있을까 하고 구글링([토렌트 봇으로 구글링](https://www.google.co.kr/search?q=토렌트+봇&gws_rd=cr&ei=EKrxWN7_H8On8QWEhpiYDA)) 하면 웬만한건 다있다는 말을 새삼 깨달음. telegram Bot API를 이용 토렌트를 자동으로 다운받은 여러 프로그램들을 이미 존재하고 github에도 공개되어 있었음. 그것도 2016년에 유행
그래도 해보면 재미있을거 같아 시작.

**[참고 사이트]**
  * 가장 기본이 된 연결고리 사이트 [Telebot을 이용한 원격 토렌트 다운로드 시스템](https://redreamer.wordpress.com/2016/01/03/telebot을-이용한-원격-토렌트-다운로드-시스템/) - redreamer님 감사합니다.
  * [telebot을 이용한 원격 토렌트 다운로드 시스템-github](https://github.com/seungjuchoi/telegram-control-torrent)
  * telegram torrent bot 프레임웍 github [telepot - Python framework for Telegram Bot API](https://github.com/nickoala/telepot#telepot---python-framework-for-telegram-bot-api)
  * 꼼꼼히 너무 잘 설명되어 있어 몇번씩 읽은 [How to Turn a Raspberry Pi into an Always-On BitTorrent Box](https://www.howtogeek.com/142044/how-to-turn-a-raspberry-pi-into-an-always-on-bittorrent-box/)
  * [Bots: An introduction for developers](https://core.telegram.org/bots)

redreamer님 블로그 [Telebot을 이용한 원격 토렌트 다운로드 시스템](https://redreamer.wordpress.com/2016/01/03/telebot을-이용한-원격-토렌트-다운로드-시스템/)와 HTG의 [How to Turn a Raspberry Pi into an Always-On BitTorrent Box](https://www.howtogeek.com/142044/how-to-turn-a-raspberry-pi-into-an-always-on-bittorrent-box/)을 기반으로 정리함. 작업하면서 동시에 정리하는 게 제일 좋을거 같은데 동시에는 마음이 급해서인지 어려움이 많다. 개요파악 - 관련 지식 습득 - 계획(시나리오) - 작업 - test - 정리 가장 좋은 절차라고 생각하나 늘 이상과 현실은 다름.


### 1. 라즈베리파이 토렌트 환경 구성
#### 라즈베리 설치 및 구성
- 기존에 설치하여 활용중인 라즈베리 파이가 있으므로 기본 구성 및 ssh 설정, 한글화 설정 등은 생략
- 본 블로그 [라즈베리언 재설치](https://igotoo.github.io/rasberry/pi/2017/03/26/RasberryPi-Rasbrian-intall.html) 참고
- HTG([How-To Geek](https://www.howtogeek.com/)) 참고
  * [Everything You Need to Know About Getting Started with the Raspberry Pi](https://www.howtogeek.com/138281/the-htg-guide-to-getting-started-with-raspberry-pi/)
  * [How to Configure Your Raspberry Pi for Remote Shell, Desktop, and File Transfer](https://www.howtogeek.com/141157/how-to-configure-your-raspberry-pi-for-remote-shell-desktop-and-file-transfer/)
  * [How to Turn a Raspberry Pi into a Low-Power Network Storage Device](https://www.howtogeek.com/139433/how-to-turn-a-raspberry-pi-into-a-low-power-network-storage-device/)
#### 노는 포터블 외장하드 활용 라즈베리파이 NAS 만들기
##### 작업요약
- 준비물 : 포터블 외장하드(약전원-USB 전원으로도 작동하는), 외장하드용 USB라인, 라즈베리파이 2
- 환경 :
- 구형 노트북에 사용했었던 포터블 외장하드(Hitachi 120G) 사용
- 라즈베리파이에 연결하자 마자 인식되었다 잠시 후 집에있는 아이맥, PC, 라즈베리 파이 모드 인식인 안됨
- 포터블 외장하드 케이스 마저 오래되어 전원부족으로 문제 생각하고 외장하드에 전원연결 재시도 했으나 인식 안됨
- 외장하드케이스에서 분리 재조립 후 아이맥에서 인식된 이후 라즈베리파이에도 인식됨
- 라즈베리파이에서 3개의 파티션 날리고(fsck) 리눅파일(ext2?)로 통으로 포멧
- [How to Turn a Raspberry Pi into a Low-Power Network Storage Device](https://www.howtogeek.com/139433/how-to-turn-a-raspberry-pi-into-a-low-power-network-storage-device/) 읽고 다시 NTFS로 포멧 및 마운트하고 samba 설치 완료
- 이 작업중에 알게 된 사실 **라즈베리파이 화면에 번개표시**가 항상 떠있길래 원래 그런줄 알았는데, **전원이 부족하다는 표시**였음 WiFi AP USB 단자로 전원을 공급했었는데 외장하드 미인식으로 아답터로 전원 공급으로 전환 후 번개 표시 사라지고 속도도 개선됨

##### 외장하드 포멧 및 마운트
- 작업 순서 : ntfs-3g 설치 -> 파티션 삭제 -> 포멧 -> 마운트 -> 부팅시 자동 마운트 설정
- pc 접근 및 응급조치 용이를 위해 M$ Windows 파일 포멧으로 외장하드 구성, 리눅스에서 Windows 파포멧 인식을 위해 ntfs-3g 설치
```sudo apt-get install ntfs-3g```
- 외장하드 디스크 마운트
  * 정보확인 : sudo fdisk -l (보통 /dev/sda로 인식됨)
  * 파티션 신규 통합 생성 : sudo fsck /dev/sda (m - p - n - 1 - w, [참고 - 우분투에서 하드디스크 파티션 및 EXT4로 포맷하기](https://solha.kr/xe/index.php?document_srl=2266&mid=board_AVQK63))
  * 포멧 : mkfs -t ntfs -v /dev/sda1
  * 마운트 디렉토리 생성 : sudo mkdir /media/usbhdd1
  * 마운트 : sudo mount /dev/sda1 /media/usbhdd1/

- 외장하드 연결결과 확인
  ```
  pi@boriliketree:~ $ sudo fdisk -l

  ##### SSD 8 G - OS
  Device         Boot  Start      End  Sectors  Size Id Type
  /dev/mmcblk0p1        8192   137215   129024   63M  c W95 FAT32 (LBA)
  /dev/mmcblk0p2      137216 15523839 15386624  7.3G 83 Linux

  Disk /dev/sda: 111.8 GiB, 120034123776 bytes, 234441648 sectors
  Units: sectors of 1 * 512 = 512 bytes
  Sector size (logical/physical): 512 bytes / 512 bytes
  I/O size (minimum/optimal): 512 bytes / 512 bytes
  Disklabel type: dos
  Disk identifier: 0x40b96660

  ### 포터볼 외장하드 120G

  Device     Boot Start       End   Sectors   Size Id Type
  /dev/sda1        2048 234441647 234439600 111.8G 83 Linux

  pi@boriliketree:~ $ df -h
  Filesystem      Size  Used Avail Use% Mounted on
  /dev/root       7.1G  5.0G  1.9G  73% /
  devtmpfs        459M     0  459M   0% /dev
  tmpfs           463M     0  463M   0% /dev/shm
  tmpfs           463M   48M  416M  11% /run
  tmpfs           5.0M  4.0K  5.0M   1% /run/lock
  tmpfs           463M     0  463M   0% /sys/fs/cgroup
  /dev/mmcblk0p1   63M   21M   42M  33% /boot
  /dev/sda1       112G   69M  112G   1% /media/usbhdd1
  tmpfs            93M     0   93M   0% /run/user/1000
  tmpfs            93M     0   93M   0% /run/user/0
  pi@boriliketree:~ $ cat /etc/fstab
  proc            /proc           proc    defaults          0       0
  /dev/mmcblk0p1  /boot           vfat    defaults          0       2
  /dev/mmcblk0p2  /               ext4    defaults,noatime  0       1
  /dev/sda1 	 /media/usbhdd1         ntfs    defaults,noatime  0       0
  # a swapfile is not a swap partition, no line here
  #   use  dphys-swapfile swap[on|off]  for that
  ```
##### samba 설치 및 설정

$ sudo vi /etc/samba/smb.confsudo apt-get install samba samba-common-bin  
- samb 설정
```
$ sudo vi /etc/samba/smb.conf
[Finetree]
comment = Share Folder
path = /media/usbhdd1/shares
valid users = @users
force group = users
create mask = 0600
directory mask = 0771
read only = no
```
- samba 전용 사용자 생성(보안상이유?) : 시스템 사용자 생성 후 samba 사용자로 등록

```
시스템 유저 생성
$ sudo useradd finetree -m -G users
$ sudo passwd finetree

samba 사용자 등록
$ sudo smbpasswd -a backups
```

### 2. telepot 이용 torrent bot 만들기

- Telegram Bot 구성
[참고 - Set Up Telegram Bot on Raspberry Pi](http://www.instructables.com/id/Set-up-Telegram-Bot-on-Raspberry-Pi/)

- deluge 설치 및 설정
  * 부팅시 자동으로 실행되도록 설정
  ```
  #Start Deluge on boot:
  sudo -u pi /usr/bin/python /usr/bin/deluged
  sudo -u pi /usr/bin/python /usr/bin/deluge-web
  ```
- telegram-control-torrent 설치 및 설정
  * 부팅시 자동으로 실행되도록 설정
  ```
  #Start telegram_torrent on boot -2017.04.16
  sudo -u pi /home/pi/telegram-control-torrent/telegram_torrent.py 2&>> /home/pi/telegram-control-torrent/telegram-control.log
  ```

### 3. 테스트/마무리
- 다운로드 후 Plex에서 라이브러리 업데이트 안되는 현상 발생 -> 해결 : 수동 업데이트 설정
>The top option, “Update my library automatically”, is the ideal one. Nearly every Plex user should check it. The only time automated library updates aren’t a viable solution is for Plex users with their media stored on a different computer from the Plex Media Server program (since the automatic detection of folders doesn’t typically work for folders on a network share).
[참고 - How to Update Your Plex Media Library, Manually and Automatically](https://www.howtogeek.com/254357/how-to-update-your-plex-media-library-manually-and-automatically/)

- 개선 필요사항
  * 영화에 대한 트레일러, 출연진, 포스트 등 (사용자가 원할 경우)정보 제공 필요
  * 다른 토렌트 사이트 사용자 선택 가능 기능(?) - 그냥 막 적는구나
  * 한글화
  * 사용자 오입력에 대한 예외처리
  * 자막도 동시에 찾아서 다운로할 수 있게 .. -> 자막파일 다운로드 할 수 있음 문제는 자막파일이 토렌트 파일에 들어 있지 않을 경우 어디에 다른 디렉토리에 두고 나중에 옮겨주어야 한다....
