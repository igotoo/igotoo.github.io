---
layout: post
title:  "Windows에서 WSL2/Vagrant/VBox로 Ansible 실습"
date:   2021-06-05 09:000:35 +0900
categories: WSL2, Vagrant, VirtualBox
---
## 개요

WSL2에 Vagrant를 설치하여 호스트에 설치된 virtualbox을 활용하여  VM 생성/구성/관리 가능

- 윈도우에는 ansible control 서버를 설치 할 수 없어 ansible provisioner를 사용할 수 없음
- vagrant에서 ansible/ansible_local 지원
    - [ansible](https://www.vagrantup.com/docs/provisioning/ansible), where Ansible is executed on the **Vagrant host**
    - [ansible_local](https://www.vagrantup.com/docs/provisioning/ansible_local), where Ansible is executed on the **Vagrant guest**
- ansible provioner는 호스트에  asnible 설치, ansible_local는 guest에 ansible 설치 따라서 window host에서는 ansible_local 사용
- 참고
    
    [주요 참고 : Appendix A - Vagrant with VirtualBox within WSL2 to run ansible-for-devops VMs #291](https://github.com/geerlingguy/ansible-for-devops/issues/291#issuecomment-815253528)

    [Common Ansible Options - Provisioning | Vagrant by HashiCorp](https://www.vagrantup.com/docs/provisioning/ansible_common)

    [Ansible - Short Introduction | Vagrant by HashiCorp](https://www.vagrantup.com/docs/provisioning/ansible_intro)

## 사전 설치

- 호스트 vagrant(windows 10)와 WSL2 vagrant 버전 통일

    > NOTE: When Vagrant is installed on the Windows system the version installed within the Linux distribution must match.'

    - 에러 메세지

    ```bash
    The provider 'virtualbox' that was requested to back the machine 'default' is reporting that it isn't usable on this system. The reason is shown below:
    			
    VirtualBox is complaining that the kernel module is not loaded. Please
    run `VBoxManage --version` or open the VirtualBox GUI to see the error
    message which should contain instructions on how to fix this error.
    ```

    - WSL2 vagrant 삭제후 재 설치

    ```bash
    > wget https://releases.hashicorp.com/vagrant/2.2.16/vagrant_2.2.16_linux_amd64.zip
    > unzip vagrant_2.2.16_linux_amd64.zip
    > sudo mv ./vagrant /usr/local/bin/vagrant
    ```

- basdtar 설치
    - vagrant가 아카이브 파일 읽고/쓰기 위해 필요, 미 설치로 다음 에러 발생

    ```bash
    INFO interface: error: The executable 'bsdtar' Vagrant is trying to run was not
    found in the PATH variable. This is an error. Please verify
    this software is installed and on the path.
    The executable 'bsdtar' Vagrant is trying to run was not
    found in the PATH variable. This is an error. Please verify
    this software is installed and on the path.
    INFO interface: Machine: error-exit ["Vagrant::Errors::CommandUnavailable", "The executable 'bsdtar' Vagrant is trying to run was not\nfound in the PATH variable. This is an error. Please verify\nthis software is installed and on the path."]
    ```

    - 설치

    ```bash
    > sudo apt install libarchive-tools
    ```

- ssh 오류 해결
    - ssh 오류 해결 plugin 설치:  vagrant plugin install virtualbox_WSL2

    ```bash
    ...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    Timed out while waiting for the machine to boot. This means that
    Vagrant was unable to communicate with the guest machine within
    the configured ("config.vm.boot_timeout" value) time period.If you look above, you should be able to see the error(s) that
    Vagrant had when attempting to connect to the machine. These errors
    are usually good hints as to what may be wrong.If you're using a custom box, make sure that networking is properly
    working and you're able to connect to the machine. It is a common
    problem that networking isn't setup properly in these boxes.
    Verify that authentication configurations are also setup properly,
    as well.If the box appears to be booting properly, you may want to increase
    the timeout ("config.vm.boot_timeout") value.
    ```

    [Private network not getting set up running under WSL2 (same Vagrantfile fine under Windows Vagrant) · Issue #11716 · hashicorp/vagrant](https://github.com/hashicorp/vagrant/issues/11716)

- wsl.conf 생성 : /etc/wsl.conf
    - private key 권한 변경 시 리눅스 파일 시스템 권한 설정 기능 필요
    - wsl.conf의 역할 : WSL 실행시 자동 구성 수행

        > Automatically configure functionality in WSL that will be applied every time you launch the subsystem using `wsl.conf`. This includes automount options and network configuration.

        > `wsl.conf` is located in each Linux distribution in `/etc/wsl.conf`.

    - automout  / metata

        > metadata	Whether metadata is added to Windows files to support Linux system permissions

    - 설정 내용

    ```bash
    > cat /etc/wsl.conf
    [automount]
    options = "metadata"
    ```

- 환경 변수 설정

    ```bash
    # for ansible + vagrant
    export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
    export PATH="$PATH:/mnt/d/virtualbox"
    export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATHPATH="/mnt/d/Ansible-Handson/"
    ```

    [Manage Linux Distributions](https://docs.microsoft.com/en-us/windows/wsl/wsl-config#set-wsl-launch-settings)

- 저자 github clone
    - 명령어 : git clone [git@github.com](mailto:git@github.com):geerlingguy/ansible-for-devops.git
    - 위치 :  /mnt/d/Ansible-Handson/ans-for-devops

## vm 생성
- vagrantfile

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.network :private_network, ip: "192.168.88.8"
  config.vm.hostname = "drupal.test"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 2048
  end
  
  #config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.synced_folder '.', '/vagrant'

  # Ansible provisioning.
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end
end
```
### config.vm.provision "ansible_local"
- config.vm.provision = ansible로 할경우 호스트 즉 windows10에 ansible을 설치 하라는 에러가 발생함. Windows10에서는 ansible을 설치 할 수 없으므로 ansible_local로 provision 해야 함

```bash
The Ansible software could not be found! Please verify
that Ansible is correctly installed on your host system.

If you haven't installed Ansible yet, please install Ansible
on your host system. Vagrant can't do this for you in a safe and
automated way.
Please check https://docs.ansible.com for more information.
```

### synced folder : config.vm.synced_folder '.', '/vagrant'
- ansible_local provision을 할 경우 playbook이 호스와 게스트 공유폴더를 통해 공유 되어야 함
- 예전 Episode에서슨 synced folder bug로 disable 권고 → bug 해결 : [https://github.com/hashicorp/vagrant/pull/12056](https://github.com/hashicorp/vagrant/pull/12056)

## Drupal 설치
- ansible_local provision을 통해 Drupal 설치
- playbook.yml 등 설치 참고 : https://github.com/geerlingguy/ansible-for-devops/tree/master/drupal
- 설치 결과
  
```bash
> vagrant provision
==> default: Running provisioner: ansible_local...
    default: Installing Ansible...
    default: Running ansible-playbook...

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
ok: [default]

TASK [Update apt cache if needed.] *********************************************
ok: [default]

TASK [Get software for apt repository management.] *****************************
changed: [default]

TASK [Add ondrej repository for later versions of PHP.] ************************
changed: [default]

TASK [Install Apache, MySQL, PHP, and other dependencies.] *********************
changed: [default]

TASK [Disable the firewall (since this is for local dev only).] ****************
changed: [default]

TASK [Start Apache, MySQL, and PHP.] *******************************************
ok: [default] => (item=apache2)
ok: [default] => (item=mysql)

TASK [Enable Apache rewrite module (required for Drupal).] *********************
changed: [default]

TASK [Add Apache virtualhost for Drupal.] **************************************
changed: [default]

TASK [Enable the Drupal site.] *************************************************
changed: [default]

TASK [Disable the default site.] ***********************************************
changed: [default]

TASK [Adjust OpCache memory setting.] ******************************************
changed: [default]

TASK [Create a MySQL database for Drupal.] *************************************
changed: [default]

TASK [Create a MySQL user for Drupal.] *****************************************
[WARNING]: Module did not set no_log for update_password
changed: [default]

TASK [Create a MySQL user for Drupal.] *****************************************
changed: [default]

TASK [Download Composer installer.] ********************************************
changed: [default]

TASK [Run Composer installer.] *************************************************
changed: [default]

TASK [Move Composer into globally-accessible location.] ************************
changed: [default]

TASK [Ensure Drupal directory exists.] *****************************************
changed: [default]

TASK [Check if Drupal project already exists.] *********************************
ok: [default]

TASK [Create Drupal project.] **************************************************
changed: [default]

TASK [Add drush to the Drupal site with Composer.] *****************************
changed: [default]

TASK [Install Drupal.] *********************************************************
changed: [default]

RUNNING HANDLER [restart apache] ***********************************************
changed: [default]

PLAY RECAP *********************************************************************
default                    : ok=24   changed=20   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

> ssh vagrant@172.17.47.225 -p 2222
vagrant@172.17.47.225's password:
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-42-generic x86_64)
```

- 사이트 접속 : http://[http://192.168.88.8/](http://192.168.88.8/)
    - vm 생성시 지정했던 IP 192.168.88.8로 웹브라우저를 통해 접속 가능
    - private ntework 즉 virtual host-only network로 호스트 - 게스트 vm간 통신 가능

![이미지](/assets/images/drupal.png)