---
layout: post
title: Ubuntu 16.04 각종 프로그램 설치 정리
---

### Chrome 설치
Download the package (64 bit):

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

Install the package, forcing install of dependencies:

```bash
sudo dpkg -i --force-depends google-chrome-stable_current_amd64.deb
```

In case any dependencies diddnt install (you would have a warning or failure message for this), you can force them via:

```bash
sudo apt-get install -f
```

Note: refer to the link above for 32 bit systems.

### Atom 설치

```bash
$ sudo add-apt-repository ppa:webupd8team/atom
$ sudo apt-get update
$ sudo apt-get install atom
```

### 스크린샷(캡쳐) 도구
우분투에 기본으로 탑재되어 있어요. 아래와 같이 시스템 설정에서 단축키로 이용이 가능합니다.

![20170313_post_1](https://cloud.githubusercontent.com/assets/13127455/23853669/f09db888-0830-11e7-9fda-6fb04dbe0a6e.png)

### Terminator 설치
기본으로 설치되어 있는 터미널은 창분할이 안되는 단점이 있어서 창분할이 지원되는 Terminator를 사용합니다.
```bash
$ sudo apt-get install terminator
```

### 참고자료
- [Ubuntu Gnome 터미널 추천 - Terminator](http://programmingsummaries.tistory.com/361)
